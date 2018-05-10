---
layout: default
title: Authentication Assurance
collection: networkconfig
permalink: networkconfig/ama/
---

When a user authenticates and you've enabled single-sign-on to applications inside your network domain, you may need to know what type of authenticator a user used: 

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

Authentication Pass-Through to a Federation service
Authentication Pass-Through for Integrated Windows Authentication


### Implementation
You can use this PowerShell script [CertificateIssuanceOIDs.ps1](https://github.com/GSA/ficam-scripts-public/tree/master/_ama){:target="_blank"} to import a list of certificate issuance policies.  

This script:

- Simplifies the steps for setting up the policies 
- Contains the list of certificate policy object identifiers focused on US Federal government agencies 
- Creates security groups with the same name as the certificate issuance policies 
- Links the policies to the groups

You need to modify the script for the following variables:

- **insert variable here and what the modification should be**

You may have to change the [powershell script execution policy](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-5.1&viewFallbackFrom=powershell-Microsoft.PowerShell.Core){:target="_blank"} to execute this script or sign the script to execute it after downloading.

An sample output of the script is shown below.

```
  PS C:\> C:\AMA\Script\CertificateIssuanceOIDs.ps1  
  Created CN=id-fpki-common-authentication,OU=Groups,OU=Administrators,DC=agency,DC=gov  
  2.16.840.1.101.3.2.1.3.13 -- Unknown ObjectId  
  
  Localized name added to DS store.
  0: 1033,id-fpki-common-authentication  
  CertUtil: -oid command completed successfully.
  
  Created CN=13.255922318A2AF32EC47D5B70735D4DB3,CN=OID,CN=Public Key Services,CN=Services,CN=Configuration,DC=agency,DC=gov  
  AD AMA set for 2.16.840.1.101.3.2.1.3.13  id-fpki-common-authentication  
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


