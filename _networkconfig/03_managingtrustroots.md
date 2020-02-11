---
layout: default
title: Trust Stores
collection: networkconfig
permalink: networkconfig/trustedroots/
---

You want your network domain to trust your users and their PIV credentials.  Your workstations and servers also need to be able to trust the network domain.  Trust and certificate chains are reviewed in the [Certificate Trust](../../pivcertchains) overview and this page includes information on configuring your network domain.

There are two trust stores to consider for your network domain:

- [Trusted Root Certification Authorities](#trusted-root-certification-authorities)
- [NTAuth Enterprise Trust Store](#ntauth-enterprise-trust-store)

##  Trusted Root Certification Authorities
You need to publish the Federal Common Policy Certification Authority (COMMON) [root certificate]({{site.baseurl}}/pivcertchains/#download-root-and-intermediate-certificates) to the Trusted Root Certification Authorities trust stores on all your workstations, devices, servers, and domain controllers.   

You want to add the COMMON [root certificate]({{site.baseurl}}/pivcertchains/#download-root-and-intermediate-certificates) to a Group Policy Object to publish it as a _trusted root_ for ALL the devices and user objects.

Additionally, the Root CA for the domain controller certificates must also be in the Trusted Root Certification Authorities trust store on all your workstations, devices, servers, and domain controllers for which the domain controller will be authorizing smart card logon.

## NTAuth Enterprise Trust Store
The _NTAuth_ enterprise trust store is used by your Active Directory domain to determine which certification authorities to trust specifically for authenticating users to the network.  The certificate for the Issuing CA of both the Smart Card certificate and the Domain Controller certificate must be published to the NTAuth store.  If your agency will accept PIV credentials issued by another agency or partner, you will need to include all possible Issuing CAs into the NTAuth store.

Use certutil to publish a certificate to the NTAuth store.  This will require Enterprise Admin permissions for the domain. 

To publish / add a certificate to NTAuth:


```
  certutil –dspublish –f certificate_to_publish.cer NTAuthCA
```

To view all certificates in NTAuth:  

```
  certutil –viewstore –enterprise NTAuth
```

To remove certificates in NTAuth:  

```
  certutil –viewdelstore –enterprise NTAuth
```

Depending on your Active Directory topology, it could take several hours to propagate any changes throughout the agency. To propagate from the domain controller(s) to the enterprise, a group policy update can be forced to an OU via Group Policy Management Console.  If troubleshooing a single computer, either of the commands run as administrator should work: 

```
  gpupdate /force
```

or

```
  certutil -pulse
```

However, the registry containing this information may not be updated if your agency has the Certificate Services Client - Auto-Enrollment disabled.

In this case, an administrator can add it locally with the command:

```
  certutil -enterprise -addstore NTAuth IssuingCaFileName.cer
```

However, keep in mind that the way a certificate is added to a store (Trusted Root, NTAuth, etc.), is the way the certificate has to be removed from the store in the future.  For example, an administrator cannot add certificates via GPO, and then remove them via the command line.
