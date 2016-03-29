---
layout: page
title: Identifiers in a PIV Credential
permalink: /identifiers/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Advanced</em>
</div>
</div>

In applications, you will need to associate the PIV credential with the local account in the application.  This is not a unique process to PIV credentials and usage.  This is a general concept that occurs in many applications including your personal email accounts, your bank accounts, or your favorite social media app.  The concept is sometimes called _account linking_.

<!-- TODO: Insert note referencing FICAM architecture and designing to a centralized identity and access management model or federated model** -->

#### Identifiers and How to Use
You have two sets of certificates and key pairs that are used for *Authentication*: PIV Authentication, and Card Authentication.  Your PIV Authentication is used for networks and applications.  We focus on the **PIV Authentication** certificate in this section to help you design and implement for these network and applications scenarios.

_Identifiers_ are the values in the certificate that are used for account linking.  The table below outlines identifiers, examples and considerations for implementation.  

| Identifiers              | Location         |  Examples               | Considerations |
| -------------            |:----:            |:----:                   |:----:|
| Subject      |                  |                         | Unique for every person _within the same agency_; Value does not change when a user receives a new, replaced or updated PIV credential _within the same agency_ |
| Issuer and Subject      |                  |                         | Unique for every person; Value does not change when a user receives a new, replaced or updated PIV credential _within the same agency_ |
| Issuer and Serial Number   |                  |                         | Unique for every person and certificate; Value changes when a user receives a new, replaced or updated PIV credential |
| Subject Key Identifier  |                  |                         | Unique for every person and certificate; Value changes when a user receives a new, replaced or updated PIV credential |
| Federal Agency Smartcard Number (FASC-N)      |                  |                         | It is not recommended to use the FASC-N as an identifier; Unique for every credential _only within the US Federal Executive Branch agencies_; No uniqueness for PIV credentials issued by Congressional or Judicial branch agencies, State and Local entities, Partners or any other systems referred to as PIV-Interoperable or PIV-I; Value changes when a user receives a new, replaced, or updated PIV credential; Legacy definition and usage was to support physical (building) access control systems as outlined in [this document](https://www.idmanagement.gov/IDM/servlet/fileField?entityId=ka0t0000000KyuCAAS&field=File__Body__s) |
| Universal Unique Identifer (UUID)      |                  |                         | Unique for every person and credential; Value changes when a user receives a new, replaced or updated PIV credential; May be commonly referred to as the Global Unique Identifier (GUID); UUID is only present in PIV credentials issued after |
| Full Certificate     |                  |                         | Unique for every person and certificate ever; Value changes when a user receives a new, replaced or updated PIV credential |
| _User Principal Name_ (in the Subject Alternative Name)    |                  |                         | Not required to be included in all PIV credentials or PIV Authentication certificates; Not recommended for use as an identifier to achieve full interoperability for networks or applications; Commonly used for enterprise smart card logon / network authentication in legacy implementations |

The full specifications which outline additional details of the data are available in the NIST Special Publication 800-73-4.
