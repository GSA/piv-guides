---
layout: page
title: Details of a PIV Credential
permalink: /details/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Advanced</em>
</div>
</div>


This section will help you learn how to view the data stored on the PIV credential and information about the certificates, In this section, we focus on the simple methods for:  

1.  [Viewing your certificates on the PIV credential using a traditional computer](#viewing-your-piv-credential),  
<!-- TODO 1.  [Exporting PIV certificates to use in troubleshooting](#exporting-piv-certificates),    -->
1.  [Understanding the PIV Certificates](#understanding-piv-certificates-and-examples).    


#### Viewing your PIV Credential  
Almost **all** the methods for using your PIV credential for networks, applications, digital signatures and encryption is using the certificates and key pairs stored on your PIV credential. However, there are scenarios where the additional information such as biometrics are accessed and used. _We will cover how to view the information for these additional scenarios and for developers in a set of Developer Guides._  

The easiest methods to view your certificate information is:

* Insert your PIV credential in your card reader.

* Choose an option from the table below and follow the steps.

| Operating System     | Module   | Steps |
| -------------             |----|----|
| Microsoft   | Internet Explorer Browser or Edge Browser  | Open _Internet Explorer Browser_ -> _Settings_ -> _Internet Options_ -> Choose _Content_ tab -> _Certificates_ -> Choose _Personal_ tab   |
| Microsoft       | Microsoft Management Console (MMC) and Certificate Snap-in  |  Open _Microsoft Management Console_ -> _File_ -> _Add/Remove Snap-In_ -> Select _Certificates_ snap-in -> _Add_ -> _My user account_ -> _Finish_ -> Expand _Certificates - Current User_ -> Select _Personal_ -> Select _Certificates_   |
| Any   | Chrome Browser  | Open _Settings_ -> _Show Advanced Settings_ -> HTTPS / SSL: _Manage Certificates_ -> Choose the _Your Certificates_ tab  |
| Any   | Firefox Browser  | Open _Menu_ -> _Preferences_ -> _Advanced_ -> Choose _Certificates_ tab -> _View Certificates_ -> Choose the _Your Certificates_ tab|
| MacOS X   | Key Chain  | Open _Applications_ -> _Utilities_ -> _Keychain Access_ -> Select _Login_ -> From Categories, select _My Certificates_  |

* You may see many certificates.  To open and view the certificate details, double-click on any certificate.

<!-- TODO
#### Exporting PIV Certificates
We won't always be using graphical user interfaces to view the PIV credential certificates.  Throughout the guides, examples are provided of code, tools and common _command line_ options for viewing and troubleshooting configurations.  The examples may use files representing the _public_ certificate(s).    

Don't worry - the public certificates are _public_.  The private keys are still stored safely on your PIV credential and can't be exported.   -->


#### Understanding PIV Certificates
Viewing the certificate information on your PIV credential may be interesting if you are a general user.  **Understanding** the certificate information is a **must** if you are a program manager, developer or engineer working on supporting, developing applications, and designing solutions for using PIV credentials.

Within the US Federal Government, the certificate information and the PIV credential information is governed by Standards, Policies, and implementation specific choices (options) across all agency credential providers.     

**We present the common information in this section with special emphasis on what is true for ALL PIV credentials and certificates issued within the past six years.**  

There are four sets of certificates and key pairs on a PIV credential.  Two sets are *ALWAYS* on every PIV credential and two sets are *SOMETIMES* on a PIV credential.  You can review [the basics of a PIV Credential](../elements/) to view the four sets and purposes.  

The table below outlines the general information for the PIV credential certificates, certificate extensions, and design considerations.  All information is presented in human-readable formats.    

| Certificate              | Required  | Key Usage  |  Extended Key Usage  | Subject Alternative Name | Considerations |
| -------------            |:----:      |:----:               |:----:               |:----:|  ----|
| PIV Authentication       |Always      | Digital Signature            | Client Authentication           | otherName = FASC-N; uniformResourceIdentifier = UUID; Principal Name = _prefix_@_suffix_  | Principal Name values are **not** required by Policy to be present in all Subject Alternative Name extensions.  The UUID value is only required to be present for certificates issued on October 15, 2015 or later.  |
| Card Authentication      |Always      | Digital Signature            | id-PIV-cardAuth            |  otherName = FASC-N; uniformResourceIdentifier = UUID|   The UUID value is only required to be present for certificates issued on October 15, 2015 or later. |
| Digital Signature        |Sometimes      | Digital Signature, Non-Repudiation            | _none required_            |  rfc822name = email address | Email address is **not** required by Policy. Email address may be multi-valued attributes and include email aliases. |
| Encryption               |Sometimes      | Key Encipherment            | _none required_            |  rfc822name = email address |  Email address is **not** required by Policy. Multiple encryption certificates may be available representing the historical encryption key pairs available. |

Additional useful information:

*  All key pairs are 2048 bit (RSA) keys  
*  All certificates issued and certified as _PIV_ are SHA-2 signed  
   *  If you are working with _Common Access Cards_, you may still encounter SHA-1 signed  
*  There has been testing in some infrastructures to migrate to Elliptic Curve Cryptography (ECC), but there are no ECC certificates in production as of the date of this guide  
*  There has been testing in some infrastructures for migration to 3072 bit (RSA) certificates, but there are no 3072 bit certificates in production as of the date of this guide  

In-depth details on the certificate profiles are contained in the current and historical Federal Public Key Infrastructure (FPKI) Policy documents.  The table below contains links to the most recent documents:

| Certificates    | Policy Update Date  | Link to Profile Information|
| -------------            |:----:               |:----:|
| PIV Certificates           | May 5, 2015             | [Worksheets 5, 6, 8 and 9 in this document](https://www.idmanagement.gov/IDM/servlet/fileField?entityId=ka0t0000000TNP2AAO&field=File__Body__s)|
| PIV _Interoperable_ Certificates           | May 5, 2015             | [Worksheets 4, 5, 6, and 7 in this document](https://www.idmanagement.gov/IDM/servlet/fileField?entityId=ka0t0000000TN9YAAW&field=File__Body__s)|
