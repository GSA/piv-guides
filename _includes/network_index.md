## Introduction to Network Authentication Guides

This section is for configuring your Windows based computer network to accept and potentially require PIV cards for authentication.

There are many useful articles and guides available online for you to review and use.  These guides outline in detail the point and click options for configurations and using generic smartcards.  

The information presented in this guide is to address some of your common questions and configurations *specific* to the US Federal Government, *PIV* smartcards, and US Federal civilian agency certificate authorities.  

### Assumptions
*  Users have PIV cards and PIV card readers
*  User workstations have the drivers to read the PIV cards
*  You're using Microsoft Active Directory to manage your Windows network
*  Domain Controllers are Microsoft 2008 R2 or above
*  User workstations joined to the network are Windows 7 or above
  * There are options for workstations that are Mac OS based and joined to a Windows network - to be covered in a separate guide


### Before You Get Started
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

To help contribute to this effort, please follow 'Submit Issues Here' link at the top right to access the GitHub page for this site and provide any feedback.