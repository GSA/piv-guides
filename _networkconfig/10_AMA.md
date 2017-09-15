---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

Logging in remotely&mdash;whether from home, on travel, or at the local bookstore&mdash;increases the risk that attackers might be able to hack into government systems and access sensitive information. 

This guide can help you to enhance the security of high-risk logins by configuring Microsoft Windows' Active Directory (AD) Domain Service's (DS) _Authentication Mechanism Assurance (AMA)_ on your Windows Server® 2012 or 2008 R2.

## Windows Server® 2012 AD DS and Later (No Patch Required)

* Use the Windows Registry Editor to enable _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001

* This Power Shell Script for the Federal Common and DoD Certificate Policies simplifies the Microsoft TechNet steps for Windows Server 2012. Go to:&nbsp;&nbsp;[AMA Certificate Issuance OIDs](https://github.com/GSA/ficam-scripts/blob/auth-mech-assurance/_AMA/CertificateIssuanceOIDs.ps1.txt){:target="_blank"}.

## Windows Server® 2008 R2 AD DS

* Go to:&nbsp;&nbsp;[Windows Server 2008 R2 AD DS Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx)[:target=_"blank"}.

* Set the _Domain Functional Level_ to _Windows Server 2008 R2_:

* You have an option to add a group membership to the user’s Kerberos token. When a user's PIV login is authenticated, it activates the group membership.

### Patch for Key Distribution Center (KDC) Error

* The Windows Server® 2008 R2 Patch corrects the known KDC error. Go to:&nbsp;&nbsp; [Hotfix](http://support.microsoft.com/kb/2771254){:target="_blank"}. 
