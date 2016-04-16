---
layout: default
title: Checking Ports and Protocols
collection: networkconfig
permalink: networkconfig/ports/
---

<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Intermediate</em>
</div>
</div>

Your workstations, servers, network domain controllers and applications need to validate the [revocation](../../pivcertchains#revocation) status of the PIV certificates and all intermediate certificate authority certificates.  In addition, the [certificate chain](../../pivcertchains#certificate-chains) path building may retrieve and download the intermediate certificate authority certificates.

The validation occurs in real-time (with some caching) and requires ensuring traffic over the network is open and available to the destination web services, ports, and protocols.

Many US Federal agencies implement a layered network security model with demilitarized zones (DMZs), proxies and Trusted Internet Connections (TICs) to monitor, defend and protect the networks, applications and users.   You may find restricted or denied access to internet web services including the OCSP and CRL web services used in the certificate validations.  Collaborate with your network engineers to review the web services, IP addresses, ports and protocols, and verify access from all local and wide area network segments.

This section covers the common network configurations and considerations including:

1. [Web services for validating PIV certificates](#web-services-for-validating-piv-certificates)
1. [Web services for the Federal Public Key Infrastructure](#web-services-for-the-federal-public-key-infrastructure-root)
1. [Verifying and Troubleshooting](#verifying-and-troubleshooting)
1. [Implementing local OCSP and CRL services inside your network](#implementing-local-ocsp-and-crl-services-inside-your-network)


#### Web services for validating PIV certificates

[Revocation](../../pivcertchains#revocation) status is validated using one of two methods, over the HTTP protocol:

| Type | Certificate Extension | Protocol (Port) | Considerations|
| ----- | -------| -------| ------|
| OCSP | Authority Information Access | HTTP (80) | All PIV certificates have OCSP references and OCSP URLs which are internet accessible and provided by the issuing certificate authority. Intermediate certificate authorities are **not** required to have OCSP available for the _intermediate_ certificates.|
| CRL  | CRL Distribution Point (CDP) | HTTP (80) | All PIV certificates have CRL capabilities provided by the issuing certificate authority.  All intermediate certificate authority certificates have CRL capabilities.  CRL files have an expiration time which varies between 6 hours to 18 hours. CRL file sizes range from a few kilobytes to over 30 megabytes (MB).

Lightweight Directory Application Protocol (LDAP) for retrieving information is not preferred and has been increasingly deprecated; therefore LDAP is not included.

To meet your initial network requirements, you should ensure the OCSP and CRL URLs included in *your agency* users' [PIV Authentication certificates](../details/#viewing-your-piv-credential) are accessible from all workstations and domain controllers.

There are dozens of OCSP and CRL URLs for *all* issued PIV credentials.  If you have users with PIV credentials from other agencies or partners, identifying all the URLs to verify against your network configurations will be more complex.

#### Web services for the Federal Public Key Infrastructure

The Federal Common Policy Certificate Authority (COMMON) is the root certificate authority and has web services to publish both [certificate chains](../../pivcertchains#certificate-chains) (p7b files) and [CRLs](../../pivcertchains#revocation) for all intermediate certificate authorities which the root signs.

To enable communications with these Federal Common Policy Certificate Authority services, including those currently operational and any expansion, it is recommended to allow outbound communications to the Federal Public Key Infrastructure Management Authority address space as registered with the American Registry for Internet Numbers (ARIN) under FPKI-NET:

| IPv4  |  Net Range  | 199.167.92.0 - 199.167.95.255 |
| IPv4  |  CIDR  | 199.167.92.0 / 22 |
| IPv6  |  Net Range  | 2620:9B:C000::- 2620:9B:C00F:FFFF:FFFF:FFFF:FFFF:FFFF |
| IPv6  |  CIDR  | 12620:9B:C000::/44 |

You should consider allowing two protocols (port): HTTP (80) and DNS (53).  Although the web services for publishing CRLs is not currently served over HTTPS (443), you may want to allow HTTPS (443) to future proof for any expansion.


#### Verifying and Troubleshooting
Non-accessible endpoints for the web services due to firewalls blocking access is a very common root cause for errors.  If you encounter user errors including "Cannot validate" and similar domain controller errors, your first troubleshooting step should be to verify your network and access.

Troubleshooting if the web services endpoints are accessible or blocked is simple to begin.  You have the basic four utility tools for troubleshooting:

*  certutil (Microsoft)
*  openssl
*  nslookup
*  tracert


For the typical network domain, _certutil_ will be your best option to identify a number of possible root causes.  There are many options available in the _certutil_ utility tool, and two are covered here.

Export your _public_ key and certificate for PIV Authentication to a .cer file (mypiv_auth.cer), and run the following command in a command line from workstation(s) *and* domain controller(s):

```certutil -verify -urlfetch mypiv_auth.cer >>verify_piv.txt
```

The text file (txt) output will include a *full* check against all options for CRLs, OCSP, intermediate certificates to verify a trust chain, and the root (COMMON).  Review all items and ensure at least one successful verification message is included for _each check_.  You may see errors for the LDAP verifications and these can be ignored if a CRL or OCSP check is successful.

Alternately, there is a graphical user interface.

```certutil -v -url mypiv_auth.cer
```

The graphical user interface allows you to check OCSP, CRL, and AIA (intermediate certificate retrievals).









#### Implementing local OCSP and CRL services inside your network
