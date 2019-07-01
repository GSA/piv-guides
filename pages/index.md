---
layout: default
title: Introduction - PIV Guides
permalink: /
---

These **Personal Identity Verification** (PIV) Guides are intended to help you implement common PIV configurations at your organization. These guides are [open source]({{ site.repo_url }}) and a _work in progress_ and we [welcome contributions](contribute/) from our colleagues.

The guides focus on using PIV credentials for _logical access_ such as authenticating to networks or applications, or digitally signing and encrypting. Using PIV for _physical access_ will be covered under another set of guides.

If you cannot find a particular topic, it may still be in development. Review the [Issues]({{ site.repo_url }}/issues) for questions and lessons that are in progress. Create a new [Issue]({{ site.repo_url }}/issues) to ask a question or share information with others.  

Read on to learn more about PIV credentials.

1. [What is PIV?](#what-is-piv)
1. [What is in the PIV Guides?](#what-is-in-the-piv-guides)
1. [Why is PIV usage important?](#why-is-piv-usage-important)
1. [What systems should use PIV?](#what-systems-should-use-piv)
1. [Where can I find the Standards?](#where-can-i-find-the-standards)

## What is PIV?

A Personal Identity Verification (PIV) credential is a US Federal governmentwide credential used to access Federally controlled facilities and information systems at the appropriate security level.

PIV credentials have certificates and key pairs, pin numbers, biometrics like fingerprints and pictures, and other unique identifiers.  When put together into a PIV credential, it provides the capability to implement multi-factor authentication for networks, applications and buildings.

## What information is in these PIV guides?  
First, we cover the basics of PIV credentials, including:

-   What PIV is, contains and looks like;
-   The basics of getting started with PIV credentials; and
-   Using PIV for network authentication (smartcard logon). 

We also cover applications, and guidance for developers and users - which need your input!  
{% include alert-success.html heading = "Share your expertise" content="Please contribute and share your lessons for configuring systems or applications, tuning considerations, code, common challenges, troubleshooting errors, as well as anything else you think would be helpful for your colleagues." %}
## Why is PIV usage important?

Enabling systems and facilities to use PIV credentials for authentication enhances agency security. PIV credentials allow for a high level of assurance in the individuals that access your resources, because they are only issued by trusted providers to individuals that have been verified in person. PIV credentials are highly resistant to identity fraud, tampering, counterfeiting, and exploitation.

PIV credentials are _standardized_ as well. PIV credentials might be issued by different organizations using different commercial or open source products, on different form factors (cards, mobile devices, etc).  However, PIV credentials are standardized - every PIV credential is required to have specific information, using technology which is _interoperable_.

Your PIV credential from one agency will have the same basic required format, information and technology as a PIV credential from your partner agencies. This allows us to trust each other, share applications, and architect and implement systems using common patterns for authentication.

## What systems should use PIV?  
Any system at your organization that requires heightened security for determining who should gain access can and should use PIV for authentication. While PIV credentials can be used for authentication on almost any system, they are especially useful for systems that protect sensitive information.

PIV should be used for:

* All authentication for all _privileged_ users including servers, networks, and applications;
* All _network_ authentication for _all_ users;
* All application authentication for _all_ users of an application that protects or contains sensitive information; and
* Access to facilities and buildings.

## Where can I find the Standards?  
Review the information on this site if you are interested in PIV credentials or work on _using_ PIV credentials.

If you are interested in the bits and bytes of PIV credentials, you can review the Standards (see below), particularly if you develop products such as hardware or software that are _specific_ to PIV credentials for the US Federal Government. (For most users and engineers, the Standards may be too detailed for your needs.)

To review the Standards, there is a [NIST website](http://csrc.nist.gov/groups/SNS/piv/standards.html){:target="_blank"}{:rel="noopener noreferrer"} with all PIV related Standards.  Links to some of the most common Standards:

- **[FIPS-201](http://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.201-2.pdf){:target="_blank"}{:rel="noopener noreferrer"}** specifies the issuance and management of PIV credentials.
- **[NIST Special Publication 800-73, "Interfaces for Personal Identity Verification"](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-73-4.pdf){:target="_blank"}{:rel="noopener noreferrer"}** specifies the interface and data elements of PIV credentials.
- **[NIST Special Publication 800-76, "Biometric Data Specification for Personal Identity Verification"](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-76-2.pdf){:target="_blank"}{:rel="noopener noreferrer"}** specifies the technical acquisition and formatting requirements for biometric data of PIV credentials.
