---
layout: default
title: PIV Application Integration Models
permalink: /pivappintmodels/
---

# First, Understand Your Application!
Before determining which PIV application integration model is best for your circumstances, it is very important to first make sure you understand your application and application environment.  It helps to have a two sentence summary of your application and what it does. Other things you should understand are:

- What is the user population?
    - Badged
        - Federal employees/contractors
            - Internal to Agency?
            - Other Federal Government Agencies (OGA)?
    - Unbadged, Trusted
        - State, Local, and Tribal (SLT) users?
        - Public Partner (Counsel, Industry/University partner, etc.)
     - Unbadged, Untrusted
         - Member of the Public
- What is the technology stack? (e.g., Java web app running on Tomcat 7 on a Linux machine, etc.)
- What environments do you have? (e.g., Production, Staging, Pre-Production, Test, etc.)
- How do you currently do authentication? (e.g., username+password)
- How do you currently do authorization? (e.g., mySQL database with custom role information in it)
- Who is the application owner?
- Who manages the development team?
- Who is the lead developer for ICAM integration?
- When must the application be ICAM-integrated in Production?

# Authentication (AuthN) Application Integration Options
Determining which authentication application integration model to use is dependent on the application you are trying to onboard. There are various factors to consider when making that decision. For example:

- What is the performance and development level of effort (LOE) of the application? 
> Performance and LOE can vary greatly between applications.
- What is the user population? It is very important to understand the user population (e.g., their skills and knowledge.

Regardless, you should use a standard format for your onboarding documents:

- Lists of users and roles
- Metadata
- Engagement documents

## *A. Native Security Assertion Markup Language (SAML) Single Sign-on (SSO)* +++++ Link to more technical info

With this approach, your application must support native SAML. Several other things to note:

- There is low development LOE on both sides: the ICAM side and the application side
- Certificates must be synced on both sides
- Metadata needs to be loaded on both sides
- There is moderate coordination effort (i.e., developers on both sides must exchange data and debug at the same time)

## *B. Mediated Integration*

Some SSO systems provide a solution for older or legacy applications that do not directly support SAML. These “mediator” libraries:
        
- Capture the SAML authN request
- Translate to a call that the application understands (e.g., JAVA, .Net, ModAuthMellon, etc.)
   
When selecting an SSO product, it is important to know what options it provides for non-SAML applications. For example:

### *B.1. Mediated Integration - static library ("Fedlet")* +++++ Link to more technical info
For the Fedlet mediated integration approach, you should note the following:

- The web server hands off requests to a special SSO library that manages the SAML session
- Unlike agent, there is no additional process to support SSO
- There is less performance overhead
- Leverages basic SAML support
- There is low development LOE on both sides (ICAM and application)
- Certificates must be synced on both sides
- Metadata needs to be loaded on both sides
- There is moderate coordination effort (i.e., developers on both sides must exchange data and debug at the same time)

### *B.2. Mediated Integration - Listening process (Agent)* +++++ Link to more technical info
For the Agency mediated integration approach, you should note the following:

- The application must install a proprietary or in-house-developed agent to either the web or application tier. Other things to note:
- There is high development effort on the application, and low develoment effort for ICAM
- The application needs to install an agent, which can be complex
- Certificates must be correct
- Metadata must be synced
- There is moderate coordination effort (development on both sides exchanging data and debugging at the same time), once application development of agent installation is complete

## *C. Kerberos SSO to Active Directory (AD)* +++++ Link to more technical info

If your application can be converted to use Kerberos (Kerberos-able), this may be the path of least resistance to be PIV-enabled.  Things to note in this case:
    
- The application must support native Kerberos (sometimes called Windows Integrated Authentication)
- Kerberos provides Authentication (AuthN) and Authorization (AuthZ)
- There is moderate development LOE on application, zero ICAM development LOE
- This approch requires coordination with developers and Active directory
- Role assignment is done within the application
- The userIDs in the application can be mapped directly to an attribute already in ICAM
    - LoginID
    - email
- No ICAM work required to support Authorization

## *D. Identity Proxy*      FIXME - need high-level info on how to implement this

## *E X.509 (Direct PIV) Login* +++++ Link to more technical info

Simply speaking, "PIV" = X.509 = two-way TLS = client authentication. Several things to note about the Direct PIV Login approach:

- The application must support PIV authentication
- The application must be connected to a Certification Authority (CA) for certificates
- The application must map users' PIV credential to application accounts
- There is high development LOE for the application, and no ICAM development involvement

# Authorization (AuthZ) Application Integration Options

There are three approaches to authorization worth noting:
    
- Role assignment within application with identical (1-1) userID mapping
- Role assignment within the application mapped to different userID
- External Role assignment where roles are assigned by Active Directory (AD) or some other mechanism

## *A. Role Mapped to Identical UserID*

UserIDs in the application can map one-to-one with an attribute already in the ICAM Directory:
        
- Network login
- Email address

There is No ICAM development work required to support AuthZ.

## *B. Role Mapped to Different UserID*

In this approach, role is mapped to a differently-named userID.  Further, ICAM must map the application userID to the network login ID.

## *C. Role Mapped Externally*

In this approach, roles are assigned by Active Directory (AD) or some other mechanism.  Other things to note:
    
- ICAM must import the users and roles
- The application must be modified to ingest the roles that ICAM passes.  This will be a manual process at first and:
    - Users must be added to AuthN Directory
    - Users must be added to the AuthZ Directory
- The application owner must provide ICAM with the following information in the agreed-upon format:
    - List of roles
    - Members per role (accurate Active Directory login IDs)

