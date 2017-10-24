---
layout: default
title: Configure Network Authentication To Accept Other Agency PIV/CAC Cards
collection: networkconfig
permalink: networkconfig/11_accept-all-agency-piv.md/
---

##### Last Updated: October 23, 2017

Your agency provides network accounts to government users on detail, as well as those who cross-collaborate on special programs. They need to authenticate to your network with their home-agency PIV/CAC credentials, rather than issuing them new credentials. 

This guide will help you configure Active Directory (AD) on your domains to allow government users with a PIV/CAC credential to authenticate. 

* [Open Access to OCSP and CRL](#open-access-to-ocsp-and-crl)
* [Add Agency UPN Suffix in AD](#add-agency-upn-suffix)
* [Import Agency-Specific PIV Issuer Certificates](#import-agency-specific-piv-issuer-certificates)
* [Link Account of the Other Agency Users](#account-linking-other-agency-users)
* [List of PIV Issuers](#list-of-piv-issuers)

## Open Access to OCSP and CRL

To configure your network to authenticate users via their home-agency PIV/CAC credentials, you need to verify that your network allows access to their home agency's Certificate Issuer website to validate the certificate. Your agency's domain controllers, servers and workstations need to access the On-line Certificate Status Protocol (OCSP) and Certificate Revocation List (CRL) links for validation in real-time. OCSP and CRL endpoints are used to define configurations for the firewalls. You must allow access to these endpoints through the firewalls so this will work.

You can find the OCSP and CRL links in the List of Issuers table below.

You can also use the CRL endpoints to poll the CRL data into your local internal agency OCSP responders (for those that have them installed!) and route your internal agency intranet traffic to your internal agency ocsp responders. How would you do this?  We will tell you - this can be configured in your microsoft domain as a setting.

## Add Agency UPN Suffix in AD

In order to trust PIV/CAC credentials from another agency, you'll have to add that agency's [UPN suffix](https://technet.microsoft.com/en-us/library/cc772007(v=ws.11).aspx){target="_blank"}_ to your agency's AD Domains and Trusts.

1. Click through _Start_ &gt; _Administrative Tools_ &gt; _Active Directory Domains and Trusts_.
2. In the console tree, right-click _AD Domains and Trusts_ and then click _Properties_.
3. On the _UPN Suffixes_ tab, type an alternative UPN suffix for the forest, and then click _Add_.

## Import Agency-Specific PIV Issuer Certificates

Your agency will have to trust the Issuer's certificates for the other agencies. You will need to install ALL the Intermediate and Issuing CA certificates into your NT Auth store for your agency networks. The agency specific PIV issuer certificates can be found in the Authority Information Access (AIA) link given in the PIV Issuers table below. Once you download the .p7c file, you will find the Issuer's public certificate. You will also be able to retrieve the other certificates in the chain to COMMON using the AIA specified in those certificates.

The agency specific PIV Issuer certificates can also be found in the [FPKI Crawler](https://fpki-graph.fpki-lab.gov/crawler/){target="_blank"}_ website. You will find the certificate listed by agencies in the table 'Certificate Files Grouped by Type'. Once you locate the agency, you can download the certificates and the path to COMMON in p7b format.
{target="_blank"}_.

Import the certificates in the Windows [NTAuth Trust Store](https://piv.idmanagement.gov/networkconfig/trustedroots/){target="_blank"}_.

## Link Account of the Other Agency User

When a user authenticates with another agency PIV/CAC card, the credential of that user may not match the account created in the Active Directory user setup in your agency. There are multiple ways to [link that PIV/CAC card](https://piv.idmanagement.gov/networkconfig/accounts/){target="_blank"} owner to the Active Directory account.

## List of PIV Issuers

This table contains the information for U.S. Executive Branch Agencies and the Certification Authorities that are used for _PIV/CAC_ credentials.
 
This table contains the links for downloading all the XXX number of certificates.  How many certificates are there?  
This table exists as a machine readable file that can be downloaded here (from this repo) and will be a CSV? or YAML? or JSON?

TWO TABLES

TABLE ONE

| Issuing Certification Authorities | AIA URIs | OCSP  | CRL |
|------|-------|-------|------
{% for issuer in site.data.pivissuers %}
|{{ issuer.Issuer }}|[{{ issuer.AIA }}]({{ issuer.AIA }}){target="_blank"}|{{ issuer.OCSP }}|{{ issuer.CRL }}|
{% endfor %}

TABLE TWO

| Agency | Issuing Certification Authorities |
|------|-------------|



