---
layout: page_collection
title: Ports and Protocols
collection: networkconfig
permalink: networkconfig/ports/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Difficulty: Moderate</em>
</div>
</div>

## Overview
This guide is for configuring your Windows based computer network to accept and potentially require PIV cards for authentication.

There are many useful articles and guides available online for you to review and use.  The online guides outline in detail the point and click options for configurations and using generic smartcards.  

The information presented in this guide is to address some of your common questions and configurations *specific* to the US Federal Government, *PIV* smartcards, and US Federal civilian agency certificate authorities.  

### Assumptions
*  Users have PIV cards and PIV card readers
*  User workstations have the drivers to read the PIV cards
*  You're using Microsoft Active Directory to manage your Windows network
*  Domain Controllers are Microsoft 2008 R2 or above
*  User workstations joined to the network are Windows 7 or above
  * There are options for workstations that are Mac OS based and joined to a Windows network - to be covered in a separate guide


#### Before You Get Started
One of the most common questions is "What are all the certificates and what do I do with them?" 

Explaining public key infrastructures and *the* Federal Public Key Infrastructure is an advanced topic and will be covered in additional guides.  For your needs, there are two basic principles to understand:

1.  Trust 
2.  Certificate *chains*

In the Federal Agencies, certificates may be issued to People (YOU), or Devices (SSL, Domain Controllers, Mobile Devices, etc).

Your PIV credentials contain certificates and private key pairs - that are issued to YOU as a person, and to the CARD as a Device that you have in your possession.  

To Trust YOU and your certificates, the workstations and network need to be configured for this trust.  Certificate chains are one of the necessary methods to configure this trust.

Certificate chains can be complex to explain, so let's use a parable:

Download the Federal Common Policy Certificate Authority (COMMON) trusted _root_ certificate

