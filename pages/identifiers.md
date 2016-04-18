---
layout: default
title: Identifiers in a PIV Credential
permalink: /identifiers/
---

<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Advanced</em>
</div>
</div>

In applications including network domains, you will associate the PIV credential with your accounts.  This is not a unique process to PIV credentials and usage, and is a general concept that occurs in many applications including your personal email accounts, your bank accounts, or your favorite social media app.  Associating a credential with an account is called _account linking_.

_Identifiers_ are the values in credentials that are used for account linking.  We focus on the **PIV Authentication** certificate and identifiers in this section to help you understand the options, and design and implement for using PIV to authenticate to networks and applications.

<!-- TODO: Insert note referencing FICAM architecture and designing to a centralized identity and access management model or federated model** -->

The table below outlines identifiers available in the PIV Authentication certificate and design considerations for implementations.

| Identifiers              | Considerations |
| -------------            |----            |----                   |----|
| Subject      |  Unique for every person _within the same agency_; Value does not change when a user receives a new, replaced or updated PIV credential _within the same agency_ |
| Issuer and Subject      | Unique for every person; Value does not change when a user receives a new, replaced or updated PIV credential _within the same agency_ |
| Issuer and Serial Number   | Unique for every person and certificate; Value changes when a user receives a new, replaced or updated PIV credential |
| Subject Key Identifier  | Unique for every person and certificate; Value changes when a user receives a new, replaced or updated PIV credential |
| Federal Agency Smartcard Number (FASC-N)   | It is not recommended to use the FASC-N as an identifier; Unique for every credential _only within the US Federal Executive branch agencies_; No uniqueness for PIV credentials issued by Legislative or Judicial branch agencies, State, Local, Tribal, Territories, Partners or any credentials certified as PIV-Interoperable or _PIV-I_; Value changes when a user receives a new, replaced, or updated PIV credential; Legacy definition and usage was to support building access control systems as outlined in [this document](https://www.idmanagement.gov/IDM/servlet/fileField?entityId=ka0t0000000KyuCAAS&field=File__Body__s) |
| Card Universal Unique Identifier (UUID)      |   Unique for every person and credential; Value changes when a user receives a new, replaced or updated PIV credential; May be commonly referred to as the Global Unique Identifier (GUID); Card UUID is only required in PIV Authentication certificates issued after May 2015 |
| User Principal Name in _Subject Alternate Name_   |  Not required to be included in all PIV Authentication certificates; Not recommended for use as an identifier to achieve full interoperability for networks or applications; Commonly used for enterprise smart card logon / network authentication in _legacy_ implementations |
