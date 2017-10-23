---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

You may need to grant elevated privileges to your agency users when they log in with their PIV/CAC credential. To help you do this, you can use a Windows Active Directory (AD) feature called _Authentication Mechanism Assurance (AMA)_. AMA allows you to add a global group membership to a user’s Kerberos token, based on the PIV/CAC’s certificate policy.

{% include info-alert.html content=" AMA does not offer an option to require a specific login method (e.g., PIV/CAC login)." %}

Let's take a look at how that works. You have one user (Joe) who needs read access to SharePoint documents. His certificate policy Object Identifier (OID) is _2.16.840.1.101.3.2.1.3.13_ and its name is _id-fpki-common-authentication_. Another user (Julie) needs write access to SharePoint documents. Her certificate policy OID is _2.16.840.1.101.3.2.1.3.16_ and its name is _id-fpki-common-high_. To grant Joe and Julie the needed privileges, you will need to set up their 2 policies in AD DS. Then, you'll need to assign their global group memberships, based on their policy OIDs. 

Select the method below based on your Windows Server version (2012, 2008 R2).

{% include info-warning.html content=" Do not use AMA to provide privileged access to servers." %}

## Windows Server® 2012 AD DS and Later

* Use the Windows Registry Editor to set the _AMA Priority_ above _Most Recently Issued Superior Certificate Heuristic_:

            [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
            "ChainWithIssuancePolicyOIDs"=dword:00000001

* This PowerShell script for the Federal Common and DoD Certificate Policies simplifies Microsoft TechNet's steps for Windows Server 2012:&nbsp;&nbsp;[AMA Certificate Issuance OIDs](https://github.com/GSA/ficam-scripts-public/tree/auth-mech-assurance/_ama){:target="_blank"}.

## Windows Server® 2008 R2 AD DS

* Go to:&nbsp;&nbsp;[Windows Server 2008 R2 AD DS Step-by-Step Guide](https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx)[:target=_"blank"}.
* Set the _Domain Functional Level_ to _Windows Server 2008 R2_.
* Add a global group membership to the user’s Kerberos token. When a user's PIV/CAC login is authenticated, it will activate the group membership.

### Hotfix for Windows® 2008 R2 Key Distribution Center (KDC) Error

* A Windows Server® 2008 R2-based Domain Hotfix corrects the known KDC error, "Access tokens are not updated correctly when you enable authentication mechanism assurance in a Windows Server 2008 R2-based domain." [Microsoft Hotfix](http://support.microsoft.com/kb/2771254){:target="_blank"}.

