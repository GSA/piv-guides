---
layout: default
title: Accept All PIV/CAC Cards
collection: networkconfig
permalink: networkconfig/accept-all-piv/
---

##### Last Updated: November 13, 2017

Your agency provides network accounts to government users on detail and those who cross-collaborate on special programs. Rather than issue them new credentials, you can allow them to authenticate to your network with their home-agency PIV/CAC credentials.

This guide will help you configure your Windows network domain to accept other agency users' PIV/CAC credentials.

* [1 Network Ports and Protocols](#1-network-ports-and-protocols)
* [2 Domain Controllers](#2-domain-controllers)
* [3 Trust Stores](#3-trust-stores)
* [4 Account Linking](#4-account-linking)
* [PIV Issuers Lists](#piv-issuers-lists)

## 1 Network Ports and Protocols

Your network must have access to the PIV/CAC Issuers' websites for other agencies so it can validate their certificates. Your agency's domain controllers, servers, and workstations must have access to the PIV/CAC Issuers' On-line Certificate Status Protocol (OCSP) Responder and Certificate Revocation List (CRL) links so you can validate certificate-revocation statuses in real-time. OCSP and CRL end-points are used to define configurations for the firewalls. You must allow access to these end-points through the firewalls so this will work. For additional information, see the PIV-Guides' [Network Ports and Protocols Playbook]({{site.baseurl}}/networkconfig/ports/#network-ports-and-protocols).

You can find the OCSP and CRL links in the [PIV/CAC Issuers List](#piv-and-cac-issuers-list) below.

Once your network allows these accesses, you can poll the CRL end-points to retrieve fresh data for your agency's own local OCSP Responders (for those that have them installed!) and route your agency's intranet traffic to them. How would you do this? Go to: [Configuring Certificate Revocation](https://technet.microsoft.com/en-us/library/cc771079(v=ws.11).aspx){:target="_blank"}.

## 2 Domain Controllers

In order for your network to trust a PIV/CAC credential from another agency, you'll have to add the user's home-agency's [UPN suffix](https://technet.microsoft.com/en-us/library/cc772007(v=ws.11).aspx){:target="_blank"}_ to your Windows AD Domains and Trusts:

1. Click through _Start_ &gt; _Administrative Tools_ &gt; _Active Directory Domains and Trusts_.
2. In the console tree, right-click _AD Domains and Trusts_ and then click _Properties_.
3. On the _UPN Suffixes_ tab, add the _UPN suffix_ for the agency, and then click _Add_.

## 3 Trust Stores

To authenticate these users to your network, you will need to trust their agencies' PIV/CAC Issuers by installing ALL of the Intermediate and Root CA certificates in the NTAuth Trust Store. The PIV/CAC Issuer certificates can be found in the Authority Information Access (AIA) links given in the [PIV/CAC Issuers List](#piv-and-cac-issuers-list) below. 

* Download the .p7c file, where you will find the PIV/CAC Issuer's public certificate. 
* You need to also retrieve and install the intermediate certificates in the chain to COMMON using the AIA extensions specified in the issuers' certificates.

The PIV/CAC Issuer certificates can also be found in the [FPKI Crawler](https://fpki-graph.fpki-lab.gov/crawler/){:target="_blank"}_ website. These are listed by agency in the table, _Certificate Files Grouped by Type_. Once you locate a specific agency, you can download the certificates and the path to COMMON in .p7b format.

Import the certificates into the Windows [NTAuth Trust Store](https://piv.idmanagement.gov/networkconfig/trustedroots/){:target="_blank"}_.

## 4 Account Linking

When users authenticate with their home-agency PIV/CACs, the credentials may not match the accounts created in the AD user set-up for your agency. There are multiple ways to link the PIV/CAC credential owner to the AD account. See the [Account Linking](https://piv.idmanagement.gov/networkconfig/accounts/){:target="_blank"} section in PIV-Guides.

You can [map a certificate to a user account](https://technet.microsoft.com/en-us/library/cc754866(v=ws.11).aspx){:target="_blank"} using the Active Directory User and Computers.

## PIV/CAC Issuers List

Table 1 contains the information for U.S. Executive Branch Agencies and the Certification Authorities that are used for PIV/CAC credentials. It contains the information for downloading each certificate using the AIA URL. 

For DoD, go to: [DoD PKI](https://iase.disa.mil/pki-pke/interoperability/Pages/index.aspx#etWPQ7){:target="_blank"}.

{% assign issuerdata=site.data.pivissuers %}
<table>        
    <caption>Table 1: PIV/CAC Issuer's List</caption>
    <thead>
    {% for column in issuerdata[0] %}
        <th>{{ column[0] }}</th>
    {% endfor %}
    </thead>
    <tbody>
    {% for row in issuerdata %}
        <tr>
        {% for cell in row %}
            <td>{{ cell[1] }}</td>
        {% endfor %}
        </tr>
    {% endfor %}
    </tbody>
</table>




