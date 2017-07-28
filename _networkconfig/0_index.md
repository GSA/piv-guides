---
layout: default
title: Introduction to Network Authentication Guides
permalink: /networkconfig/
collection: networkconfig
---

These Network Authentication guides will help you configure your Windows _network domain_ for smartcard logon using PIV credentials.

There are many useful pages and technical articles available online that include details on configurations and using generic smartcards.  The information presented here addresses common questions and configurations **specific** to the US Federal Government, **PIV** smartcards, and US federal civilian agency Certification Authorities.

{% include alert-info.html heading = "Teamwork" content="Work with your Network Engineers, Domain Admins, Account Management, and Information Security colleagues to review the information, perform the configurations, and troubleshoot any issues together." %}

## Pre-Launch Checklist

Check the following items **before** reviewing these network guides and lessons learned:

1. Users have PIV credentials and PIV card readers
1. You are using Microsoft Active Directory to manage your Windows network
1. Domain Controllers are Microsoft 2008 R2 or 2012 or above
1. User workstations **are joined** to your network and are Windows 7, Windows 8, or Windows 10-based

## Configuration Checklist

There are five configuration categories to review with your colleagues.  All five includes steps that need to be completed and it's best to review and complete in this order:    

- [Network Ports and Protocols]({{site.baseurl}}/networkconfig/ports/)
- [Domain Controllers]({{site.baseurl}}/networkconfig/domaincontrollers/)
- [Trust Stores]({{site.baseurl}}/networkconfig/trustedroots/)
- [Account Linking: Associating PIV credentials with User Accounts]({{site.baseurl}}/networkconfig/accounts/)
- [Group Policies and Enforcement]({{site.baseurl}}/networkconfig/grouppolicies/)


There are two additional guides with pointers for tuning and using a local certification authority for domain controller certificates:

- [Network Tuning]({{site.baseurl}}/networkconfig/tuning/)
- [Local Certification Authority]({{site.baseurl}}/networkconfig/localca/)

We want to add additional information for installing online certificate status protocol (OCSP) services, common errors and troubleshooting, and configuring MacOSX and other operating systems.  

Submit an [Issue]({{site.repo_url}}/issues) to identify information that would be helpful to you, or consider contributing a page to these guides with your lessons learned.   


