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

You need to be able to validate your PIV credential.  The primary question answered during validation is: _Are you and your credential (PIV certificate) still trusted?_

Why would a PIV credential not be _trusted_ anymore?  

Your workstations, servers and browsers may also need to retrieve and validate the certificate chains we talked about [here](#before-you-get-started).  

This validation depends on ensuring the network traffic is open for the ports and protocols.  

> Validation is performed using a variety of algorithms on different operating systems and with different cryptographic libraries. This section focuses on the _basics_ for common agency network configurations.  In addition, the LDAP protocol for retrieving revocation information is not preferred and is being increasingly deprecated; therefore LDAP is not included in this guide.

#### Checking the Network for Ports and Protocols

Validation occurs using one of two mechanisms, over the HTTP protocol:

*  On-line Certificate Status Protocol (OCSP): HTTP / Port 80
*  Certificate Revocation Lists (CRLs): HTTP / Port 80


#### Simple Checks for Ports and Protocols

 
