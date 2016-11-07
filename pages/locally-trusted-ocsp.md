---
layout: page
title: Locally Trusted OCSP Configuration
permalink: /Locally Trusted OCSP Configuration/
---
#Locally Trusted OCSP Configuration
----------
#####Table of Contents
##[Introduction](#Introduction-1)
##[Security Risks](#Security-Risks-1)
##[Prerequisites](#Prerequisites-1)
##[Locally Trusted Microsoft OCSP Responder](#Locally-Trusted-Microsoft-OCSP-Responder-1)
###[Installation](#Installation-1)
####[Add the ADCS role to the Server](#Add-the-ADCS-role-to-the-Server-1)
####[Initial Configuration](#Initial-Configuration-1)
###[Revocation Sources](#Revocation-Sources-1)
####[Manually Adding a Revocation Source](#Manually-Adding-a-Revocation-Source-1)
####[Using PowerShell to Add a Revocation Source](#Using-PowerShell-to-Add-a-Revocation-Source-1)
##[Windows Client Configuration](#Windows-Client-Configuration-1)
###[Manual Client Configuration](#Manual-Client-Configuration-1)
###[Group Policy Configuration](#Group-Policy-Configuration-1)
##[End-to-End Testing](#End-to-End-Testing-1)
###[Windows certutil](#Windows-certutil-1)
###[Common problems and solutions](#Common-problems-and-solutions-1)

----------

##Introduction
What is OCSP
for locally trusted, not delegated - **not public** - who would want this and why
Non-microsoft clients can use it too

##Security Risks
Are local security requirements and processes on par with external CA/OCSP operation?
Operator is assuming all risks introduced by shortfalls

##Prerequisites
CA to issue responder certificates
Windows 2012 R2 server
Recommended: Hardware security module(s)

##Locally Trusted Microsoft OCSP Responder
Other products could be used
Again - this is local only

###Installation
Administrative rights / domain right needed

####Add the ADCS role to the Server
Step by step through software install, screen shots

####Initial Configuration
Step by step initial  configuration, screen shots

###Revocation Sources
Every issuer CA certificate must be individually configured 
General guidance on CRL update frequency

####Manually Adding a Revocation Source
Step by step, with screen shots

####Using PowerShell to Add a Revocation Source

	include code sample

##Windows Client Configuration 

###Manual Client Configuration
mmc.exe to configure local certificate store properties

###Group Policy Configuration
group policy editor

##End-to-End Testing

###Windows certutil
Use certutil and CAPI 2 event logging to test and debug operation

###Common problems and solutions
Event log entries, what they means, how to fix them
