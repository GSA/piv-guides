---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

As a system administrator of an agency, you may want to provide higher privileges to users when they use their PIV/CAC card for login. In such a scenatio, you can utilize the Authentication Mechanism Assurance (AMA) feature of Windows Active Directory (AD). When the AMA is enabled, it will allow you to insert an administrator designated global group membership based on the certificate policy of the PIV/CAC card into the authentication Kerberos token.

{% include info-alert.html content=" AMA does not offer an option to require a specific login method (e.g., PIV login)." %}

As an example, you want to allow Joe read access to sharepoint documents if Joe has a certificate with a policy OID 2.16.840.1.101.3.2.1.12.6 and policy name 'id-eca-medium-hardware-pivi'. You also want Julie to have write privileges since she has a certificate with a policy OID 2.16.840.1.101.3.2.1.3.16 and name id-fpki-common-high. You will setup these 2 policies in AD using any of the available methods listed below and then assign group memberships based on these policy OIDs to read and write access to sharepoint.

{% include info-alert.html content=" Do not use AMA to provide privileged access to servers." %}

## Windows Server® 2012 AD DS and Later

* Use the Windows Registry Editor to set the _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001

* This PowerShell script for the Federal Common and DoD Certificate Policies simplifies Microsoft TechNet's steps for Windows Server 2012:&nbsp;&nbsp;[AMA Certificate Issuance OIDs](https://github.com/GSA/ficam-scripts/tree/auth-mech-assurance/_AMA){:target="_blank"}. <--This link will change after the pull request is merged with staging -->

## Windows Server® 2008 R2 AD DS

* Go to:&nbsp;&nbsp;[Windows Server 2008 R2 AD DS Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx)[:target=_"blank"}.
* Set the _Domain Functional Level_ to _Windows Server 2008 R2_.
* Add a group membership to the user’s Kerberos token. When a user's PIV login is authenticated, it will activate the group membership.

### Hotfix for Windows® 2008 R2 Key Distribution Center (KDC) Error

* A Windows Server® 2008 R2-based Domain Hotfix corrects the known KDC error, "Access tokens are not updated correctly when you enable authentication mechanism assurance in a Windows Server 2008 R2-based domain." [Microsoft Hotfix](http://support.microsoft.com/kb/2771254){:target="_blank"}. 
