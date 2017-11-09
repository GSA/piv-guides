---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

You may need to make privilege decisions in applications for your agency users when they log in with their PIV/CAC or client certificate credential versus another lower assurance authentication method. To help you do this, you can use a Windows Active Directory (AD) feature called _Authentication Mechanism Assurance (AMA)_. AMA allows you to add a global group membership to a user’s Kerberos token, based on the PIV/CAC's certificate policy.

AMA is available in Windows Server® 2008 R2 and later versions.

{% include info-warning.html content="Do not use AMA to provide privileged user access to servers." %}

### Understanding AMA
Go to:&nbsp;&nbsp;[AMA Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx){:target=_"blank"} to understand the implementation of AMA.

### Windows PowerShell Script For Common Federal/DoD Certificate Policies
[CertificateIssuanceOIDs.ps1](https://github.com/GSA/ficam-scripts-public/tree/master/_ama){:target="_blank"} is a PowerShell script that imports a list of Federal Common and DoD Certificate certification policies. It simplifies Microsoft TechNet's steps for setting up the policies. The script has a list of policies to import grouped under different categories. You should only import the policies that are applicable to your agency.

You may have to change the [powershell script execution policy](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-5.1&viewFallbackFrom=powershell-Microsoft.PowerShell.Core) to execute this script or sign the script to execute it after downloading.

An example output of the script for one policy is shown below.

     PS C:\> C:\AMA\Script\CertifateIssuanceOID.ps1
     Created OU=Administrators,DC=agency,DC=gov
     Created OU=Groups,OU=Administrators,DC=agency,DC=gov
     Created CN=id-fpki-common-authentication,OU=Groups,OU=Administrators,DC=agency,DC=gov
     2.16.840.1.101.3.2.1.3.13 -- Unknown ObjectId

     Localized name added to DS store.
     0: 1033,id-fpki-common-authentication
     CertUtil: -oid command completed successfully.
     Created CN=13.255922318A2AF32EC47D5B70735D4DB3,CN=OID,CN=Public Key Services,CN=Services,CN=Configuration,DC=agency,DC=gov
     AD AMA set for 2.16.840.1.101.3.2.1.3.13  id-fpki-common-authentication

### Windows® 2008 R2 Considerations
* You should raise the Domain Functional Level to Windows Server 2008 R2 if not already set.

* A Windows Server® 2008 R2-based Domain Hotfix corrects the known KDC error, "Access tokens are not updated correctly when you enable authentication mechanism assurance in a Windows Server 2008 R2-based domain." [Microsoft Hotfix](http://support.microsoft.com/kb/2771254){:target="_blank"}. No patch is requried for Windows Server® 2012 and later versions.

* Use the Windows Registry Editor to set the _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:

     [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
     "ChainWithIssuancePolicyOIDs"=dword:00000001
            
* Add a global group membership to the user’s Kerberos token. When a user's PIV/CAC login is authenticated, it will activate the group membership.