* [COMMON can be downloaded here](http://http.fpki.gov/fcpca/fcpca.crt)  
  * cn=Federal Common Policy CA, ou=FPKI, o=U.S. Government, c=US    
  * 90 5f 94 2f d9 f2 8f 67 9b 37 81 80 fd 4f 84 63 47 f6 45 c1  

Download the Intermediate Certificate Authority certificates

* [Intermediate Certificate Authority certificates] (http://http.fpki.gov/fcpca/caCertsIssuedByfcpca.p7c)
  * The file type (p7c) can be 
  * 
  *   

Identify and download any additional Intermediate Certificate Authority certificates

* You can generally ask your agency's information security team for help on the additional 
* You can also look at your PIV card and certificates

Are you ready to get started?  

#### Outline of Steps
1. [Checking the network for Ports and Protocols](#checking-the-network-for-ports-and-protocols)
2. Configuration considerations for Domain Controller certificates
2. [Addition of US Federal Certificate chains to the Trusted Root Certificate Authorities](#addition-of-us-federal-certificate-chains-to-the-trusted-root-certificate-authorities)
3. Publishing the US Federal Certificate chains to the NT Auth Store
4. [Associating PIV Credentials to the Active Directory User Accounts using altSecurityIdentities](#associating-piv-credentials-to-the-active-directory-user-accounts-using-altSecurityIdentities)
5. Configuring group policies for PIV (smartcard) logon

#### Checking the network for Ports and Protocols

The primary question answered during validation is: _Are you and the chain still trusted?_  You need to be able to validate the certificates during use.  Your workstations, servers and browsers may also need to retrieve the certificate chains we talked about [here](#before-you-get-started).

> Validation is performed using a variety of algorithms on different operating systems and with different cryptographic libraries. This section focuses on the _basics_ for common agency network configurations.  In addition, the LDAP protocol for retrieving revocation information is not preferred and is being increasingly deprecated; therefore LDAP is not included in this guide. 
{:class="alert"}

Validation occurs using one of two mechanisms, over the HTTP protocol:

*  On-line Certificate Status Protocol (OCSP): HTTP / Port 80
*  Certificate Revocation Lists (CRLs): HTTP / Port 80 

 
	
	
### Domain Controller certificates

Include:
Getting the GUID commands
certutil / command to query domain controllers for certs and status
extensions for domain controller certs
where to get domain controller certs and options


Work with the Federal Public Key Infrastructure management team to request a domain controller certificate for your domain controller(s). Each domain controller that is going to authenticate smartcard users must have a domain controller certificate.  

The certificate for each domain controller must meet the following specific format requirements:

*  The certificate must have a CRL distribution-point extension that points to a valid certificate revocation list (CRL).
    *  Optionally, the certificate Subject section should contain the directory path of the server object (the distinguished name), for example:  
            CN=controller1.agency.gov OU=Domain Controllers DC=agency DC=gov  
    *  The certificate Key Usage section must contain:  
            Digital Signature, Key Encipherment

    *  Optionally, the certificate Basic Constraints section should contain:

            [Subject Type=End Entity, Path Length Constraint=None]

    *  The certificate Enhanced Key Usage section must contain:

            Client Authentication (1.3.6.1.5.5.7.3.2)
            Server Authentication (1.3.6.1.5.5.7.3.1)

    *  The certificate Subject Alternative Name section must contain the Domain Name System (DNS) name. If SMTP replication is used, the certificate Subject Alternative Name section must also contain the globally unique identifier (GUID) of the domain controller object in the directory.
        *  To determine the Domain Controller GUID, start Ldp.exe and locate the domain-naming context. Double-click the name of the domain controller that you want to view. The list of attributes for that object contains "Object GUID" followed by a long number. The number is the GUID for that object. For example:

                Other Name: 1.3.6.1.4.1.311.25.1 = ac 4b 29 06 bb d6 5d 4f e3 9c 4c ab c3 6a 55 d9 DNS Name=controller1.agency.gov


*  The domain controller certificate must be installed in the local computer's certificate store.


### Addition of US Federal Certificate chains to the Trusted Root Certificate Authorities

The root certificate and intermediate CA certs are required by the domain controller to establish trust between the parent CA and the end users and applications. 

This allows the domain controller to issue trusted certificates to PIV cards within the directory and confirm the validity of smart card certificates during an access attempt.

Active Directory must be configured to trust a certification authority to authenticate users based on certificates from that CA. 

Both workstations and domain controllers must be configured to trust the certificates 

This task will configure Active Directory to trust the Certification Authority chain that signed the users' authentication certificates. To configure Active Directory with the signing CA Certificate chain:

1.	On your Active Directory Domain Controller server, select **Active Directory Users and Computers**
2.	In the **Management Console**, right click the **Domain** and click **Properties**
3.	Once you're on the **Group Policy Tab**, click **Open** to open the **Group Policy Management Console plug-in**
4.	Right Click **Default Domain Policy** and click **Edit**
5.	Expand the **Computer Configuration** section and open **Windows Settings > Security Settings > Public Key**
6.	Right click **Trusted Root Certification Authorities** and select **Import**
7.	Follow the prompts in the Wizard to import the **Root Certificate** for the CA and click OK

From here, follow these steps to import the intermediate certificate(s):

1.	Right click **Intermediate Certification Authorities** and select **Import**
2.	Follow the prompts in the Wizard to import the **Intermediate Certificate(s)** for the CA and click OK


### Publish the CA Certificates to the NTAuth Store

By publishing the CA certificate to the enterprise NTAuth store, the system administrator indicates that the CA is trusted to issue certain certificates. This allows the correct certificates to be issued to smartcards and thus enables logon through PIV card authentication.

This task will configure Active Directory to trust the CA chain that signed the users' authentication certificates. To configure Active Directory with the signing CA Certificate chain:

1.	On the Active Directory Domain Controller, launch an **elevated command prompt** to use the **certutil** utility
2.	To **Publish the Certificate** to the **Enterprise NTAuth store** type

        certutil –dpublish –f "path_to_root_CA_cert" NTAuthCA

3.	The CA is now trusted to issue certificates of this type


### Associating PIV Credentials to the Active Directory User Accounts using altSecurityIdentities

A portion of agencies may be using the User Principal Name (UPN) mapping to associate a PIV certificate to a user account.  In the UPN model:

* Each PIV credential can only be associated with ONE account
* The User Principal Name value from the Subject Alternate Name in the PIV authentication certificate is required to be populated 
* There is less flexibility for managing privileged accounts

You will find more flexibility in using the altSecurityIdentities mapping options which were made available in 2008.  In the altSecurityIdentities model:

* Each PIV credential can be associated with MORE THAN ONE account
* Six options from the certificate can be used to map to each account
* There is flexibility for managing privileged accounts
* Users are presented a User Name Hint to help choose which account to authenticate to

To help you configure and enable User Name Hints and altSecurityIdentities, there is documentation available freely online from sources.  The information provided here is to help you with PIV and US Federal government common challenges.

1. It is NOT required that you get updated PIV credentials and certificates without a UPN value populated
  * This is a common misconception
  * If your PIV credentials do have a UPN value in the Subject Alternative Name, this method will still work for your agency.  

1. Disable UPN Mapping
  * This is a registry setting and you must disable this setting on all domain controllers
  * [Link to the registry setting](https://technet.microsoft.com/en-us/library/ff520074(WS.10).aspx)
  
1. Map the user certificates to the altSecurityIdentities attribute for each account
  * You have six options from the certificates to use
  * A common challenge 

  
  
| Options       | Tag     | Example | Considerations |
| ------------- |:-------------:| -----:|-----:|
| Subject     | X509:\<S> | X509:\<S>C=US,O=U.S. Government,OU=General Services Administration,CN=LACHELLE LEVAN OID.0.9.2342.19200300.100.1.1=47001003151020 |   | 
| Issuer and Subject     | X509:\<I>\<S>  | X509:\<I>C=US,O=Entrust,OU=Certification Authorities,OU=Entrust Managed Services SSP CA\<S>C=US,O=U.S. Government,OU=General Services Administration,CN=LACHELLE LEVAN OID.0.9.2342.19200300.100.1.1=47001003151020 |   |
| Issuer and Serial Number | X509:\<I>\<SR> |    $1 |  
| SHA1 hash of public key| X509:\<SHA1-PUKEY> |    $1 |  
| RFC822 name | X509:\<RFC822>      |    $1 | 
| UPN     | X509:\<S> | $1600 | 

You can consider the pros and cons of each method for your agency.  The most common pros and cons are based on whether the attributes would need to be updated if a user receives an updated PIV credential.

| altSecurityIdentities       | Pro          | Con  |
| ------------- |:-------------:| -----:|
| Subject     |  | $1600 |
| Issuer and Subject     | X509:<I><S>      |   $12 |
| Issuer and Serial Number | X509:<I><SR>      |    $1 |  
| SHA1 hash of public key| X509:<SHA1-PUKEY>      |    $1 |  
| RFC822 name | X509:<SHA1-PUKEY>      |    $1 | 
| UPN     | X509:<S> | $1600 | 


There are helpful guides and links at the bottom of this page with public information on altSecurityIdentities and User Name Hints.  



To configure Active Directory one-to-one mapping using altSecurityIdentities attributes:

1.	Click Start, click Programs, click Administrative Tools, and click Active Directory Users and Computers.
2.	Expand the domain name node containing the user(s) to manage and click the Users folder. In the right pane, right-click the account to map and click Name Mappings.
3.	On the X.509 Certificates tab, click the Add button. Select the user certificate from the .cer file that should be mapped to the account.
4.	The Use Issuer for alternate security identity will be selected and appear gray by default because you need to use this for both one-to-one mapping and many-to-one mapping. 
Select the Use Subject for alternate security identity option to do one-to-one mapping. By unchecking this option, you will be doing many-to-one mapping. Click OK.
5.	Go to the section, testing the Mapping, to verify that this works.


### Configure group policies for PIV Authentication

This task describes 2 common configurations related to domain Group Policy Objects (GPO).

|  scforceoption  |  This security policy setting requires users to log on to a computer by using a smart card.  |  Enabled / Disabled  |
|  scremoveoption  |  This setting determines what happens when the smart card for a logged-on user is removed from the smart card reader.  |  No Action / Lock Workstation / Force Logoff / Disconnect if a Remote Desktop Services session  |

**scforceoption** directs client Windows computers to enforce PIV logon for users. It is important to understand the ramifications of executing this step.

When you select the Smart Card is required for interactive logon check box in the Active Directory (AD) user account properties, Windows automatically resets the user password to a random complex password. In addition, Windows adds the SMARTCARD_REQUIRED flag to the UserAccountControl user account attribute and sets the DONT_EXPIRE_PASSWORD flag on the user account. The latter ensures that the user's password never expires after the Smart Card is required for interactive logon option is selected.

When a user logs on to Windows either locally or remotely using a Remote Desktop session, the Windows client automatically checks for the presence of the SMARTCARD_REQUIRED flag. If the Smart Card is required for interactive logon option is set for the user, Windows rejects the logon attempt if it's not made with smart card credentials.

Again, upon activation of scforceoption, users will **no longer know the password** to their account and will be **required** to use their PIV for authentication. Care should be used if enabling this option.

To enable or disable either of these policies:

1.  Open the Group Policy Management Console
1.  In the GPMC console tree, double-click Group Policy Objects in the forest and domain containing the GPO that you want to edit.
1.  Right-click the GPO, and then click Edit.
1.  In the console tree, edit the settings as appropriate.



#### References

Elements of this guide were derived from a [Microsoft Knowledgebase Article](https://support.microsoft.com/en-us/kb/281245)
