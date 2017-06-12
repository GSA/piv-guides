---
layout: default
title: Creating Domain Controller Certificate Profiles
collection: networkconfig
permalink: networkconfig/2a_newdc-3.md/
---

* [Creating Domain Controller Certificate Profiles](#creating-domain-controller-certificate-profiles)
* [Issuing Domain Controller Certificates](#issuing-domain-controller-certificates)

To use smartcards and PIV <!--PIV/CAC?-->credentials for network authentication, all Domain Controllers must have Domain Controller authentication certificates. To generate and install a Domain Controller authentication certificate, you will need to create a certificate profile.

{% include alert-info.html heading = "Devices authenticate too!" content="When your users are using certificates to authenticate to the network, the Domain Controllers are also authenticating as devices that use certificates. This system works together to create secure connections. To learn more, click on the links <!--Only one link below.-->below or search for online resources that discuss Public Key Cryptography for Initial Authentication (PKINIT) protocols." %}

## Creating Domain Controller Certificate Profiles <!--Are profiles are being created here? The word, "created" is never used.-->

Domain Controller certificates must be issued with a set of specific extensions and values.  The certificate profile for each Domain Controller must meet the following requirements:

- The certificate **Key Usage** extension must contain:

            Digital Signature, Key Encipherment

- The certificate **Enhanced Key Usage** extension must contain:

            Client Authentication (1.3.6.1.5.5.7.3.2)
            Server Authentication (1.3.6.1.5.5.7.3.1)

- The certificate **Subject Alternative Name** extension must contain the Domain Name System (DNS) qualifier and fully qualified Domain Controller name. For example:

            DNS Name=controller1.intranet.agency.gov

- The certificate **Subject Alternative Name** must also contain the Domain Controller's Global Unique Identifier (GUID) (i.e., for the "Domain Controller object"). 

  * To determine the Domain Controller's GUID, start **Ldp.exe** and locate the **domain-naming context**. 
  * Double-click on the **name of the Domain Controller** whose GUID you want to view.
  
    > The list of attributes for the Domain Controller object contains the **"Object GUID" followed by a long number**. The number is the object GUID. For example:

            Other Name: 1.3.6.1.4.1.311.25.1 = ac 4b 29 06 bb d6 5d 4f e3 9c 4c ab c3 6a 55 d9

    > The Domain Controller's certificate must be installed in the Domain Controller's local computer's **_personal certificate store_**, as described in _Auto-Enroll Domain Controllers Using Group Policy Object_ section under [_Installing a Local Certification Authority_]({{site.baseurl}}/local-certification-authority). <!--Is this the correct section to link to? Proper linking method?-->

## Issuing Domain Controller Certificates <!--Jordan directed that this section should be added back in here.-->

US Federal Civilian agencies have a variety of policies concerning whether you should use a Domain Controller certificate issued from your agency's local enterprise Certificate Authority or whether the certificate must be issued from a Certificate Authority managed and certified under the Federal Public Key Infrastructure (FPKI). Providing a common guide and recommendation is challenging, as each agency's information security policy should be followed.

It is not recommended that you set up a local-enterprise Certification Authority just to issue Domain Controller certificates without ensuring that proper management and security protections are in place. Your Chief Information Security Officer (CISO) has awareness and oversight for Certification Authority management.

The best option is to collaborate with your CISO or Information Security office for a definitive answer and direction.

