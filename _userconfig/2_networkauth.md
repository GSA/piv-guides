---
layout: default
title: Configure Network Authentication to Accept Other Agency PIV/CAC cards
collection: userconfig
permalink: userconfig/2_networkauth.md/
---

If you want to allow other agency users to authenticate to your agency network, this article will help you configure your agency's Active Directory to support other agency issued PIV/CAC card authentication.

# Import Agency Specific PIV Issuer Certificates

The agency specific PIV Issuer certificates can be found on the [FPKI Crawler](https://fpki-graph.fpki-lab.gov/crawler/){target="_blank"}_ website. You will find the certificate listed by agencies in the table 'Certificate Files Grouped by Type'. Once you locate the agency, you can download the certificates and the path to COMMON in p7b format.
{target="_blank"}_.

Import the certificates in the Windows [NTAuth Trust Store](https://piv.idmanagement.gov/networkconfig/trustedroots/){target="_blank"}_.

# Add Agency Suffix to Domain Controllers



# Account Linking of Other Agency Users
