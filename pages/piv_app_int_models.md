---
layout: default
title: PIV Application Integration Models
permalink: /piv_app_int_models/
---

# Authentication (AuthN) Options
Determining which authentication application integration model to use is dependent on the application you are trying to onboard. There are various factors to consider when making that decision. For example:
- What is the performance and development level of effort (LOE) of the application? Performance and LOE can vary greatly between applications.
- What is the user population? It is very important to understand the user population (e.g., their skills and knowledge.

Regardless, you should use a standard format for your onboarding documents:
- Lists of users and roles
- Metadata
- Engagement documents

## Understand your Application!
It helps to have a two sentence summary of your application and what it does. You should also understand the various specific facets of the application.  For example:

- What is the user population?
        Badged
            Federal employees/contractors
                Internal to Agency?
                Other Federal Government Agencies (OGA)?
        Unbadged, Trusted
            State, Local, and Tribal (SLT) users?
            Public Partner (Counsel, Industry/University partner, etc.)
        Unbadged, Untrusted
            Member of the Public
    
- What is the technology stack? (e.g., Java web app running on Tomcat 7 on a Linux machine, etc.)
- What environments do you have? (e.g., Production, Staging, Pre-Production, Test, etc.)
- How do you currently do authentication? (e.g., username+password)
- How do you currently do authorization? (e.g., mySQL database with custom role information in it)
- Who is the application owner?
- Who manages the development team?
- Who is the lead developer for ICAM integration?
- When must the application be ICAM-integrated in Production?

## Native Security Assertion Markup Language (SAML) Single Sign-on (SSO) +++++ Link to more technical info

With this approach, your application must support native SAML. Several other things to note:

- There is low development LOE on both sides: the ICAM side and the application side
- Certificates must be synced on both sides
- Metadata needs to ve loaded on both sides
- There is moderate coordination effort (i.e., developers on both sides must exchange data and debug at the same time)

### Mediated Integration

Some SSO systems provide a solution for older or legacy applications that do not directly support SAML. These “mediator” libraries:
        
- Capture the SAML authN request
- Translate to a call that the application understands (e.g., JAVA, .Net, ModAuthMellon, etc.)
   
When selecting an SSO product, it is important to know what options it provides for non-SAML applications. For example:

- Mediated Integration - static library ("Fedlet") +++++ Link to more technical info
- The web server hands off requests to a special SSO library that manages the SAML session
- Unlike agent, there is no additional process to support SSO
- There is less performance overhead
- Leverages basic SAML support
- There is low development LOE on both sides (ICAM and application)
- Certificates must be synced on both sides
- Metadata needs to be loaded on both sides
- There is moderate coordination effort (i.e., developers on both sides must exchange data and debug at the same time)

Mediated Integration - Listening process (Agent) +++++ Link to more technical info

    Application must install a proprietary or in-house-developed agent to either web or application tier
    High development effort on application, low effort for ICAM
        Application must install agent, which can be complex
        Certificates must be correct
        Metadata must be synced
    Moderate coordination effort (Devs on both sides exchanging data and debugging at the same time), once application development of agent installation is complete

Kerberos SSO to AD +++++ Link to more technical info

    If your application is Kerberos-able, this may be the path of least resistance to be PIV-enabled
    Application must support native Kerberos (sometimes called Windows Integrated Authentication)
    Provides Authentication (AuthN) and Authorization (AuthZ)
    Moderate LOE on application, zero ICAM LOE
    Requires coordination with developers and Active directory
    Role Assignment within Application
    The userIDs in the application can be mapped directly to an attribute already in ICAM
        LoginID
        email
    No ICAM work required to support AUTHZ

Identity Proxy

FIXME - need high-level info on how to implement this
X509 (Direct PIV) Login +++++ Link to more technical info

    Application must support PIV authentication
    Application must be connected to CA for certificates
    Application must map users PIV credential to app accounts
    High LOE for application, no ICAM involvement

## Authorization (AuthZ) Options

    Role Assignment within Application with identical (1-1) userID mapping
    Role Assignment within Application – mapped to different userID
    External Role assignment – roles are assigned by AD or some other mechanism

Role mapped to identical userID

    UserIDs in application can map one-to-one with an attribute already in the ICAM Directory:
        Network login
        Email address
    No ICAM work required to support AUTHZ

Role mapped to different UserID

• Role is mapped to a differently named userID
• ICAM must map the application userID to the network login ID
Role mapped externally

    Roles are assigned by AD or some other mechanism
    ICAM must import the users and roles
    The application must be modified to ingest the roles that ICAM passes
    This will be a manual process at first and:
        Users must be added to AuthN directory
        Users must be added to the AuthZ directory
    The application owner must provide ICAM with the following information in the agreed-upon format:
        List of Roles
        Members per role (accurate AD login IDs)

