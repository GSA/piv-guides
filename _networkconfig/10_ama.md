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

A Federal employee authenticates to the agency's intranet using a PIV credential, and attempts to access an application hosted by a different federal agency. 
 
- The application is restricted to only allow users access who have authenticated with a valid PIV Authentication Certificate. 
- All other users are denied access to the website. 
 
This Federal employee successfully accesses the other federal agency application with minimal inputs. 
 
This Federal employee is successful because:

- the employee's home agency has a Federation Service installed, and
- the employee's home agency has integrated with the other federal agency's Federation Service

During and after logon to the network, the following steps are executed without the Federal employee's intervention:
 
1.	The PIV Authentication Certificate is parsed,
2.  The Policy OID asserted within the certificate allows Microsoft AD on the home agency network to assign the user to a group specifically for PIV credential authenticated users, 
2.	The user's session is granted a Kerberos ticket that includes the additional group membership,
2.  The user browses to the other federal agency application,
2.  The user's browser is redirected to their home agency Federation Service,
2.  The Federation Service at the home agency finds the Kerberos ticket for the user's session,
2.  A Security Assertion Markup Language (SAML) assertion is created by the Federation Service (this is a token translation),
2.  The SAML assertion includes the AD group membership information signifying that the user authenticated with a PIV credential,
2.  The user's browser is redirected back to the other federal agency application,
2.  The user is successfully authenticated with the valid SAML assertion, and
2.  The federal agency application is configured to only allow access to users who are authenticated using a PIV credential. 

In this use case and steps, the user did **not** have to authenticate directly with the PIV credential to the other agency's application.  A federation model was used.    

{% include alert-info.html content="One example to view this implementation pattern is Max.gov.  At the Max.gov login page, the bottom section contains the Login with Agency icons.  Each of those icons redirects the user back to their home agency federation services." %}


#### Authentication Pass-Through for Integrated Windows Authentication

A Federal employee authenticates to their Agencies intranet using a PIV credential and attempts to access a local SharePoint site. 

- The SharePoint site is restricted to only allow users access who have authenticated with a valid PIV Authentication Certificate. 
- All other users are denied access to the SharePoint site. 
 
The Federal employee successfully accesses the local SharePoint site.
 
1.	The PIV Authentication Certificate is parsed,
2.  The Policy OID asserted within the certificate allows Microsoft AD on the home agency network to assign the user to a group specifically for PIV credential authenticated users, 
2.	The user's session is granted a Kerberos ticket that includes the additional group membership, and
2.  The SharePoint site is configured to only allow access to users who are authenticated using a PIV credential.
 

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


