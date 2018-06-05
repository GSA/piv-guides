---
layout: default
title: Identifiers in a PIV Credential
permalink: /identifiers/
---

In applications including network domains, you will associate the PIV credential with your accounts.  This is not a unique process to PIV credentials and usage, and is a general concept that occurs in many applications including your personal email accounts, your bank accounts, or your favorite social media app.  
{% include alert-info.html content="Associating a credential with an account is called Account Linking." %}

_Identifiers_ are the values in credentials that are used for account linking.  We focus on the **PIV Authentication** certificate and identifiers in this section to help you understand the options, and design and implement for using PIV to authenticate to networks and applications.

The table below outlines identifiers available in the PIV Authentication certificate and design considerations for implementations.

| Identifiers              | Considerations |
| -------------            |----            |----                   |----|
| Subject      |  Unique for every person _within the same agency_; Value does not change when a user receives a new, replaced or updated PIV credential _within the same agency_ |
| Issuer and Subject      | Unique for every person; Value does not change when a user receives a new, replaced or updated PIV credential _within the same agency_ |
| Issuer and Serial Number   | Unique for every person and certificate; Value changes when a user receives a new, replaced or updated PIV credential |
| Subject Key Identifier  | Unique for every person and certificate; Value changes when a user receives a new, replaced or updated PIV credential |
| SHA-1 Hash of Public Key  | Value changes when a user receives a new, replaced, or updated PIV credential; Commonly referred to as the thumbprint of the certificate |
| Federal Agency Smartcard Number (FASC-N)   | It is not recommended to use the FASC-N as an identifier; Unique for every credential _only within the US Federal Executive branch agencies_; No uniqueness for PIV credentials issued by Legislative or Judicial branch agencies, State, Local, Tribal, Territories, Partners or any credentials certified as PIV-Interoperable or _PIV-I_; Value changes when a user receives a new, replaced, or updated PIV credential; Legacy definition and usage was to support building access control systems as outlined in [this document](https://www.idmanagement.gov/wp-content/uploads/sites/1171/uploads//TIG_SCEPACS_v2.2_0.pdf){:target="_blank"} |
| Card Universal Unique Identifier (UUID)      |   Unique for every person and credential; Value changes when a user receives a new, replaced or updated PIV credential; Card UUID value is only required to be present for new or replacement PIV credentials issued after August 2014; May also commonly be referred to as the Global Unique Identifier (GUID). |
| User Principal Name in _Subject Alternate Name_   |  Not required to be included in all PIV Authentication certificates; Not recommended for use as an identifier to achieve full interoperability for networks or applications; Commonly used for enterprise smart card logon / network authentication in _legacy_ implementations |

For all items referencing an _agency_ in the table, you should consider the reference as the small organizational unit.  For example, a user who switches between one component in a large agency to another component may receive a new Subject name when the user requires a replacement PIV credential.
