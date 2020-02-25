---
layout: default
title: Trust Stores
collection: networkconfig
permalink: networkconfig/trustedroots/
---

You want your Active Directory domain, including servers and workstations, to trust user's PIV credentials for authentication.  Trust and certificate chains are reviewed in the [Certificate Trust](../../pivcertchains) overview, and this page includes information on configuring your Active Directory domain.

There are two trust stores to consider for your Active Directory domain:

- [Trusted Root Certification Authorities Trust Store](#trusted-root-certification-authorities-trust-store)
- [Enterprise NTAuth Trust Store](#enterprise-ntauth-trust-store)

##  Trusted Root Certification Authorities Trust Store
You need to publish the Federal Common Policy Certification Authority (COMMON) [root certificate]({{site.baseurl}}/pivcertchains/#download-root-and-intermediate-certificates) to the Trusted Root Certification Authorities trust stores on all your workstations, devices, servers, and domain controllers.   

It is recommended to add the COMMON [root certificate]({{site.baseurl}}/pivcertchains/#download-root-and-intermediate-certificates) to a Group Policy Object (GPO) to publish it as a _trusted root_ for all domain users and computers.  It is also possible to install it via command line, however, keep in mind that the way a certificate is added to a store (Trusted Root, NTAuth, etc.), is the way the certificate has to be removed from the store in the future.  For example, an administrator cannot add certificates locally to a system via command line, and then remove the certificate later using a GPO.

Additionally, the Root CA for the domain controller certificates must also be in the Trusted Root Certification Authorities trust store on all your workstations, devices, servers, and domain controllers for which the domain controller will be authorizing smart card logon.

## Enterprise NTAuth Trust Store
The Enterprise NTAuth trust store is used by your Active Directory domain to determine which certification authorities to trust for issuing certificates that are authorized for smart card logon.  The certificate for the Issuing CA of both the smart card certificate and the Domain Controller certificate must be published to the Enterprise NTAuth store.  If your agency will accept PIV credentials issued by another agency or partner, you will need to include all possible Issuing CAs into the Enterprise NTAuth store.

Use certutil to publish a certificate to the NTAuth store.  This will require Enterprise Admin permissions for the domain. 

To publish / add a certificate to NTAuth:


```
  certutil –dspublish –f IssuingCaFileName.cer NTAuthCA
```

To view all certificates in NTAuth:  

```
  certutil –viewstore –enterprise NTAuth
```

To remove certificates in NTAuth:  

```
  certutil –viewdelstore –enterprise NTAuth
```

Depending on your Active Directory topology, it could take several hours to propagate any changes throughout the agency. To propagate from the domain controller(s) to the enterprise, a group policy update can be forced to an OU via Group Policy Management Console.  If troubleshooting a single computer, running either of the following commands, from an elevated command prompt, on the problem computer should work: 

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

