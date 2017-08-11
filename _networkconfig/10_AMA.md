---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---
# Authentication Mechanism Assurance (AMA)

A high-risk login to a government system, like from a favorite coffee shop or home, requires stringent authentication mechanisms.

You can increase the security of high-risk logins by using Microsoft Windows' Active Directory (AD) Domain Service's (DS) _Authentication Mechanism Assurance (AMA)_, which adds a group membership to the user’s security identifier attributes (SIDs). 

These guidelines are to help you configure AMA on your Windows Server. 

## Windows Server 2012® AD DS and Later

* No patch is required. Enable _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_ by using the Windows Registry Editor:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001

* This Power Shell Script for the Federal Common and DoD Certificate Policies simplifies the Microsoft TechNet steps for Windows Server 2012: 

    https://github.com/GSA/piv-guides/files/621976/CertificateIssuanceOIDs.ps1.txt

## Windows Server® 2008 R2 AD DS

* Set the _Domain Functional Level_ to _Windows Server 2008 R2_:

    https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx

* AMA gives you the option to add a group membership to the user’s Kerberos token. The user’s authenticated PIV login activates the group membership. 

* The Windows Server® 2008 R2 Patch corrects the known Key Distribution Center (KDC) error: 

    http://support.microsoft.com/kb/2771254 
