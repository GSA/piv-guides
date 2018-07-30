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
You need to publish the Federal Common Policy Certification Authority (COMMON) [root certificate]({{site.baseurl}}/pivcertchains/#download-root-and-intermediate-certificates) to the trusted root certification authority trust stores on all your workstations, devices, servers and domain controllers.   

You want to add the COMMON [root certificate]({{site.baseurl}}/pivcertchains/#download-root-and-intermediate-certificates) to a Group Policy Object to publish it as a _trusted root_ for ALL the devices and user objects.

## NTAuth Enterprise Trust Store
The _NTAuth_ enterprise trust store is used by your network domain to determine which certification authorities to trust specifically for authenticating users to the network.  To understand the difference between the typical network domain Trust Stores and NTAuth, you may want to think of NTAuth as an _explicit trust list_ of certification authorities used for network authentication.

There are two very different options for what certification authority certificates you need publish to the NTAuth trust store.  Each option depends on the choice you make for [linking your user accounts](../accounts/).

| Trust Store | Account Linking Approach | Certificates to Publish | Considerations|
| ----- | -------| -------| ------|
| NTAuth | Principal Name | COMMON and ALL Intermediate Certification Authority certificates | If your agency needs the ability to accept any PIV credentials for network authentication and has users with PIV credentials issued by another agency or partner, you will need to include all possible Intermediate Certification Authority certificates. |
| NTAuth  | altSecurityIdentities _using_ Issuer+Subject as identifier | COMMON | _*Please note: this line is in draft and needs to be tested for bridged intermediate certification authorities._ |
| NTAuth  | altSecurityIdentities _not using_ Issuer+Subject as identifier | COMMON and ALL Intermediate Certification Authority certificates | If your agency needs the ability to accept any PIV credentials for network authentication and has users with PIV credentials issued by another agency or partner, you will need to include all possible Intermediate Certification Authority certificates. |


To publish a certificate to NTAuth, you can use either a group policy object (recommended) OR the certutil tool.  

Using **certutil**, you will need to have Enterprise Admin permissions for the domain.  

To publish / add a certificate to NTAuth:


```
  certutil –dspublish –f certificate_to_publish.cer NTAuthCA
```

To view all certificates in NTAuth:  

```
  certutil –viewstore –enterprise NTAuth
```

To propagate from the domain controller(s) to the enterprise, you'll want to do a _gpupdate_:  

```
  gpupdate /force
```
