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
Go to:&nbsp;&nbsp;[AMA Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx)[:target=_"blank"} to understand the implementation of AMA.

### Windows PowerShell Script For Common Federal/DoD Certificate Policies
[CertificateIssuanceOIDs.ps1](https://github.com/GSA/ficam-scripts-public/tree/master/_ama){:target="_blank"} is a PowerShell script that imports a list of Federal Common and DoD Certificate certification policies. It simplifies Microsoft TechNet's steps for setting up the policies. The script has a list of policies to import grouped under different categories. You should only import the policies that are applicable to your agency.

### Windows® 2008 R2 Considerations
* You should raise the Domain Functional Level to Windows Server 2008 R2 if not already set.

* A Windows Server® 2008 R2-based Domain Hotfix corrects the known KDC error, "Access tokens are not updated correctly when you enable authentication mechanism assurance in a Windows Server 2008 R2-based domain." [Microsoft Hotfix](http://support.microsoft.com/kb/2771254){:target="_blank"}. No patch is requried for Windows Server® 2012 and later versions.

* Use the Windows Registry Editor to set the _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001
            
* Add a global group membership to the user’s Kerberos token. When a user's PIV/CAC login is authenticated, it will activate the group membership.
