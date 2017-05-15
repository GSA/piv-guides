---
layout: default
title: Domain Controllers
collection: networkconfig
permalink: networkconfig/domaincontrollers/
---
# How do I generate and install Certification Authority (CA) certificates for Domain Controllers?

To use smartcards and PIV credentials for network authentication, all Domain Controllers need to have Domain Controller authentication certificates.

{% include alert-info.html heading = "Devices authenticate too!" content="When your users are using certificates to authenticate to the network, the Domain Controllers are also authenticating as devices that use certificates. This system works together to create secure connections. To learn more, click on the links below or search for online resources that discuss Public Key Cryptography for Initial Authentication (PKINIT) protocols." %}

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

    > The Domain Controller's certificate must be installed in the domain controller's local computer's **_personal certificate store_**, as described below in the _Generate and install Domain Controller certificate_ procedures.

## Issue Domain Controller certificates

Each U.S. Federal Government's Civilian agency has information-security policies that guide its decision-making about whether its Domain Controller's <!-- More than one DC? More than one certificate possible? -->certificate should be issued by the agency's local enterprise Certificate Authority (CA) or whether a Federal Public Key Infrastructure (FPKI)-managed and certified CA should issue it. Providing a common guide and recommendation is challenging, as each agency should follow its own policies; however, we do not recommend that agencies set up a local enterprise CA just to issue Domain Controller certificates. The best option is to collaborate with your agency's Chief Information Security Officer (CISO) (or the Information Security Office), who can give you definitive direction and has oversight for managing CAs and ensuring that security protections are in place.
