---
layout: default
title: Domain Controllers
collection: networkconfig
permalink: networkconfig/domaincontrollers/
---

To use smartcards and PIV credentials for network authentication, all Domain Controllers need to have Domain Controller authentication certificates.

{% include alert-info.html heading = "Devices authenticate too!" content="When your users are using certificates to authenticate to the network, the Domain Controllers are also authenticating as devices using certificates. Each works together to create secure connections. To learn more, search for online resources that discuss Public Key Cryptography for Initial Authentication (PKINIT) protocols." %}

This page contains information on domain controller certificate profiles, and issuing domain controller certificates.

- [Domain Controller certificate profiles](#domain-controller-certificate-profiles)
- [Issue Domain Controller certificates](#issue-domain-controller-certificates)

## Domain controller certificate profiles

Domain Controller certificates must be issued with a set of specific extensions and values.  The certificate profile for each Domain Controller must meet the following requirements:

- The certificate **Key Usage** extension must contain:

            Digital Signature, Key Encipherment

- The certificate **Enhanced Key Usage** extension must contain:

            Client Authentication (1.3.6.1.5.5.7.3.2)
            Server Authentication (1.3.6.1.5.5.7.3.1)

- The certificate **Subject Alternative Name** extension must contain the Domain Name System (DNS) qualifier and fully qualified Domain controller name.  For example:

            DNS Name=controller1.intranet.agency.gov

- The certificate **Subject Alternative Name** must also contain the Domain Controller's Global Unique Identifier (GUID) (i.e., for the "Domain Controller object"). 

  * To determine the Domain Controller's GUID, start **Ldp.exe** and locate the **domain-naming context**. 
  * Double-click on the **name of the Domain Controller** whose GUID you want to view.
  
    > The list of attributes for the Domain Controller object contains **"Object GUID" followed by a long number**. The number is the object GUID. For example:

            Other Name: 1.3.6.1.4.1.311.25.1 = ac 4b 29 06 bb d6 5d 4f e3 9c 4c ab c3 6a 55 d9

    > The Domain Controller's certificate must be installed in the domain controller's local computer's **_personal certificate store_**.

## Issue Domain Controller certificates

US Federal Civilian agencies have a variety of information security policies.  These policies cover whether you should use a Domain Controller certificate issued from your agency's local enterprise Certificate Authority, or whether the certificate must be issued from a Certificate Authority managed and certified under the Federal Public Key Infrastructure (FPKI).  Each agency's information security policy should be followed.

It is not recommended to set up a local enterprise certificate authority just to issue domain controller certificates without ensuring the proper management and security protections are enabled.  Your Chief Information Security Officer (CISO) must have awareness and oversight established for the certificate authority management.

Collaborate with your Chief Information Security Officer (CISO) or Information Security office for a definitive answer and direction.

If you do have a local enterprise Certification Authority, [here are some tips.]({{site.baseurl}}/networkconfig/localca/)

