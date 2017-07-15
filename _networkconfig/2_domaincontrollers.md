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
