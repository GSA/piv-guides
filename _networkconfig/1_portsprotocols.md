---
layout: page_collection
title: Checking Ports and Protocols
collection: networkconfig
permalink: networkconfig/ports/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Intermediate</em>
</div>
</div>

This section covers the common network configurations and considerations for implementation including:

1. [Ports and Protocols](#ports-and-protocols)
1. [Common web services in the Federal Public Key Infrastructure](#common-web-services-in-the-federal-public-key-infrastructure)
1. [Verifying and Troubleshooting](#verifying-and-troubleshooting)
1. [Implementing local OCSP and CRL services inside your network](#implementing-local-ocsp-and-crl-services-inside-your-network)    


Your workstations, servers, network domain controllers and applications need to validate the [revocation](../../pivcertchains#revocation) status of the PIV certificates and all intermediate certificate authority certificates.  In addition, the [certificate chain](../../pivcertchains#certificate-chains) path building may retrieve and download the intermediate certificate authority certificates.  

This validation occurs in real-time (with some limited caching) and requires ensuring traffic over the network is open and available to the destination web services, ports, and protocols.   

Many US Federal agencies may implement a layered network security model with firewalls, demilitarized zones (DMZs), proxies and Trusted Internet Connections (TICs) to monitor, defend and protect the networks, applications and users.   Therefore, you may find restricted or denied access to internet web services including the OCSP and CRL web services used in the certificate validations.  It is recommended to collaborate with your network engineers to review the web services, internet protocol (IP) addresses, ports and protocols and verify access from all local and wide area network segments.   

#### Ports and Protocols

[Revocation](../../pivcertchains#revocation) status is checked using one of two methods, over the HTTP protocol:

| Type | Certificate Extension | Protocol (Port) | Considerations|
| ----- | -------| -------| ------|
| OCSP | Authority Information Access | HTTP (80) | All PIV certificates have OCSP references and OCSP URLs which are internet accessible and provided by the issuing certificate authority. Intermediate certificate authorities are **not** required to have OCSP available for the _intermediate_ certificates.|
| CRL  | CRL Distribution Point (CDP) | HTTP (80) | All PIV certificates have CRL capabilities provided by the issuing certificate authority.  All intermediate certificate authority certificates have CRL capabilities.  CRL files have an expiration time which varies between 6 hours to 18 hours. CRL file sizes range from a few kilobytes to over 30 megabytes (MB).

The LDAP protocol for retrieving revocation information is not preferred and is being increasingly deprecated; therefore LDAP is not included in this guide.


#### Common web services in the Federal Public Key Infrastructure

The Federal Common Policy Certificate Authority (COMMON) is the root of The

To enable communications with the <what?> network of webservices available, including those currently operational and any expansion, it is recommended to allow outbound communications to the Federal Public Key Infrastructure Management Authority address space as registered with the American Registry for Internet Numbers (ARIN) under FPKI-NET:

| IPv4  |  Net Range  | 199.167.92.0 - 199.167.95.255 |
| IPv4  |  CIDR  | 199.167.92.0 / 22 |
| IPv6  |  Net Range  | 2620:9B:C000::- 2620:9B:C00F:FFFF:FFFF:FFFF:FFFF:FFFF |
| IPv6  |  CIDR  | 12620:9B:C000::/44 |



#### Verifying and Troubleshooting

*  nslookup
*  tracert
*  certutil
*  openssl




```certutil -verify -urlfetch mypiv_auth.cer >>verify_piv.text
```


```certutil -verify -url mypiv_auth.cer >>verify_piv.text
```




#### Implementing local OCSP and CRL services inside your network
