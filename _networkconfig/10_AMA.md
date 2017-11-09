---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

You may need to make privilege decisions in applications for your agency users when they log in with their PIV/CAC credential versus another lower assurance authentication method. To help you do this, you can use a Windows Active Directory (AD) feature called _Authentication Mechanism Assurance (AMA)_. AMA allows you to add a global group membership to a user’s Kerberos token, based on the PIV/CAC’s certificate policy and using the PIV/CAC for log in.

AMA is available in Windows Server 2008 R2 and later versions.

{% include info-warning.html content="Do not use AMA to provide privileged user access to servers." %}

* Go to:&nbsp;&nbsp;[Windows Server 2008 R2 AD DS Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx)[:target=_"blank"} to understand the implementation of AMA.

* Use the Windows Registry Editor to set the _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001

* This PowerShell script can be used to automate the setup for the Federal Common and DoD Certificate Policies. It simplifies Microsoft TechNet's steps for Windows Server 2012:&nbsp;&nbsp;[AMA Certificate Issuance OIDs](https://github.com/GSA/ficam-scripts-public/tree/auth-mech-assurance/_ama){:target="_blank"}.

* Set the _Domain Functional Level_ to _Windows Server 2008 R2_.
* Add a global group membership to the user’s Kerberos token. When a user's PIV/CAC login is authenticated, it will activate the group membership.

### Hotfix for Windows® 2008 R2 Key Distribution Center (KDC) Error

* A Windows Server® 2008 R2-based Domain Hotfix corrects the known KDC error, "Access tokens are not updated correctly when you enable authentication mechanism assurance in a Windows Server 2008 R2-based domain." [Microsoft Hotfix](http://support.microsoft.com/kb/2771254){:target="_blank"}.

