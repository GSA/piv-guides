---
layout: default
title: Trust Stores
collection: networkconfig
permalink: networkconfig/trustedroots/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Moderate</em>
</div>
</div>

You want your network domain to trust your users and their PIV credentials.  Your workstations and server also need to be able to trust the network domain.  Trust and certificate chains are reviewed in the [Certificate Trust](../pivcertchains) overview and this page includes information on configuring your network domain.

There are two Trust stores to consider for your network domain:

1.  [Trusted Root Certificate Authorities](#trusted-root-certificate-authorities)
2.  [NTAuth Enterprise Trust Store](#ntauth-enterprise-trust-store)

####  Trusted Root Certificate Authorities
You need to publish the Federal Common Policy Certificate Authority (COMMON) [root certificate](../pivcertchains/#download-root-and-intermediate-certificates) to the trusted root certificate authority trust stores on all your workstations, devices, servers and domain controllers.  

For Microsoft and Apple, the COMMON certificate is included as a trusted root certificate authority by default.  However, you may have your network and devices configured to not automatically update trusted root certificates published by any commercial trust stores.  

You want to add the COMMON [root certificate](../pivcertchains/#download-root-and-intermediate-certificates) to a group policy object or automated configuration management tools to publish COMMON as a _trusted root_ for all your devices used to access the network, servers joined to the network, and all domain controllers.

#### NTAuth Enterprise Trust Store
The _NTAuth_ enterprise trust store is used by your network domain to determine which certificate authorities to trust specifically for authenticating users to the network.  To understand the difference between the typical Trust Stores and NTAuth, you may want to think of NTAuth as an _explicit trust list_ of certificate authorities used for network authentication.

There are two very different options for what certificate authority certificates you need publish to the NTAuth trust store.  Each option depends on the choice you make for [linking your user accounts](../accounts/).

| Trust Store | Account Linking Approach | Certificates to Publish | Considerations|
| ----- | -------| -------| ------|
| NTAuth | Principal Name | COMMON and ALL Intermediate Certificate Authority certificates | If your agency needs the ability to accept any PIV credentials for network authentication and has users with PIV credentials issued by another agency or partner, you will need to include all possible Intermediate Certificate Authority certificates. |
| NTAuth  | altSecurityIdentities _using_ Issuer+Subject as identifier | COMMON | _*Please note: this line is in draft and needs to be tested for bridged intermediate certificate authorities._ |
| NTAuth  | altSecurityIdentities _not using_ Issuer+Subject as identifier | COMMON and ALL Intermediate Certificate Authority certificates | If your agency needs the ability to accept any PIV credentials for network authentication and has users with PIV credentials issued by another agency or partner, you will need to include all possible Intermediate Certificate Authority certificates. |



To publish a certificate to NTAuth, you can use either a group policy object (recommended) or the certutil tool.  If using certutil, you will need to have Enterprise Admin permissions for the domain.

```
certutil –dspublish –f certificate_to_publish.cer NTAuthCA
```
