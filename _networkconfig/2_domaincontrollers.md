---
layout: default
title: Domain Controllers
collection: networkconfig
permalink: networkconfig/domaincontrollers/
---
# How do I issue, generate, and install a domain controller certificate?

These procedures are intended for network and system administrators, or other IT professionals, who are responsible for the day-to-day network operations of Federal Government agencies. As part of their roles, these professionals will be authorized by their agencies to manage various aspects of their networks' Domain Controllers, including the creation of certificate profiles and being knowledgeable about how domain-controller certificates are issued and installed. Domain Controllers must have certificates in order for employees to use PIV card credentials for network authentication. These pages present detailed information about how domain-controller certificate profiles and certificates are issued.  

{% include alert-info.html heading = "Devices authenticate too!" content="When your users are using certificates to authenticate to the network, the Domain Controllers are also authenticating as devices that use certificates. This system works together to create secure connections. To learn more, click on the links below or search for online resources that discuss Public Key Cryptography for Initial Authentication (PKINIT) protocols." %}

- [Domain Controller Certificate Profiles](#domain-controller-certificate-profiles)
- [Issuing Domain Controller Certificates](#issuing-domain-controller-certificates)

## Domain controller certificate profiles

Domain Controller certificates must be issued with a set of specific extensions and values.  The certificate for each Domain Controller must meet the following requirements:

- The certificate **Key Usage** extension must contain:

            Digital Signature, Key Encipherment

- The certificate **Enhanced Key Usage** extension must contain:

            Client Authentication (1.3.6.1.5.5.7.3.2)
            Server Authentication (1.3.6.1.5.5.7.3.1)

- The certificate **Subject Alternative Name** extension must contain the Domain Name System (DNS) qualifier and fully qualified Domain controller name.  For example:

            DNS Name=controller1.intranet.agency.gov

- The certificate **Subject Alternative Name** must also contain the Domain Controller's Global Unique Identifier (GUID) (i.e., for the "Domain Controller object"). 

  * To determine the Domain Controller's GUID, start **Ldp.exe** and locate the **domain-naming context**. 
  * Double-click on the **name of the Domain Controller** whose GUID you want to view.
  
    > The list of attributes for the Domain Controller object contains **"Object GUID" followed by a long number**. The number is the object GUID. For example:

            Other Name: 1.3.6.1.4.1.311.25.1 = ac 4b 29 06 bb d6 5d 4f e3 9c 4c ab c3 6a 55 d9

    > The Domain Controller's certificate must be installed in the domain controller's local computer's _personal certificate store_, as described below in the _Generate and install Domain Controller certificate_ procedures.

## Issue Domain Controller certificates

Each U.S. Federal Government's Civilian agency has information-security policies that guide its decision-making about whether its Domain Controller <!-- More than one DC? More than one certificate possible? -->certificate should be issued by the agency's **local enterprise Certificate Authority (CA)** or whether a Federal Public Key Infrastructure (FPKI)-managed and certified CA should issue it. Providing a common guide and recommendation is challenging, as each agency should follow its own policies. However, we do not recommend that agencies set up a local enterprise CA just to issue Domain Controller certificates. The best option is to collaborate with the agency Chief Information Security Officer (CISO) (or the Information Security Office), who can give definitive direction and has oversight for managing CAs and ensuring that security protections are in place.

## Generate and install Domain Controller certificate

_**Use Case:** We would like to use a local enterprise Microsoft CA to issue a Domain Controller certificate to the Domain Controller server. The server must have a certificate installed with the appropriate fields/values as a prerequisite to enabling PIV credential login for domain-connected devices._

  > **Note:** These procedures are accurate for using Microsoft 2012 Server, Standard Edition, for CA and Domain Controller servers (as of March 2017).

### Prerequisite

  * The server that hosts the CA must be on the domain

### Install CA role

  1. Log on to the CA server as a member of the **Enterprise Administrators** group.
  2. Open **Server Manager**
  3. Click **Manage** , and then click **Add Roles and Features**.
  4. Proceed through the Add Roles and Features Wizard, choosing the following options:
     1. Server Roles: _Active Directory Certificate Services_
     2. AD CS Roles Services: _Certification Authority_ 
  5. On the Results page, click **Configure Active Directory Certificate Services on the destination server**.
  6. Proceed through the AD CS Configuration, choosing the following options as necessary:
  * Role Service: _Certification Authority_ 
  * Setup Type: E_nterprise CA_ 
  * CA Type: _Root CA_
  * Private Key: _Create a new private key_ 
  * Cryptography: _RSA#Microsoft Software Key Storage Provider, 2048 bit, SHA-256_ 6e
  * CA Name should use Recommended naming convention:
        dc=[_AD suffix_], dc=[_AD domain_], cn=[_certification authority name_], 
        e.g. dc=_gov_, dc=_[AgencyName]_, cn=_[AgencyName] __NPE__ CA1_ 
  * Validity Period: _6 years_ 
  * Certificate Database: _&lt;your preference&gt;_ 



**Configure CA Template for Domain Controller**

_\* Certificate templates are only available on Enterprise CAs_

7. Log on to the CA server as a member of the **Enterprise Administrators** group
8. Open the certificate templates MMC snap-in (i.e. **certtmpl.msc** )
9. Right-click the **Domain Controller Authentication** template and click **Duplicate Template**
10. Under the **Compatibility Tab** , modify the **Compatibility Settings** for both the CA and certificate recipients to as high as possible (e.g. **Windows Server 2012 R2, Windows 7 / 2008 R2** )
11. Under the **General tab** :
  * Recommend renaming template to: _&lt;Your organization&gt; - Domain Controller Authentication_
  * Recommend modifying validity period to:  _3 years_
  * Recommend modifying Renewal period to: _6 weeks_
12. Under the **Cryptography tab** :
  * Set minimum key size to 2048
  * If possible, set Request hash to SHA256
13. Open the CA console (i.e. **certsrv.msc** )
14. In the console tree, click the name of the CA
15. In the details pane, double-click **Certificate Templates**
16. In the console tree, right-click **Certificate Templates** , click **New** , and then click **Certificate Template To Issue**
17. Select and enable the certificate template that were created in step 9 above, and then click **OK**

**Auto-enroll Domain Controller Certificate Using Group Policy Object (GPO)**

18. Log on to the Domain Controller server as a member of the **Enterprise Administrators** group
19. Open the GPMC (i.e. **gpmc.msc** )
20. Within the appropriate GPO, navigate to _Computer Configuration\Policies\Windows Settings\Security Settings\Public Key Policies\_
21. Configure **Certificate Services Client – Auto-Enrollment** with the following options:
  * Configuration Model: _Enabled_
  * Renew Expired Certificates, Update Pending Certificates, Remove Revoked Certificates: _Check_
  * Update Certificates That Use Certificate Templates: _Check_
22. You can now force the group policy to update via command-line: _gpupdate /force_ or wait for the group policy to update on its own
23. If successful, you should see a new DC cert in the Certificate (Local Computer) -&gt; Personal -&gt; Certificates folder. _(_e. _open MMC.exe -&gt; File -&gt; Add/Remove Snap-in -&gt;Certificates -&gt;Computer account -&gt;Local computer)._ If you look at the furthest tab called &quot;Certificate Template&quot; you should see a cert generated with the custom template you created in step 9.
