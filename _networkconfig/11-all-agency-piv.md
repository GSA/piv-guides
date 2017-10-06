---
layout: default
title: Configure Network Authentication to Accept Other Agency PIV/CAC cards
collection: userconfig
permalink: networkconfig/11_accept-all-agency-piv.md/
---

If you want to allow other agency users to authenticate to your agency network, this article will help you configure your agency's Active Directory to support other agency issued PIV/CAC card authentication.

## Network Ports and Protocols - Open Access to OCSP and CRL

The first step in setting up the support for other agency PIV/CAC is to validate that your agencies network is open to the Certificate Issuer website to validate the certificate. Your agency's domain controllers, servers and workstations should be able to access the OCSP and CRL links for validation in real time.

## Domain Controllers - Add Agency UPN Suffix

In order to trust the PIV/CAC cards from another agency, you have to [add the UPN suffix](https://technet.microsoft.com/en-us/library/cc772007(v=ws.11).aspx){target="_blank"}_ of that agency in your agencies Active Directory Domains and Trusts.

To add UPN suffixes

1. Open Active Directory Domains and Trusts. To open Active Directory Domains and Trusts, click Start , click Administrative Tools, and then click Active Directory Domains and Trusts .
2. In the console tree, right-click Active Directory Domains and Trusts, and then click Properties.
3. On the UPN Suffixes tab, type an alternative UPN suffix for the forest, and then click Add.

## Trust Store - Import Agency Specific PIV Issuer Certificates

The agency specific PIV Issuer certificates can be found on the [FPKI Crawler](https://fpki-graph.fpki-lab.gov/crawler/){target="_blank"}_ website. You will find the certificate listed by agencies in the table 'Certificate Files Grouped by Type'. Once you locate the agency, you can download the certificates and the path to COMMON in p7b format.
{target="_blank"}_.

Import the certificates in the Windows [NTAuth Trust Store](https://piv.idmanagement.gov/networkconfig/trustedroots/){target="_blank"}_.

## Account Linking - Other Agency Users

When a user authenticates with another agency PIV/CAC card, the credential of that user may not match the account created in the Active Directory user setup in your agency. There are multiple ways to match that PIV/CAC card owner to the Active Directory account.

## List of PIV Issuers

| Name | PIV Issuer  | Links |
|------|-------------|-------|
|USAccess|OU = Entrust Managed Services SSP CA <br>OU = Certification Authorities<br> O = Entrust<br> C = US | AIA: http://sspweb.managed.entrust.com/AIA/CertsIssuedToEMSSSPCA.p7c<br> OCSP:<br>  CRL: http://sspweb.managed.entrust.com/CRLs/EMSSSPCA2.crl |
|Entrust Federal SSP|Entrust Federal SSP||
|Department of Defense|||
|Department of Homeland Security|||
|Department of State|||
|FAA Custom|||
|NASA|||
