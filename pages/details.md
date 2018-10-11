---
layout: default
title: Details of a PIV Credential
permalink: /details/
---

You can use these simple methods to view, export, and understand the information stored on a PIV credential.

-   [View Your PIV Credential Certificates](#view-your-piv-credential-certificates)
-   [Export PIV Certificates](#export-piv-certificates)
-   [Understand PIV Certificates](#understand-piv-certificates)

## View Your PIV Credential Certificates
Almost **all** of the methods for using your PIV credential for networks, applications, digital signatures, and encryption involve the certificates and key pairs stored on your PIV credential.  There are also scenarios where additional information (such as biometrics) is also accessed and used. 

To view your certificate information:

-   Insert your PIV credential into your card reader.
-   Choose an option from the table below and follow the steps.

| Operating System     | Module   | Steps |
| -------------             |----|----|
| Microsoft   | Internet Explorer  | Open _Internet Explorer Browser_ -> _Tools_ wheel or Alt+X) -> _Internet Options_ -> _Content_ tab -> _Certificates_ button -> _Personal_ tab  |
| Microsoft       | Microsoft Management Console (MMC) and Certificate Snap-in  |  Open _Microsoft Management Console_ -> _File_ -> _Add/Remove Snap-In_ -> _Certificates_ snap-in -> _Add_ -> _My user account_ -> _Finish_ -> Expand _Certificates - Current User_ -> _Personal_ -> _Certificates_   |
| Any   | Chrome Browser  | Open _Chrome Browser_ -> _Settings_ -> _Show Advanced Settings_ -> _Manage Certificates_ (_Manage HTTPS/SSL Certificates and Settings_)  -> _Personal_ tab  |
| Any   | Firefox Browser  | Open _Firefox Browser_ -> _Settings_ wheel -> _Privacy & Security_ -> _Security_ -> _Certificates_ > _View Certificates_ button -> _Certificates Manager_ -> _Your Certificates_ tab
| macOS X   | Keychain  | Open _Applications_ -> _Utilities_ -> _Keychain Access_ -> Select _Login_ -> _Categories_ -> _My Certificates_  |

{% include alert-info.html heading = "View" content="You may see many certificates.  To open and view the certificate details, double-click on any certificate." %}

## Export PIV Certificates
We won't always be using graphical user interfaces to view the PIV credential certificates.  Throughout the _PIV_ and _Federal PKI (FPKI) Guides_, we're continuing to add useful procedures for network engineers and examples of code, tools, and common _command line_ options for viewing and troubleshooting configurations.  (**Note:** These examples may use files representing _public_ certificates.)

{% include alert-info.html heading = "Export" content="Look for an Export button and save the file as DER or PEM-encoded, with a file extension of cer (.cer)." %}

{% include alert-warning.html heading = "Keys are safe!" content="Don't worry - the public certificates are public.  The private keys are always stored safely on your PIV credential and can never be exported. " %}

## Understand PIV Certificates
Viewing the certificate information on your PIV credential may be interesting if you are a general user.  Understanding the certificate information is a **must** if you are a program manager or engineer developing applications and designing solutions for using PIV credentials.

Within the U.S. Federal Government, the certificate and PIV credential information is governed by standards, policies, and implementation-specific choices (options) across all agency credential providers.

Typically, there are four certificates and four key pairs on a PIV credential.  However, one pair (i.e., one certificate and one key pair) is *ALWAYS* on every PIV credential and three pairs (i.e., three certificates and three key pairs) are *SOMETIMES* on a PIV credential.  You can review the [Basics of a PIV Credential](../elements/) to view the four pairs and purposes.

The table below outlines the general information for the PIV credential certificates, certificate extensions, and design considerations. 

{% include alert-info.html heading = "Six Years" content="PIV credentials and certificates have changed over time due to updates in standards.  Since users may have credentials for up to six years and there are both optional and mandatory elements, the information presented is what is valid for ALL PIV credentials and certificates currently in use. (Although credentials are valid for six years, the certificates contained on a credential are valid for only three years.)" %}

| Certificate              | Required  | Key Usage  |  Extended Key Usage  | Subject Alternative Name | Design Considerations |
| -------------            |:----:      |:----:               |:----:               |:----:|  ----|
| PIV Authentication       |Always      | Digital Signature            | Client Authentication           | otherName = FASC-N;<br> uniformResourceIdentifier = UUID;<br>Principal Name = _prefix_@_suffix_  | Principal Name values are **not** required by policy to be present in all Subject Alternative Name extensions. The Card UUID may also commonly be referred to as the Global Unique Identifier (GUID). |
| Card Authentication      |Sometimes      | Digital Signature            | id-PIV-cardAuth            |  Name = FASC-N; <br>uniformResourceIdentifier = UUID|   Card Authentication must be included in new and replacement PIV credentials issued after August 2014; it is not expected that **all** PIV credentials will have Card Authentication certificates until September 2019. The Card UUID may also commonly be referred to as the GUID. |
| Digital Signature        |Sometimes      | Digital Signature, Non-Repudiation            | Specific EKUs are required for certificates issued after June 2019            |  rfc822name = email address | Email address is **not** required by policy. Email address may be multi-valued attributes and include email aliases. |
| Encryption               |Sometimes      | Key Encipherment            | Specific EKUs are required for certificates issued after June 2019            |  rfc822name = email address |  Email address is **not** required by policy. Encryption certificates that represent available, retired encryption key pairs may exist, depending on the PIV issuer. 

Additional useful information:

-   All key pairs for users are 2048-bit (RSA) keys
-   All certificates issued and certified as _PIV_ are SHA-256 signed
-   If you are working with _Common Access Cards_, you may still encounter SHA-1-signed certificates and might _not_ see a Card Authentication certificate
-   There has been testing in some infrastructures to migrate to Elliptic Curve Cryptography (ECC), but there are no ECC certificates for users in production as of the date of this guide
-   There has been testing in some infrastructures to migrate to 3072-bit (RSA) certificates, but there are no 3072-bit certificates for users in production as of the date of this guide

In-depth details on the certificate profiles are contained in the current and historical Federal Public Key Infrastructure (FPKI) policy documents. The most recent policy and certificate profile documents may be found on IDManagement.gov's [Federal Public Key Infrastructure page](https://www.idmanagement.gov/fpki/#certificate-policies){:target="_blank"}.

