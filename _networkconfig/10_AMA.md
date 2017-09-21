---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

As a system administrator of an agency, you may want to provide higher privileges to users when they use their PIV/CAC card for login. In such a scenatio, you can utilize the Authentication Mechanism Assurance (AMA) feature of Windows Active Directory (AD). When the AMA is enabled, it will allow you to insert a group policy from the certificate into the authentication token.


{% include info-alert.html content=" AMA does not offer an option to require a specific login method (e.g., PIV login)." %}

## Windows Server® 2012 AD DS and Later

* Use the Windows Registry Editor to set the _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001

* This PowerShell script for the Federal Common and DoD Certificate Policies simplifies Microsoft TechNet's steps for Windows Server 2012:&nbsp;&nbsp;[AMA Certificate Issuance OIDs](https://github.com/GSA/ficam-scripts/blob/auth-mech-assurance/_AMA/CertificateIssuanceOIDs.ps1.txt){:target="_blank"}.

## Windows Server® 2008 R2 AD DS

* Go to:&nbsp;&nbsp;[Windows Server 2008 R2 AD DS Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx)[:target=_"blank"}.
* Set the _Domain Functional Level_ to _Windows Server 2008 R2_.
* Add a group membership to the user’s Kerberos token. When a user's PIV login is authenticated, it will activate the group membership.

### Hotfix for Windows® 2008 R2 Key Distribution Center (KDC) Error

* A Windows Server® 2008 R2-based Domain Hotfix corrects the known KDC error, "Access tokens are not updated correctly when you enable authentication mechanism assurance in a Windows Server 2008 R2-based domain." Go to:&nbsp;&nbsp; [Microsoft Hotfix](http://support.microsoft.com/kb/2771254){:target="_blank"}. 
