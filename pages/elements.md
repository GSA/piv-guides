---
layout: page
title: Elements of a PIV Card
permalink: /elements/
---
Many of the design features and data elements on the PIV card enable enhanced security and privacy when used to verify a claimed identity. The features of the PIV card can be broken out into two main categories: physical card features, including security features and visual card topography, and the data objects stored electronically on the embedded integrated-circuit chip (ICC).  

#### Physical Elements

<table>
<thead><tr><th>Element Type</th><th>Description</th><th>Standard Element</th></tr></thead>
<tr><td>Security Features</td><td>The PIV Card shall contain, at a minimum, one security feature that aids in reducing counterfeiting, is resistant to tampering, and provides visual evidence of tampering attempts.</td><td>Optical varying structures, optical varying inks, laser etching and engraving, holograms, holographic images, watermarks
</td></tr>
<tr><td>Visual Card Topography</td><td>The visual card topography for the PIV card specifies the information that is mandatory and optional and defines a common design for the placement of printed components.</td><td>Front of Card - Photograph, Name, Employee Affiliation, Organizational Affiliation, Expiration Date
<br/>Back of Card - Agency Card Serial Number, Issuer Identification
</td></tr>
</table>

Most applications for the PIV card leverage the logical data elements on the card to perform electronic verification of a claimed identity. These data elements are defined as part of the PIV card data model, outlined in <a href="http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-73-4.pdf">NIST SP 800-73</a>. The PIV card data objects provide graduated levels of identity assurance and allow an agency the opportunity to select appropriate levels of security for applications being accessed with the PIV card. The following elements comprise the mandatory objects of the PIV card data model:

- Card Capability Container: An object that holds data sets and supports minimum capacity for retrieval of the Data Model. The Card Capability Container allows each PIV card to carry the information needed for software to communicate with the card
- Cardholder Unique Identifier (CHUID): A data element used by the card to prove the identity of the cardholder to an external entity. The CHUID includes a 16 byte Global Unique Identifier (GUID), a 25-byte Federal Agency Smart Credential Number (FASC-N), which uniquely identifies each card, expiration date, and issuer digital signature.
- Certificate for PIV Authentication: A certificate used with its associated private key to authenticate the card and the cardholder.
- Cardholder fingerprints: Primary and secondary fingerprint templates stored on the card for performing authentication.
- Security Object: Signed data object that enforces the integrity of unsigned information (and optionally all PIV data objects, excluding digital certificates).

In addition to the mandatory data objects, there are also 28 optional data objects for interoperable use. Of particular note are the optional certificates that further support authentication and expanded uses, including encryption and digital signing. Digital certificates are a primary tool for performing electronic verification for logical access applications and for modernization of physical access applications. 
