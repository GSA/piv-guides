---
layout: default
title: Configure Network Authentication To Accept Other Agency PIV/CAC Cards
collection: networkconfig
permalink: networkconfig/11_accept-all-agency-piv/
---

##### Last Updated: October 25, 2017

Your agency provides network accounts to government users on detail and those who cross-collaborate on special programs. Rather than issue them new credentials, you can enable their home-agency PIV/CAC credentials so they can authenticate to your network.

* [1 Network Ports and Protocols](#1-network-ports-and-protocols)
* [2 Domain Controllers](#2-domain-controllers)
* [3 Trust Stores](#3-trust-stores)
* [4 Account Linking](#4-account-linking)
* [PIV Issuers Lists](#piv-issuers-lists)

## 1 Network Ports and Protocols

Your network must have access to the PIV/CAC Issuer websites for other agencies so you can validate their users' certificates. Your agency's domain controllers, servers, and workstations must also have access to the On-line Certificate Status Protocol (OCSP) Responder and Certificate Revocation List (CRL) links to validate their certificate-revocation statuses in real-time. For this to work, you'll need to configure your firewalls to allow these accesses. <!--These OCSP responders and CRL end-points relate to the user's home agency?-->

You can find the OCSP and CRL links in the [PIV and CAC Issuers List](#piv-and-cac-issuers-list) below.

You can also poll these CRL end-points to retrieve fresh data for your agency's own local OCSP Responders (for those that have them installed!) and route your agency's intranet traffic to them. How would you do this? You can configure your Microsoft domain through Windows AD setting.<**What is that setting? Add steps? Provide a link to steps?**>

For additional information, see the FPKI-Guides' [Network Ports and Protocols Playbook]({{site.baseurl}}/networkconfig/ports/#network-ports-and-protocols).

## 2 Domain Controllers

In order for your agency to trust a PIV/CAC credential from another agency, you'll have to add the user's home-agency's [UPN suffixes](https://technet.microsoft.com/en-us/library/cc772007(v=ws.11).aspx){target="_blank"}_ to your Windows AD Domains and Trusts:

1. Click through _Start_ &gt; _Administrative Tools_ &gt; _Active Directory Domains and Trusts_.
2. In the console tree, right-click _AD Domains and Trusts_ and then click _Properties_.
3. On the _UPN Suffixes_ tab, type an alternative UPN suffix for the forest, and then click _Add_.

## 3 Trust Stores

To authenticate these users to your network, your agency will have to trust their PIV/CAC Issuers' certificates. You'll need to install ALL of the Intermediate and Issuing CA certificates into the NT Auth Trust Store for your agency networks. The agency-specific, PIV/CAC Issuer certificates can be found via the Authority Information Access (AIA) links given in the [PIV and CAC Issuers List](#piv-and-cac-issuers-list) below. 

* Download the .p7c file, where you will find the PIV/CAC Issuer's public certificate.<!--One or multiple certificates? Next sentence says "those certificates."--> 
* You can also retrieve and install the Intermediate and Issuing CA certificates in the chain to COMMON using the AIA extensions <!--Links?--->specified in those certificates.<!--"Those certificates" refers to which certificates?-->

**CB STOPPED**

The agency-specific PIV Issuer certificates can also be found in the [FPKI Crawler](https://fpki-graph.fpki-lab.gov/crawler/){target="_blank"}_ website. These are listed by agency in the table, _Certificate Files Grouped by Type_. Once you locate a specific agency, you can download the certificates and the path to COMMON in .p7b format.
{target="_blank"}_.

Import the certificates into the Windows [NTAuth Trust Store](https://piv.idmanagement.gov/networkconfig/trustedroots/){target="_blank"}_.

## 4 Account Linking

When a user authenticates with his/her home-agency PIV/CAC card, the credential may not match the account created in the AD user set-up for your agency. There are multiple ways to [link that PIV/CAC credential](https://piv.idmanagement.gov/networkconfig/accounts/){target="_blank"} owner to the AD account.

## PIV Issuers List

This table contains the information for U.S. Executive Branch Agencies and the Certification Authorities that are used for PIV/CAC credentials.
 
This table contains the links for downloading all the XXX number of certificates.  How many certificates are there?  
This table exists as a machine readable file that can be downloaded here (from this repo) and will be a CSV? or YAML? or JSON?

TABLE 1. PIV Issuer's List

| Issuing Certification Authorities | AIA URIs | OCSP  | CRL |
|------|-------|-------|------
{% for issuer in site.data.pivissuers %}
|{{ issuer.Issuer }}|[{{ issuer.AIA }}]({{ issuer.AIA }}){target="_blank"}|{{ issuer.OCSP }}|{{ issuer.CRL }}|
{% endfor %}

TABLE TWO

| Agency | Issuing Certification Authorities |
|------|-------------|



