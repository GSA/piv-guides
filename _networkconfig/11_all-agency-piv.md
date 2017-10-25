---
layout: default
title: Configure Network Authentication To Accept Other Agency PIV/CAC Cards
collection: networkconfig
permalink: networkconfig/11_accept-all-agency-piv.md/
---

##### Last Updated: October 24, 2017

Your agency provides network accounts to government users on detail and those who cross-collaborate on special programs. Rather than issue them new credentials, you can enable their home-agency PIV/CAC credentials so they can authenticate to your network.

* [Network Ports and Protocols](#network-ports-and-protocols)
* [Add Agency UPN Suffix in AD](#domain-controllers)
* [Import Agency-Specific PIV Issuer Certificates](#trust-stores)
* [Link Account of the Other Agency Users](#account-linking)
* [List of PIV Issuers](#list-of-piv-issuers)

## 1&nbsp;&nbsp;Network Ports and Protocols
<!--We don't use the terms "network ports and protocols" anywhere. Firewall configuration? Is the need for network access to PIV Issuer website in order for DCs, servers, and workstations to have access OCSP and CRLs? If so, then we can reduce some redundancy in this paragraph.-->
<!--It sounds like the admin is validating the user's PIV/CAC certificate for first-time log in via the PIV Issuer website AND then validating it again via the OCSP and CRLs. Is this correct?-->To allow these users to authenticate, your network must have access to a user's home agency <**PIV Issuer's?**> Certificate Issuer's website so you can validate their certificates<!--Is the "Certificate Issuer" the same as the "PIV Issuer"?-->. Your agency's domain controllers, servers, and workstations must also have access to the On-line Certificate Status Protocol (OCSP) Responder and Certificate Revocation List (CRL) links for real-time certificate validation. For this to work, you'll need to configure your firewalls to allow this access.

You can find the OCSP and CRL links in the PIV Issuers List below.

You can also use the CRL end-points to poll<!--Does the OCSP Responder poll the CRL end-points to import their data?--> the CRL data into your agency's local OCSP Responders (for those that have them installed!) and route your agency's intranet traffic<!--What part of the intranet traffic?--> to your agency's OCSP Responders. How would you do this?  We will tell you - this can be configured in your Microsoft domain as an AD setting.

## 2&nbsp;&nbsp;Domain Controllers

In order for your agency to trust other agencies' users' PIV/CACs, you'll have to add those agencies' [UPN suffixes](https://technet.microsoft.com/en-us/library/cc772007(v=ws.11).aspx){target="_blank"}_ to your Windows AD Domains and Trusts:

1. Click through _Start_ &gt; _Administrative Tools_ &gt; _Active Directory Domains and Trusts_.
2. In the console tree, right-click _AD Domains and Trusts_ and then click _Properties_.
3. On the _UPN Suffixes_ tab, type an alternative UPN suffix for the forest, and then click _Add_.

## 3&nbsp;&nbsp;Trust Stores

Your agency will have to trust the PIV Issuer's certificates for these users.<!--meaning?-->. You'll need to install ALL of the Intermediate and Issuing CA certificates into your NT Auth Trust Store for your agency networks. The agency-specific PIV Issuer certificates can be found via the Authority Information Access (AIA) links given in the PIV Issuers table below. 

* Download the .p7c file, where you will find the Issuer's public certificate. 
* You can also retrieve the other certificates in the chain to COMMON using the AIA extensions <!--Links?--->specified in those certificates.

The agency-specific PIV Issuer certificates can also be found in the [FPKI Crawler](https://fpki-graph.fpki-lab.gov/crawler/){target="_blank"}_ website. These are listed by agency in the table, _Certificate Files Grouped by Type_. Once you locate a specific agency, you can download the certificates and the path to COMMON in .p7b format.
{target="_blank"}_.

Import the certificates into the Windows [NTAuth Trust Store](https://piv.idmanagement.gov/networkconfig/trustedroots/){target="_blank"}_.

## 4&nbsp;&nbsp;Account Linking

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



