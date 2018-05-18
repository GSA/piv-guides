---
layout: default
title: Authentication Assurance
collection: networkconfig
permalink: networkconfig/ama/
---

When a user authenticates to your network and you've enabled Single Sign-on to applications inside your network domain, you need to know which of these authenticators was used: 

- A username and password 
- A PIV credential
- An alternate authenticator  
  
You need to know the type of authenticator to implement increasingly granular authorization policies, and grant or deny a user access to information available from applications and shared network resources. 

To grant a user access, based on the type of authenticator used, you can use a Windows Active Directory (AD) feature called _Authentication Mechanism Assurance (AMA)_. AMA allows you to add a group membership identifier to the user’s Kerberos token.

{% include alert-warning.html content="Do not use AMA to provide privileged user access." %}

AMA is available for domains operating on Windows Server 2008 R2 and later versions. 

- [Implementation](#implementation)
- [Testing](#testing)
- [Use Case Scenarios](#use-case-scenarios)
- [Other Considerations](#other-considerations)

## Implementation
You can use this PowerShell script [CertificateIssuanceOIDs.ps1](https://github.com/GSA/ficam-scripts-public/tree/master/_ama){:target="_blank"} to import and set up a list of certificate issuance policies. This script:

- Contains a list of certificate issuance policy object identifiers (OIDs) used by U.S. Federal Government agencies
- Creates security groups with the same names as the policies 
- Links the policies to the security groups

You can run the script with a few simple steps.

- You'll need to specify the Group Distinguished Name (GroupDN) within the script. This targets where you want to create the security groups in your network directory: 

  - `CertificateIssuanceOIDs.ps1 -GroupDN \<group DN string>`
  - For example: `CertificateIssuanceOIDs.ps1 -GroupDN 'OU=Groups,OU=Administrators,DC=agency,DC=gov'`

- After downloading this script, you may need to change the [PowerShell script execution policy](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-5.1&viewFallbackFrom=powershell-Microsoft.PowerShell.Core){:target="_blank"} to execute the script or sign the script to execute it.

An sample output from the script is shown below: 

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

**Note:**&nbsp;&nbsp;If the GroupDN is not entered in the command line when executing the script, it will prompt for the input.

```
  PS C:\> C:\AMA\Script\CertificateIssuanceOIDs.ps1 
  cmdlet ama-script.ps1 at command pipeline position 1
  Supply values for the following parameters:
  GroupDN: ou=groups,ou=security,dc=agency,dc=gov
==============================================
  GroupDN entered is ou=groups,ou=security,dc=agency,dc=gov

```

## Testing
To test the output on your network domain, log in with your PIV credential and check the groups assigned.  

- Authenticate with your PIV credential
- From the command line: `C:\whoami /groups`

```
  agency\id-fpki-common-authentication   Group  S-1-5-21-179144328 1-1764752353-2202401552-1113   
  Mandatory group, Enabled by default, Enabled group
```

## Use Case Scenarios

### Authentication Pass-Through to a Federation Service

A federal employee authenticates to the agency's intranet using a PIV credential and attempts to access an application hosted by a different federal agency. 
 
- The application is restricted to allow access by only users who have authenticated with a valid PIV Authentication Certificate. 
- All other users are denied access to the application. 
 
This federal employee successfully accesses the other federal agency's application with minimal inputs. The employee is successful because:

- The employee's home agency has a Federation Service installed, and
- The employee's home agency has integrated with the other agency's Federation Service

During and after the employee's logon to the network, the following steps were executed without the employee's intervention:
 
1.	The PIV authentication certificate is parsed
2.  The certificate policy OID asserted allows Microsoft AD on the home agency's network to assign the user to a group specifically for PIV authenticated users 
2.	The user's session is granted a Kerberos ticket that includes the additional group membership
2.  The user browses to the other federal agency's application
2.  The user's browser is redirected to his/her home agency's Federation Service
2.  The Federation Service at the home agency finds the Kerberos ticket for the user's session
2.  A Security Assertion Markup Language (SAML) assertion is created by the Federation Service (This is a token translation.)
2.  The SAML assertion includes the AD group membership information that identifies that this user authenticated with a PIV credential
2.  The user's browser is redirected back to the other federal agency's application
2.  The user is successfully authenticated with the valid SAML assertion
2.  The other federal agency's application is configured to allow access to only those users who have authenticated using a PIV credential 

In this Use Case and steps, the user did **not** have to authenticate directly with a PIV credential to the other agency's application.  A federation model was used.    

{% include alert-info.html content="One example for viewing this implementation pattern is Max.gov.  If you click on the upper right-hand Login button, you'll see the Max.gov LOGIN page. The bottom section allows you to click on an agency icon.  Each of these icons redirects the user back to that agency's Federation Service." %}

### Authentication Pass-Through for Integrated Windows Authentication

A federal employee authenticates to his/her agency's intranet using a PIV credential and attempts to access a local SharePoint site. 

- The SharePoint site is restricted to allow access to only those users who have authenticated with a PIV Authentication Certificate. 
- All other users are denied access to the SharePoint site. 
 
The federal employee successfully accesses the local SharePoint site. 

During and after the employee's logon to the network and attempt to access the SharePoint site, the following steps were executed without the employee's intervention:
 
1.	The PIV authentication certificate is parsed
2.  The certificate policy OID asserted allows Microsoft AD on the home agency's network to assign the user to a group specifically for PIV authenticated users
2.	The user's session is granted a Kerberos ticket that includes the additional group membership
2.  The SharePoint site is configured to only allow access to only those users who have authenticated using a PIV credential 
 

## Other Considerations and References
Use the Windows Registry Editor to set the _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:  

- `[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]`
- `"ChainWithIssuancePolicyOIDs"=dword:00000001`


Refer to [AMA Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx){:target=_"blank"} to understand the implementation of AMA.

