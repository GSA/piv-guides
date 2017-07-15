---
layout: default
title: Introduction to Network Authentication Guides
permalink: /networkconfig/
collection: networkconfig
---

These Network Authentication guides are to help you configuring your Windows _network domain_ for smartcard logon using PIV credentials.

There are many useful pages and technical articles available online which include details on configurations and using generic smartcards.  The information presented here is to address common questions and configurations **specific** to the US Federal Government, **PIV** smartcards, and US Federal civilian agency certificate authorities.

## Pre-Launch Checklist
Check the following items **before** reviewing these network guides and lessons learned:

1. Users have PIV credentials and PIV card readers
1. You are using Microsoft Active Directory to manage your Windows network
1. Domain Controllers are Microsoft 2008 R2 or 2012 or above
1. User workstations **are joined** to the network and are Windows 7, Windows 8 or Windows 10

## Configuration Checklist

There are five configuration categories to review through with your colleagues.  

- [Network Ports and Protocols]({{site.baseurl}}/networkconfig/ports/)
- [Domain Controllers]({{site.baseurl}}/networkconfig/domaincontrollers/)
- [Trust Stores]({{site.baseurl}}/networkconfig/trustedroots/)
- [Account Linking: Associating PIV credentials to User Accounts]({{site.baseurl}}/networkconfig/accounts/)
- [Group Policies and Enforcement]({{site.baseurl}}/networkconfig/grouppolicies/)

{% include alert-info.html heading = "Teamwork" content="Work with your Network Engineers, Domain Admins, Account Management, and Information Security colleagues to review the information, perform the configurations, and troubleshoot any issues together." %}

We want to add additional information for installing online certificate status protocol (OCSP) services, tuning configurations, common errors and troubleshooting, and configuring MacOSX or other operating systems.  

Submit an [Issue]({{site.repo_url}}/issues) to identify information that would be helpful to you, or consider contributing a page to these guides with your lessons learned.   

There are options for workstations and devices that are Mac OS based and joined to a Windows network; these will to be covered in additions to these guides.
