---
layout: default
title: Identifiers in a PIV Credential
permalink: /identifiers/
---

In applications, including those within network domains, you will associate PIV credentials with your accounts.  This is not a unique process to PIV credentials and their use. It is a general concept that occurs with many applications and authenticators. For example, you could associate a Fast IDentity Online (FIDO) authenticator with your personal email account or favorite social media app.

{% include alert-info.html content="Associating a credential with an account is called Account Linking." %}

_Identifiers_ are the values in credentials that are used for account linking.  We focus on the **PIV Authentication** certificate and identifiers in this section to help you understand the options and to design and implement for using PIV credentials to authenticate to networks and applications.

This table outlines identifiers available in the PIV Authentication certificate and design considerations for implementations.

| Identifiers              | Considerations |
| -------------            |----            |
| Subject      |  Unique for every person _within the same agency_.<sup>[1](#1)</sup> Value does not change when a user receives a new, replaced, or updated PIV credential _within the same agency_. |
| Issuer and Subject      | Unique for every person. Values do not _normally_ change when a user receives a new, replaced, or updated PIV credential _within the same agency_; however, when a Certification Authority changes, the Issuer may change too. |
| Issuer and Serial Number   | Unique for every person and certificate. Values change when a user receives a new, replaced, or updated PIV credential. |
| Subject Key Identifier  | Unique for every person and certificate. Value changes when a user receives a new, replaced, or updated PIV credential. _Subject Key Identifier_ is the SHA-1 hash of the certificate's public key. |
| SHA-1 Hash of Public Key  | Value changes when a user receives a new, replaced, or updated PIV credential. The SHA-1 hash of the certificate's public key is commonly referred to as the certificate's _thumbprint_.  |
| Federal Agency Smartcard Number (FASC-N)   | Using the FASC-N as an identifier is not recommended; however, [NIST SP 800-116, Revision 1](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-116r1.pdf){:target="_blank"} (June 2018) considers the FASC-N normative for physical access control systems and it may still support legacy definitions, as outlined in [this document](https://www.idmanagement.gov/wp-content/uploads/sites/1171/uploads/TIG_SCEPACS_v2.3.pdf){:target="_blank"}. The FASC-N is _unique_ for those credentials issued _only within the U.S. Federal Executive branch agencies_.  It is _not unique_ for PIV credentials issued by Legislative or Judicial branch agencies; State, Local, Tribal, Territories; or Partners or for those credentials certified as PIV-Interoperable (_PIV-I_). Value changes when a user receives a new, replaced, or updated PIV credential. |
| Card Universal Unique Identifier (UUID)      |   Unique for every person and credential. Value changes when a user receives a new, replaced, or updated PIV credential. The Card UUID value must be present for new or replacement PIV credentials issued after August 2014. The Card UUID is also commonly referred to as the _Global Unique Identifier (GUID)_. |
| User Principal Name (UPN) in _Subject Alternate Name_   |  Not required to be included in all PIV Authentication certificates. Using the UPN in the Subject Alternate Name as an identifier is not recommended to achieve full interoperability for networks or applications. The UPN is commonly used for enterprise smart card logon/network authentication in _legacy_ implementations |

--------
<a name="1">1</a>. For all _agency_ references above, consider these to connote a _small component within an agency_.  For example, a user who switches between one small component in a large agency to another small component may actually be given a _new Subject name_ when the user requires a replacement PIV credential.<br>
