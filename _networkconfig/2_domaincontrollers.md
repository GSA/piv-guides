---
layout: default
title: Domain Controllers
collection: networkconfig
permalink: networkconfig/domaincontrollers/
---

To use smartcards and PIV credentials for network authentication, all the Domain Controllers need to have Domain Controller Authentication certificates.

{% include alert-info.html heading = "Devices authenticate too!" content="When your users are using certificates to authenticate to the network, the Domain Controllers are also authenticating as devices using certificates.  Each works together to create secure connections.  To learn more, search other online resources for information on PKINIT protocols." %}

This page contains information on domain controller certificate profiles, and issuing domain controller certificates.

- [Domain Controller Certificate Profiles](#domain-controller-certificate-profiles)
- [Issuing Domain Controller Certificates](#issuing-domain-controller-certificates)

## Domain Controller Certificate Profiles
The domain controller certificates need to be issued with a set of specific extensions and values.  The certificate for each domain controller must meet these requirements:

- The certificate **Key Usage** extension must contain:

            Digital Signature, Key Encipherment

- The certificate **Enhanced Key Usage** extension must contain:

            Client Authentication (1.3.6.1.5.5.7.3.2)
            Server Authentication (1.3.6.1.5.5.7.3.1)

- The certificate **Subject Alternative Name** extension must contain the Domain Name System (DNS) qualifier and name.  This must be the fully qualified domain controller name.  For example:

            DNS Name=controller1.intranet.agency.gov

- The certificate **Subject Alternative Name** must also contain the global unique identifier (GUID) of the domain controller object in the domain.

            To determine the Domain Controller GUID, start Ldp.exe and locate the domain-naming context. Double-click the name of the domain controller that you want to view. The list of attributes for that object contains "Object GUID" followed by a long number. The number is the GUID for that object. For example:

            Other Name: 1.3.6.1.4.1.311.25.1 = ac 4b 29 06 bb d6 5d 4f e3 9c 4c ab c3 6a 55 d9

- The domain controller certificate must be installed in the domain controller's local computer's _personal certificate store_.

## Issuing Domain Controller Certificates
US Federal Civilian agencies have a variety of policies on whether you should use a Domain Controller certificate issued from your agency's local enterprise Certificate Authority, or whether the certificate must be issued from a Certificate Authority managed and certified under the Federal Public Key Infrastructure (FPKI).  Providing a common guide and recommendation is challenging as each agency's information security policy should be followed.

It is not recommended to set up a local enterprise certificate authority just to issue domain controller certificates without ensuring the proper management and security protections are enabled, and your Chief Information Security Officer (CISO) has awareness and oversight for the certificate authority management.

The best option is to collaborate with your Chief Information Security Officer (CISO) or Information Security office for a definitive answer and direction.


# Generating and Installing Domain Controller Certificate

_Accurate as of 3/17/2017 using Microsoft 2012 Server Standard Edition for Certification Authority and Domain Controller servers._

**Use Case:** Would like to use a local Enterprise Microsoft Certification Authority (CA) to issue a Domain Controller (DC) certificate to the DC server. The DC server must have a certificate installed with the appropriate fields/values as a pre-requisite to enabling PIV credential login for domain connected devices.

_\*Pre-requisite: Server hosting the CA must be on the domain_

**Install CA Role**

1. Log on to the CA server as a member of the **Enterprise Administrators** group.
2. Open **Server Manager**
3. Click **Manage** , and then click **Add Roles and Features**.
4. Proceed through the Add Roles and Features Wizard, choosing the following options:
  * Server Roles: _Active Directory Certificate Services_
  * AD CS Roles Services: _Certification Authority_ 
5. On the Results page, click **Configure Active Directory Certificate Services on the destination server**.
6. Proceed through the AD CS Configuration, choosing the following options as necessary:
  * Role Service: _Certification Authority_ 
  * Setup Type: E_nterprise CA_ 
  * CA Type: _Root CA_
  * Private Key: _Create a new private key_ 
  * Cryptography: _RSA#Microsoft Software Key Storage Provider, 2048 bit, SHA-256_ 6e
  * CA Name should use Recommended naming convention:
        dc=[_AD suffix_], dc=[_AD domain_], cn=[_certification authority name_], 
        e.g. dc=_gov_, dc=_[AgencyName]_, cn=_[AgencyName] __NPE__ CA1_ 
  * Validity Period: _6 years_ 
  * Certificate Database: _&lt;your preference&gt;_ 



**Configure CA Template for Domain Controller**

_\* Certificate templates are only available on Enterprise CAs_

7. Log on to the CA server as a member of the **Enterprise Administrators** group
8. Open the certificate templates MMC snap-in (i.e. **certtmpl.msc** )
9. Right-click the **Domain Controller Authentication** template and click **Duplicate Template**
10. Under the **Compatibility Tab** , modify the **Compatibility Settings** for both the CA and certificate recipients to as high as possible (e.g. **Windows Server 2012 R2, Windows 7 / 2008 R2** )
11. Under the **General tab** :
  * Recommend renaming template to: _&lt;Your organization&gt; - Domain Controller Authentication_
  * Recommend modifying validity period to:  _3 years_
  * Recommend modifying Renewal period to: _6 weeks_
12. Under the **Cryptography tab** :
  * Set minimum key size to 2048
  * If possible, set Request hash to SHA256
13. Open the CA console (i.e. **certsrv.msc** )
14. In the console tree, click the name of the CA
15. In the details pane, double-click **Certificate Templates**
16. In the console tree, right-click **Certificate Templates** , click **New** , and then click **Certificate Template To Issue**
17. Select and enable the certificate template that were created in step 9 above, and then click **OK**

**Auto-enroll Domain Controller Certificate Using Group Policy Object (GPO)**

18. Log on to the Domain Controller server as a member of the **Enterprise Administrators** group
19. Open the GPMC (i.e. **gpmc.msc** )
20. Within the appropriate GPO, navigate to _Computer Configuration\Policies\Windows Settings\Security Settings\Public Key Policies\_
21. Configure **Certificate Services Client – Auto-Enrollment** with the following options:
  * Configuration Model: _Enabled_
  * Renew Expired Certificates, Update Pending Certificates, Remove Revoked Certificates: _Check_
  * Update Certificates That Use Certificate Templates: _Check_
22. You can now force the group policy to update via command-line: _gpupdate /force_ or wait for the group policy to update on its own
23. If successful, you should see a new DC cert in the Certificate (Local Computer) -&gt; Personal -&gt; Certificates folder. _(_e. _open MMC.exe -&gt; File -&gt; Add/Remove Snap-in -&gt;Certificates -&gt;Computer account -&gt;Local computer)._ If you look at the furthest tab called &quot;Certificate Template&quot; you should see a cert generated with the custom template you created in step 9.
