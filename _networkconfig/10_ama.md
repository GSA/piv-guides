---
layout: default
title: Authentication Assurance
collection: networkconfig
permalink: networkconfig/ama/
---

When a user authenticates to the network and you've enabled single-sign-on to applications inside your network domain, you need to know what type of authenticator was used: 

- A username and password, 
- A PIV credential, or
- An alternate authenticator  

You need to know the type of authenticator to help you implement increasingly granular authorization policies, and grant or deny access to information in applications and shared network resources.   

You can use a Windows Active Directory (AD) feature called _Authentication Mechanism Assurance (AMA)_. AMA allows you to add a group membership identifier to the user’s Kerberos token, based on the type of authenticator used.

AMA is available for domains operating on Windows Server 2008 R2 and later versions. 

- [Use Case Scenarios](#use-case-scenarios)
- [Implementation](#implementation)
- [Testing](#testing)
- [Other Considerations](#other-considerations)

{% include alert-warning.html content="Do not use AMA to provide privileged user access." %}

### Use Case Scenarios

#### Authentication Pass-Through to a Federation service

A Federal employee authenticates to their Agencies intranet using smartcard logon with their PIV Card and attempts to access a local SharePoint site. 
 
The SharePoint site is restricted to only allow users access who have authenticated with a valid PIV Authentication Certificate. All other users are denied access to the SharePoint site. 
 
This Federal employee successfully accesses the local SharePoint site.
 
This Federal employee is successful because at logon to their workstation their PIV Authentication Certificate is parsed and the Policy OID asserted within the certificate allows Microsoft Active Directory (AD) to place the user in an additional AD group. This AD group membership is specifically for PIV Card authenticated users. The SharePoint site is configured to restrict access to all users who are not members of the PIV Card authenticated users group.

#### Authentication Pass-Through for Integrated Windows Authentication

A Federal employee authenticates to their Agencies Intranet using smartcard logon with their PIV Card and attempts to access to a website hosted by a different Federal Agency. 
 
The website is restricted to only allow users access who have authenticated with a valid PIV Authentication Certificate. All other users are denied access to the website. 
 
This Federal employee successfully accesses the other Federal Agency website.
 
This Federal employee is successful because the employee’s Agency has an Active Directory Federation Services (ADFS) trust relationship established with the other Federal Agency hosting the website. At logon to their workstation:
 
1.	Their PIV Authentication Certificate is parsed and the Policy OID asserted within the certificate allows Microsoft AD to place the user in an additional AD group specifically for PIV Card authenticated users; and
2.	They are granted a Kerberos ticket that includes the additional AD group membership.
 
This Federal employee attempts to access the other Federal Agency website and is redirected to their Agencies ADFS server to authenticate. Their Kerberos ticket is presented to the ADFS server and they are authenticated. After the successful authentication to ADFS a Security Assertion Markup Language (SAML) assertion is created. The SAML assertion includes the AD group membership information signifying them as having a valid PIV Card. They are redirected back to the other Federal Agency website and are successfully authenticated with the valid SAML assertion. The website is configured to restrict access to all users who are not members of the PIV Card authenticated users group. 

### Implementation
You can use this PowerShell script [CertificateIssuanceOIDs.ps1](https://github.com/GSA/ficam-scripts-public/tree/master/_ama){:target="_blank"} to import a list of certificate issuance policies.  

This script:

- Simplifies the steps for setting up the policies 
- Contains the list of certificate policy object identifiers in use by US Federal Government agencies only
- Creates security groups with the same name as the certificate issuance policies 
- Links the policies to the groups

You will provide the script the Group Distinguished Name (DN) for where to create the security groups in your network directory. 

- CertificateIssuanceOIDs.ps1 -GroupDN \<group DN string>
- Example:  CertificateIssuanceOIDs.ps1 -GroupDN 'OU=Groups,OU=Administrators,DC=agency,DC=gov'

You may have to change the [powershell script execution policy](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-5.1&viewFallbackFrom=powershell-Microsoft.PowerShell.Core){:target="_blank"} to execute this script or sign the script to execute it after downloading.

An sample output of the script is shown below. You have to specify the location (GroupDN) where you want the AD groups to be created.

```
  PS C:\> C:\AMA\Script\CertificateIssuanceOIDs.ps1 -GroupDN 'ou=groups,ou=security,dc=agency,dc=gov'
  
  Created CN=id-fpki-common-authentication,ou=groups,ou=security,dc=agency,dc=gov  
  2.16.840.1.101.3.2.1.3.13 -- Unknown ObjectId  
  
  Localized name added to DS store.
  0: 1033,id-fpki-common-authentication  
  CertUtil: -oid command completed successfully.
  
  Created CN=13.255922318A2AF32EC47D5B70735D4DB3,CN=OID,CN=Public Key Services,CN=Services,CN=Configuration,DC=agency,DC=gov  
  AD AMA set for 2.16.840.1.101.3.2.1.3.13  id-fpki-common-authentication  
```

If the GroupDN is not entered in the command line while executing the script, it will prompt for the input.

```
PS C:\> C:\AMA\Script\CertificateIssuanceOIDs.ps1 
cmdlet ama-script.ps1 at command pipeline position 1
Supply values for the following parameters:
GroupDN: ou=groups,ou=security,dc=agency,dc=gov
==============================================
Group DN entered is ou=groups,ou=security,dc=agency,dc=gov.

```

### Testing
To test the output on your network domain, you will login with your PIV credential and check the groups assigned.  

- Authenticate with your PIV credential
- From the command line: C:\whoami /groups

```
  agency\id-fpki-common-authentication   Group  S-1-5-21-179144328 1-1764752353-2202401552-1113   
  Mandatory group, Enabled by default, Enabled group
```
 

### Other Considerations and References
Use the Windows Registry Editor to set the _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:  

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
- "ChainWithIssuancePolicyOIDs"=dword:00000001


Refer to [AMA Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx){:target=_"blank"} to understand the implementation of AMA.


