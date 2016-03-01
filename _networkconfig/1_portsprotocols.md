---
layout: page_collection
title: Checking Ports and Protocols
collection: networkconfig
permalink: networkconfig/ports/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Difficulty: Moderate</em>
</div>
</div>


#### Outline of Steps
1. [Checking the network for Ports and Protocols](#checking-the-network-for-ports-and-protocols)
2. Configuration considerations for Domain Controller certificates
2. [Addition of US Federal Certificate chains to the Trusted Root Certificate Authorities](#addition-of-us-federal-certificate-chains-to-the-trusted-root-certificate-authorities)
3. Publishing the US Federal Certificate chains to the NT Auth Store
4. [Associating PIV Credentials to the Active Directory User Accounts using altSecurityIdentities](#associating-piv-credentials-to-the-active-directory-user-accounts-using-altSecurityIdentities)
5. Configuring group policies for PIV (smartcard) logon

#### Checking the network for Ports and Protocols

The primary question answered during validation is: _Are you and the chain still trusted?_  You need to be able to validate the certificates during use.  Your workstations, servers and browsers may also need to retrieve the certificate chains we talked about [here](#before-you-get-started).

> Validation is performed using a variety of algorithms on different operating systems and with different cryptographic libraries. This section focuses on the _basics_ for common agency network configurations.  In addition, the LDAP protocol for retrieving revocation information is not preferred and is being increasingly deprecated; therefore LDAP is not included in this guide. 
{:class="alert"}

Validation occurs using one of two mechanisms, over the HTTP protocol:

*  On-line Certificate Status Protocol (OCSP): HTTP / Port 80
*  Certificate Revocation Lists (CRLs): HTTP / Port 80 

 
