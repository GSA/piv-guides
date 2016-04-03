---
layout: page_collection
title: Account Linking
collection: networkconfig
permalink: networkconfig/accounts/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Advanced</em>
</div>
</div>

For your network domains, you will need to associate the PIV credential to the user account(s).  This is not unique to PIV credentials or smartcard logon; it is a general concept that happens in any application even your personal email accounts, your bank accounts, or your favorite social media app.  

In the smartcard and PIV approach, there is a two step process that ensures the credential you are presenting is authenticated (PIV Authentication) and has an identifier in the credential to find one or more accounts to determine authorization.  

1.  **Authentication:** A challenge response using the PIV Authentication key pair and certificate.  You are prompted to enter a PIN code; the PIN is stored only on the PIV credential and is used unlock the private key and prove "something you know".  For the two-factor, the "something you have" **is** the private key stored on your PIV credential.  When the challenge response is successful and the PIV Authentication certificate has been validated as Trusted, then the _authentication_ succeeds.
2.  **Authorization:**  The network domain uses one or more identifiers in the certificate you present to _find_ your account(s) and determine if you are authorized to have access.  

Step 1 is processed by the network domain and components including the PIV credential, the operating systems, domain controllers, and network infrastructure.   For detailed information on how this works in network domains, you can search online for topics such as _PKINIT protocols_ to learn more.

The most common questions for US Federal Government and using PIV for civilian agencies encompass Step 2.  

### Linking a PIV credential to network user account(s)    
There are two attributes for your users in your network domain directories to choose from:

1. User Principal Name (UPN) - _not recommended_
1. altSecurityIdentities - _recommended_

A portion of agencies may be using the User Principal Name (UPN) to associate a PIV Authentication certificate to a user account.  In the User Principal Name approach:

* Each PIV credential can only be associated with ONE account
* The User Principal Name value from the _Subject Alternate Name_ in the PIV authentication certificate is required to be populated during PIV credential issuance
* There is no flexibility for managing privileged accounts
* There is less flexibility for easily and securely accepting PIV credentials issued by other government agencies or partners, including PIV-Interoperable credentials

You will have more flexibility and security in using the altSecurityIdentities mapping options.  In the altSecurityIdentities approach:

* Each PIV credential can be associated with MORE THAN ONE account
* Six options from the certificate can be used to map to each account
* This provides flexibility for managing privileged accounts and using one PIV credential to authenticate to more than one account
* Users are presented a second _User Name Hint_ option to help choose which account the user is trying to access

<!-- #### Associating PIV credentials using altSecurityIdentities
To help you configure and enable User Name Hints and altSecurityIdentities, there is documentation available freely online.  The information provided in this section is to help you with PIV and US Federal government common challenges.

* It is NOT required that you get updated PIV credentials and certificates without a UPN value populated
  * This is a common misconception
  * If your PIV Authentication certificates do contain UPN value in the _Subject Alternative Name_ extension, this method will still work for you, your agency, and your users.   -->

There are three steps to configure altSecurityIdentities for your network domain(s) and users.

1. [Disable UPN Mapping](#disable-upn-mapping)
1. [Map the user PIV Authentication identifier to the altSecurityIdentities attribute for each user account](#map-the-user-piv-authentication-identifier-to-the-altSecurityIdentities-attribute-for-each-user-account)
1. [Enable Username Hints](#enable-username-hints)

#### 1. Disable UPN Mapping  

  * This is a registry setting and you must disable this setting on all domain controllers
     * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Kdc  
     * Change the value of the DWORD UseSubjectAltName to 00000000
     * [Link to the description of the registry setting](https://technet.microsoft.com/en-us/library/ff520074(WS.10).aspx)
  * Management of registry settings should be deployed using group policy objects

#### 2. Map the user PIV Authentication certificate identifier to the altSecurityIdentities attribute for each account

  * You have six options from the certificates to use
  * A common challenge is determining how the certificate values should be mapped.  A table is shown below with options and example values which closely resemble a production format for PIV Authentication.


| Options       | Tag     | Example | Considerations |
| ------------- |-------------| -----|-----|
| Subject     | X509:\<S> | X509:\<S>C=US,O=U.S. Government,OU=Government Agency,CN=JANE DOE OID.0.9.2342.19200300.100.1.1=25001003151020 |  For certificates which assert the UID identifier (0.9.2342.19200300.100.1.1) or other object identifier in the Common Name, the identifier is prepended with the _OID_ qualifier. |
| Issuer and Subject     | X509:\<I>\<S>  | X509:\<I>C=US,O=U.S. Government,OU=Certification Authorities,OU=Government Demonstration CA\<S>C=US,O=U.S. Government,OU=Government Agency,CN=JANE DOE OID.0.9.2342.19200300.100.1.1=47001003151020 | Note the spaces carefully when testing and machine readable formats of the certificate extensions versus the human readable formats |
| Issuer and Serial Number | X509:\<I>\<SR> | X509:\<I>C=US,O=U.S. Government,OU=Certification Authorities,OU=Government Demonstration CA\<SR>46a65d49 | Serial number is reversed byte order from human readable version, starting at most significant byte |
| Subject Key Identifier     | X509:\<SKI> |   X509:\<SKI>df2f4b04462a5aba81fec3a42e3b94beb8f2e087 |  Not generally recommended; may be difficult to manage |
| SHA1 hash of public key| X509:\<SHA1-PUKEY> |  X509:\<SHA1-PUKEY>50bf88e67522ab8ce093ce51830ab0bcf8ba7824 |  Not generally recommended; may be difficult to manage   |
| RFC822 name | X509:\<RFC822>      |   Not recommended |    Not recommended; not commonly populated in PIV Authentication certificates |


#### 3. Enable Username Hints
Enabling username hints will modify the logon prompts for _Windows_ workstations and servers joined to the network domain.  You will be prompted to provide both your PIN value and a Username Hint value.  

* Management of smart card settings should be deployed using a group policy object for the domain(s)
* Username Hint setting:
   * _Computer Configuration_ -> _Policies_-> _Administrative Templates_ -> _Windows Components_, and then expand _Smart Card_.
   * Double-click _Allow user name hint_
