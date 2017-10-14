---
layout: default
title: Configure Network Authentication To Accept Other Agency PIV/CAC Cards
collection: networkconfig
permalink: networkconfig/11_accept-all-agency-piv.md/
---

Published On: October 6th, 2017<br/>
Last Updated On: October 14th, 2017

<!--Based on LaChelle's Use Case. More complete description. May edit further. LaChelle's notes say "any government user," not just those on detail or who collaborate on programs.-->Your agency provides network accounts to government users on detail, as well as those who cross-collaborate on special programs. They need to authenticate to your network with their home-agency PIV/CAC credentials, rather than issuing them new credentials. 

This guide will help you configure Active Directory (AD) on your domains to allow government users with a PIV/CAC credential to authenticate. 

* [Network Ports and Protocols &mdash; Open Access to OCSP and CRL](#nework-ports-and-protocols-open-access-to-ocsp-and-crl)
* [Domain Controllers &mdash; Add Agency UPN Suffix](#domain-controllers-add-agency-upn-suffix)
* [Trust Store &mdash; Import Agency-Specific PIV Issuer Certificates](#trust-store-import-agency-specific-piv-certificates)
* [Account Linking &mdash; Other Agency Users](#account-linking-other-agency-users)
* [List of PIV/CAC Issuers](#list-of-piv/cac-issuers)


<!--I'm thinking that the following headings should be numbered to show that these are ordered steps--a bit of a roadmap-->

## Network Ports and Protocols &mdash; Open Access to OCSP and CRL

To configure your network to authenticate users via their home-agency PIV/CAC credentials, you need to verify that your network <!--Explain "is open to...Is this what you mean?" Some agency networks don't allow access to other agencies' Certificate Issuer websites?-->allows access to their home agency's Certificate Issuer website to validate the certificate. Your agency's domain controllers, servers and workstations need to access the On-line Certificate Status Protocol (OCSP) and Certificate Revocation List (CRL) links for validation in real-time<!--Immediate/instantaneous?-->. You can find the OCSP and CRL links in the List of Issuers table below.

## Domain Controllers:&nbsp;&nbsp;Add Agency UPN Suffix

In order to trust PIV/CAC credentials from another agency, you'll have to add that agency's [UPN suffix](https://technet.microsoft.com/en-us/library/cc772007(v=ws.11).aspx){target="_blank"}_ to your agency's AD Domains and Trusts.

1. Click through _Start_ &gt; _Administrative Tools_ &gt; _Active Directory Domains and Trusts_.
2. In the console tree, right-click _AD Domains and Trusts_ and then click _Properties_.
3. On the _UPN Suffixes_ tab, type an alternative UPN suffix for the forest, and then click _Add_.

## Trust Store &mdash; Import Agency-Specific PIV Issuer Certificates

Your agency will have to trust the Issuer's certificates for the other agencies. The agency specific PIV issuer certificates can be found in the Authority Information Access (AIA) link given in the PIV Issuers table below. Once you download the .p7c file, you will find the Issuer's public certificate. You will also be able to retrieve the other certificates in the chain to COMMON using the AIA specified in those certificates.

The agency specific PIV Issuer certificates can also be found in the [FPKI Crawler](https://fpki-graph.fpki-lab.gov/crawler/){target="_blank"}_ website. You will find the certificate listed by agencies in the table 'Certificate Files Grouped by Type'. Once you locate the agency, you can download the certificates and the path to COMMON in p7b format.
{target="_blank"}_.

Import the certificates in the Windows [NTAuth Trust Store](https://piv.idmanagement.gov/networkconfig/trustedroots/){target="_blank"}_.

## Account Linking &mdash; Other Agency Users

When a user authenticates with another agency PIV/CAC card, the credential of that user may not match the account created in the Active Directory user setup in your agency. There are multiple ways to [link that PIV/CAC card](https://piv.idmanagement.gov/networkconfig/accounts/){target="_blank"} owner to the Active Directory account.

## List of PIV Issuers

This table contains the information for U.S. Executive Branch Agencies and the Certification Authorities that are used for _PIV/CAC_ credentials.

OCSP and CRL endpoints are used to define configurations for the firewalls. You must allow access to these endpoints through the firewalls so this will work.

You can also use the CRL endpoints to poll the CRL data into your local internal agency OCSP responders (for those that have them installed!) and route your internal agency intranet traffic to your internal agency ocsp responders. 
How would you do this?  We will tell you - this can be configured in your microsoft domain as a setting.  
You will need to install ALL the Intermediate and Issuing CA certificates into your NT Auth store for your agency networks.  
This table contains the links for downloading all the XXX number of certificates.  How many certificates are there?  
This table exists as a machine readable file that can be downloaded here (from this repo) and will be a CSV? or YAML? or JSON?

TWO TABLES

TABLE ONE
This is for the END ENTITY Certificates first....

| Issuing Certification Authorities | OCSP  | CRL | AIA URIs |
|------|-------|-------|------

TABLE TWO

| Agency | Issuing Certification Authorities |
|------|-------------|


| Name | PIV/CAC Issuer  | Links |
|------|-------------|-------|
|Department of Defense|||
|Department of Homeland Security|OU = DHS CA4<br>OU = Certification Authorities<br>OU = Department of Homeland Security<br>O = U.S. Government<br>C = US|AIA: http://pki.dimc.dhs.gov/dhsca_ee_aia.p7c<br/><br/>OCSP: http://ocsp.dimc.dhs.gov<br/><br/>CRL: http://pki.dimc.dhs.gov/DHS_CA1.crl |
|Department of State|CN = U.S. Department of State PIV CA<br/>CN = AIA<br/>CN = Public Key Services<br/>CN = Services<br/>CN = Configuration<br/>DC = state<br/>DC = sbu<br/>|AIA: http://crls.pki.state.gov/AIA/CertsIssuedToDoSPIVCA.p7c<br/><br/>OCSP: http://ocsp.pki.state.gov/OCSP/DoSOCSPResponder<br/><br/>CRL: http://crls.pki.state.gov/crls/DoSADPKIPIVCA.crl|
|Entrust Federal SSP|||
|Executive Office of the President|CN = Executive Office of the President CA-B8<br/>OU = PKI<br/>OU = Services<br/>DC = ssp<br/>DC = eop<br/>DC = gov<br/>|AIA: http://aia1.ssp-strong-id.net/CA/EOP-SSP-CA-B8.p7c<br/>http://keys.eop.gov/ca/eopcaB8.p7c<br/>http://strong-auth.eop.gov/ca/EOP-SSP-CA-B8.p7c<br/><br/>OCSP:http://ocsp1.ssp-strong-id.net/EOP-SSP-CA-B8/<br/><br/>http://strong-auth.eop.gov/OCSP/<br/><br/>CRL: URL=http://cdp1.ssp-strong-id.net/CDP/EOP-SSP-CA-B8.crl<br/>URL=http://keys.eop.gov/eopcab8.crl<br/>URL=http://strong-auth.eop.gov/CRL/EOP-SSP-CA-B8.crl<br/>|
|FAA|CN = U.S. Department of Transportation Agency CA G4<br/>OU = U.S. Department of Transportation<br/>O = U.S. Government<br/>C = US|AIA:  http://ssp-aia.symauth.com/SSP/DoT_Agency_G4.p7c<br/>OCSP:  http://ssp-ocsp.symauth.com<br/><br/>CRL: http://onsitecrl.verisign.com/USDepartmentofTransportationFAAPIVG4/LatestCRL.crl|
|Health & Human Services|||
|NASA|||
|Naval Reactors SSP Agency CA G3|||
|Senate|CN = Senate PIV-I CA G4<br/>OU = Office of the Sergeant at Arms<br/>OU = U.S. Senate<br/>O = U.S. Government<br/>C = US|AIA: http://ssp-aia.symauth.com/VTNSSP/USSenate-PIV-I-G4.p7c<br/>OCSP: http://ssp-ocsp.symauth.com<br/>CRL: http://onsitecrl.verisign.com/USSenateSSPPIVIG4PROD/LatestCRL.crl|
|Social Security Administration|OU = Social Security Administration Certification Authority<br/>OU = SSA<br/>O = U.S. Government<br/>C = US|AIA: http://pki.treas.gov/ssaca_ee_aia.p7c|
|Treasury|||
|USAccess|OU = Entrust Managed Services SSP CA <br>OU = Certification Authorities<br> O = Entrust<br> C = US | AIA: http://sspweb.managed.entrust.com/AIA/CertsIssuedToEMSSSPCA.p7c<br> OCSP:<br>  CRL: http://sspweb.managed.entrust.com/CRLs/EMSSSPCA2.crl |
|Veterans Affairs|||
