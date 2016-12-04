---
layout: default
title: Introduction to Network Authentication Guides
permalink: /networkconfig/
collection: networkconfig
---

These Network Authentication guides are to help you configuring your Windows _network domain_ for smartcard logon using PIV credentials.

There are many useful pages and technical articles available online which include details on configurations and using generic smartcards.  The information presented here is to address common questions and configurations **specific** to the US Federal Government, **PIV** smartcards, and US Federal civilian agency certificate authorities.

There are five configuration categories to review through with your colleagues.  We recommend working with your Network Engineers, Domain Admins, Account Management, and Information Security colleagues to review the information, perform the configurations, and troubleshoot any issues together.

1. [Network Ports and Protocols](../networkconfig/ports/)
2. [Domain Controllers](../networkconfig/domaincontrollers/)
3. [Trust Stores](../networkconfig/trustedroots/)
4. [Account Linking: Associating PIV credentials to User Accounts](../networkconfig/accounts/)
5. [Group Policies and Enforcement](../networkconfig/grouppolicies/)

We want to add additional information for installing online certificate status protocol (OCSP) services, tuning configurations, common errors and troubleshooting, and configuring MacOSX or other operating systems.  Submit an Issue to identify information that would be helpful to you, or consider contributing a page to these guides with your lessons learned.   

#### Assumptions
You should check the following items before reviewing these network guides and lessons learned:

*  Users have PIV cards and PIV card readers
*  You're using Microsoft Active Directory to manage your Windows network
*  Domain Controllers are Microsoft 2008 R2 or 2012
*  User workstations joined to the network are Windows 7, Windows 8 or Windows 10
   * There are options for workstations that are Mac OS based and joined to a Windows network to be covered in addendums to this guide
