---
layout: default
title: Authentication Mechanism Assurance
collection: networkconfig
permalink: networkconfig/AMA/
---

### Authentication Mechanism Assurance

For the purpose of protecting resources based on login method, authentication mechanism assurance from Active Directory (AD) 
domain service adds an additional group membership to the user's security identifiers attribute (SIDs) 
when a user logs on using a certificate-based login method, such as a smart-card login. For example, you can restrict access 
to sensitive resources to users whom log on by using their smart cards, which requires a physical reader that you place 
in a physically secured location.

* Authentication mechanism assurance is an added capability in Windows Server 2008 R2 AD DS that you can use 
when the domain functional level is set to Windows Server 2008 R2. When it is enabled, authentication mechanism assurance adds 
an administrator-designated global group membership to a user’s Kerberos token when the user’s credentials are authenticated 
during logon using a certificate-based logon method

* Authentication Mechanism Assurance (AMA)  for AD DS in Windows Server 2008 R2 

    https://technet.microsoft.com/en-us/library/dd378897(v=WS.10).aspx


* Power Shell Script for Common Federal/DoD Certificate Policies simplifies implementation as compared to TechNet Step-by-Step Guide.

* The Windows Server® 2008 R2 patch to correct the KDC not setting the certificate issuance policy when the KDC validates 
the smartcard certificate is now available via the following link. 

    http://support.microsoft.com/kb/2771254 

* Windows Server® 2012 and after -- no patch required • Enable AMA Priority above  Most Recently Issued Superior Certificate Heuristic
with the following 

      ```
      
1.  Windows Registry Editor Version 5.00 
2.  [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\kdc]
3.  "ChainWithIssuancePolicyOIDs"=dword:00000001
      ```
