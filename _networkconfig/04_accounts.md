---
layout: default
title: Account Linking
collection: networkconfig
permalink: networkconfig/accounts/
---

For your network domains, you will need to associate the PIV credential to the user accounts.  This is the [account linking]({{site.baseurl}}/identifiers) information discussed in the Identifiers section. The most common questions for US Federal Government and using PIV for network authentication are related to linking a PIV credential to network user accounts.  

This page includes the information on the Identifiers for account linking in network authentication:

- [Comparing Principal Name versus altSecurityIdentities options for the network](#comparing-principal-name-versus-altsecurityidentities-options)
- [Implementing altSecurityIdentities and PIV certificate mapping](#implementing-altsecurityidentities-and-piv-certificate-mapping)


## Comparing Principal Name versus altSecurityIdentities options
There are two attributes in your network domain directories to choose from:

- Principal Name
- altSecurityIdentities - _recommended_

For the Principal Name approach:

- Each PIV credential can only be associated with ONE account
- The User Principal Name value from the _Subject Alternate Name_ in the PIV authentication certificate is required to be populated during PIV credential issuance
- There is no flexibility for associating the PIV credential to separate privileged accounts
- There is less flexibility for accepting PIV credentials issued by other government agencies or partners, including PIV-Interoperable credentials

For the altSecurityIdentities approach:

- Each PIV credential can be associated with MORE THAN ONE account
- Six options from the certificate can be used to map to each account
- This provides flexibility for managing privileged accounts and using one PIV credential to authenticate to more than one account
- Users are presented a second _User Name Hint_ field during network authentication to identify which account the user wants to access
- There is more flexibility for accepting PIV credentials issued by other government agencies or partners, including PIV-Interoperable credentials


{% include alert-info.html heading = "PIV Certificates and UPN values" content="It is not required that you update your PIV credentials and certificates to not have a UPN value populated to use the altSecurityIdentities approach. This is a common misconception due to incorrect information found elsewhere online. If your PIV Authentication certificates do contain a UPN value in the <i>Subject Alternative Name</i> extension, altSecurityIdentities will still work for you, your agency, and your users." %}


## Implementing altSecurityIdentities and PIV certificate mapping

If you have a large network with many domains, you will want to carefully plan for a migration from solely using Principal Name to the altSecurityIdentities approach.  

You may find that you have many applications that rely upon the Principal Name values only.  You can still populate the Principal Name with the PIV Authentication certificate User Principal Name value for one of the user accounts (the non-privileged accounts) to maintain those applications but disable user principal name mapping for _network authentication_.

You have three steps to implement altSecurityIdentities and PIV certificate mapping:

- [Disable User Principal Name Mapping](#disable-user-principal-name-mapping)
- [Link the PIV Authentication Certificate](#link-the-piv-authentication-certificate)
- [Enable User Name Hints](#enable-user-name-hints)

#### Disable User Principal Name Mapping
To implement the altSecurityIdentities approach, you will need to disable _subject alternate name_ for the network domain.  This setting simply tells your network domain: _I don't always want to use the Subject Alternate Name values for my user certificates._

This is a registry setting and you must disable this setting on all domain controllers:

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Kdc
- Change the value of the DWORD UseSubjectAltName to 00000000
- [LINK to External MSDN Article to Disable UPN Mapping](https://technet.microsoft.com/en-us/library/ff520074(WS.10).aspx){:target="_blank"}

Management of registry settings should use group policy objects or other centralized management options,

#### Link the PIV Authentication Certificate
You need to link the PIV Authentication certificate to each of the user's accounts.  You implement this by populating one of the PIV Authentication certificate identifiers to the altSecurityIdentities attribute for each account.

- You have six options from the certificates to use
- A common challenge is determining how the certificate values should be mapped.  A table is shown below with options and example values which closely resemble a production format for PIV Authentication.


| Options       | Tag     | Example | Considerations |
| ------------- |-------------| -----|-----|
| Subject     | X509:\<S> | X509:\<S>C=US,O=U.S. Government,OU=Government Agency,CN=JANE DOE OID.0.9.2342.19200300.100.1.1=25001003151020 |  For certificates which assert the UID identifier (0.9.2342.19200300.100.1.1) or other object identifier in the common name, the identifier is prepended with the _OID_ qualifier. |
| Issuer and Subject     | X509:\<I>\<S>  | X509:\<I>C=US,O=U.S. Government,OU=Certification Authorities,OU=Government Demonstration CA\<S>C=US,O=U.S. Government,OU=Government Agency,CN=JANE DOE OID.0.9.2342.19200300.100.1.1=47001003151020 | Note the spaces carefully when testing and machine readable formats of the certificate extensions versus the human readable formats |
| Issuer and Serial Number | X509:\<I>\<SR> | X509:\<I>C=US,O=U.S. Government,OU=Certification Authorities,OU=Government Demonstration CA\<SR>46a65d49 | Serial number is reversed byte order from human readable version, starting at most significant byte |
| Subject Key Identifier     | X509:\<SKI> |   X509:\<SKI>df2f4b04462a5aba81fec3a42e3b94beb8f2e087 |  Not generally recommended; may be difficult to manage |
| SHA1 hash of public key| X509:\<SHA1-PUKEY> |  X509:\<SHA1-PUKEY>50bf88e67522ab8ce093ce51830ab0bcf8ba7824 |  Not generally recommended; may be difficult to manage   |
| RFC822 name | X509:\<RFC822>      |   Not recommended |    Not recommended; not commonly populated in PIV Authentication certificates |

#### Enable User Name Hints
You need to enable _user name hints_ for your network domain.  This will modify the logon prompts for _Windows_ workstations and servers joined to the network domain.  Your users will be prompted to provide both the PIV credential PIN value and a User Name Hint value.

Username Hint Setting:
  For Windows 2008 R2:
  - _Computer Configuration_ -> _Policies_-> _Administrative Templates_ -> _Windows Components_, and then expand _Smart Card_.
  - Select _Allow user name hint_

  For Windows 2012:
  - _Computer Configuration_ -> _Administrative Templates_ -> _Windows Components_, and then expand _Smart Card_.
  - Select _Allow user name hint_

Management of smart card settings should be deployed using a group policy object for the domain.
