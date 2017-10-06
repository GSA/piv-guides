---
layout: default
title: Configure Network Authentication to Accept Other Agency PIV/CAC cards
collection: userconfig
permalink: networkconfig/11_accept-all-agency-piv.md/
---

If you want to allow other agency users to authenticate to your agency network, this article will help you configure your agency's Active Directory to support other agency issued PIV/CAC card authentication.

## Network Ports and Protocols - Open Access to OCSP and CRL

The first step in setting up the support for other agency PIV/CAC is to validate that your agencies network is open to the Certificate Issuer website to validate the certificate. Your agency's domain controllers, servers and workstations should be able to access the OCSP and CRL links for validation in real time.

## Domain Controllers - Add Agency UPN Suffix

In order to trust the PIV/CAC cards from another agency, you have to [add the UPN suffix](https://technet.microsoft.com/en-us/library/cc772007(v=ws.11).aspx){target="_blank"}_ of that agency in your agencies Active Directory Domains and Trusts.

To add UPN suffixes

1. Open Active Directory Domains and Trusts. To open Active Directory Domains and Trusts, click Start , click Administrative Tools, and then click Active Directory Domains and Trusts .
2. In the console tree, right-click Active Directory Domains and Trusts, and then click Properties.
3. On the UPN Suffixes tab, type an alternative UPN suffix for the forest, and then click Add.

## Trust Store - Import Agency Specific PIV Issuer Certificates

The agency specific PIV Issuer certificates can be found on the [FPKI Crawler](https://fpki-graph.fpki-lab.gov/crawler/){target="_blank"}_ website. You will find the certificate listed by agencies in the table 'Certificate Files Grouped by Type'. Once you locate the agency, you can download the certificates and the path to COMMON in p7b format.
{target="_blank"}_.

Import the certificates in the Windows [NTAuth Trust Store](https://piv.idmanagement.gov/networkconfig/trustedroots/){target="_blank"}_.

## Account Linking - Other Agency Users

When a user authenticates with another agency PIV/CAC card, the credential of that user may not match the account created in the Active Directory user setup in your agency. There are multiple ways to match that PIV/CAC card owner to the Active Directory account.

## List of PIV Issuers

| Name | PIV Issuer  | Links |
|------|-------------|-------|
|Department of Defense|||
|Department of Homeland Security|OU = DHS CA4<br>OU = Certification Authorities<br>OU = Department of Homeland Security<br>O = U.S. Government<br>C = US|AIA: http://pki.dimc.dhs.gov/dhsca_ee_aia.p7c<br/><br/>OCSP: http://ocsp.dimc.dhs.gov<br/><br/>CRL: http://pki.dimc.dhs.gov/DHS_CA1.crl |
|Department of State|CN = U.S. Department of State PIV CA<br/>CN = AIA<br/>CN = Public Key Services<br/>CN = Services<br/>CN = Configuration<br/>DC = state<br/>DC = sbu<br/>|AIA: http://crls.pki.state.gov/AIA/CertsIssuedToDoSPIVCA.p7c<br/><br/>OCSP: http://ocsp.pki.state.gov/OCSP/DoSOCSPResponder<br/><br/>CRL: http://crls.pki.state.gov/crls/DoSADPKIPIVCA.crl|
|Entrust Federal SSP|Entrust Federal SSP||
|Executive Office of the President|CN = Executive Office of the President CA-B8<br/>OU = PKI<br/>OU = Services<br/>DC = ssp<br/>DC = eop<br/>DC = gov<br/>|AIA: http://aia1.ssp-strong-id.net/CA/EOP-SSP-CA-B8.p7c<br/>http://keys.eop.gov/ca/eopcaB8.p7c<br/>http://strong-auth.eop.gov/ca/EOP-SSP-CA-B8.p7c<br/><br/>OCSP:http://ocsp1.ssp-strong-id.net/EOP-SSP-CA-B8/<br/><br/>http://strong-auth.eop.gov/OCSP/<br/><br/>CRL: URL=http://cdp1.ssp-strong-id.net/CDP/EOP-SSP-CA-B8.crl<br/>URL=http://keys.eop.gov/eopcab8.crl<br/>URL=http://strong-auth.eop.gov/CRL/EOP-SSP-CA-B8.crl<br/>|
|FAA|CN = U.S. Department of Transportation Agency CA G4<br/>OU = U.S. Department of Transportation<br/>O = U.S. Government<br/>C = US|AIA:  http://ssp-aia.symauth.com/SSP/DoT_Agency_G4.p7c<br/>OCSP:  http://ssp-ocsp.symauth.com<br/><br/>CRL:  http://onsitecrl.verisign.com/USDepartmentofTransportationFAAPIVG4/LatestCRL.crl|
|NASA|||
|USAccess|OU = Entrust Managed Services SSP CA <br>OU = Certification Authorities<br> O = Entrust<br> C = US | AIA: http://sspweb.managed.entrust.com/AIA/CertsIssuedToEMSSSPCA.p7c<br> OCSP:<br>  CRL: http://sspweb.managed.entrust.com/CRLs/EMSSSPCA2.crl |
