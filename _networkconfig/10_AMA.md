---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

Logging in remotely&mdash;whether from home, on travel, or at the local bookstore&mdash;increases the risk that attackers might be able to hack into government systems and access sensitive information. 

This guide can help you to can increase the security of high-risk logins by configuring Microsoft Windows' Active Directory (AD) Domain Service's (DS) _Authentication Mechanism Assurance (AMA)_ on your Windows server.

## Windows Server 2012® AD DS and Later

* No patch is required. Enable **AMA Priority** above **_Most Recently Issued Superior Certificate Heuristic_** by using the Windows Registry Editor:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001

* This Power Shell Script for the Federal Common and DoD Certificate Policies simplifies the Microsoft TechNet steps for Windows Server 2012: 

    https://github.com/GSA/ficam-scripts/blob/auth-mech-assurance/_AMA/CertificateIssuanceOIDs.ps1.txt

## Windows Server® 2008 R2 AD DS

* Set the **Domain Functional Level** to **_Windows Server 2008 R2_**:

    https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx

* AMA gives you the option to add a group membership to the user’s Kerberos token. The user’s authenticated PIV login activates the group membership. 

* The Windows Server® 2008 R2 Patch corrects the known Key Distribution Center (KDC) error: 

    http://support.microsoft.com/kb/2771254 
