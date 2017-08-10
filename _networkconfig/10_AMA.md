---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

# Authentication Mechanism Assurance (AMA)

A high-level login risk, like logging into a government system from your favorite coffee shop, home, or the internet, means your system needs more stringent authentication mechanisms than for a low-risk logins (e.g., logging in at the office).

You can increase the protections for high-risk logins to sensitive federal resources by using Microsoft’s Windows Active Directory (AD) Domain Service’s (DS) _Authentication Mechanism Assurance (AMA)_. AMA adds a group membership to a user’s security identifier attributes (SIDs). 

Microsoft offers AMA with several Windows Server versions. Use these guidelines to configure your Windows Server. 

## Specific Implementations

### Windows Server 2012® AD DS and Later
* No patch is required.  Enable _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_ by using the Windows Registry Editor:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001

* The Power Shell Script below for the Federal Common and DoD Certificate Policies simplifies the Microsoft TechNet steps for the Windows Server 2012: 

    https://github.com/GSA/piv-guides/files/621976/CertificateIssuanceOIDs.ps1.txt

### Windows Server® 2008 R2 AD DS
* Set the _Domain Functional Level_ to _Windows Server 2008 R2_:

    https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx

* AMA gives you the option to add a global group membership to a user’s Kerberos token. The user’s authenticated PIV login activates the group membership.

* The Windows Server® 2008 R2 Patch corrects the Key Distribution Center (KDC) error: 

    http://support.microsoft.com/kb/2771254 
