---
layout: default
title: Network Autentication
collection: networkconfig
permalink: networkconfig/network-authen/
---


- [Configure Active Directory and Domain Controller](#configure-active-directory-and-domain-controller)
- [Configure Windows Enterprise Certificate Authority](#configure-windows-enterprise-certificate-authority)
- [Configure Certificate Trusts](#configure-certificate-trusts)

## Configure Active Directory and Domain Controller

Required: Active Directory must have the third-party issuing CA in the NTAuth store to authenticate users to active directory.
Required: Domain controllers must be configured with a domain controller certificate to authenticate smartcard users.
Optional: Active Directory can be configured to distribute the third-party root CA to the trusted root CA store of all domain members using the Group Policy.
Smartcard certificate and workstation requirements

Required: All of the smartcard requirements outlined in the "Configuration Instructions" section must be met, including the text formatting of the fields. Smartcard authentication fails if they are not met.
Required: The smartcard and private key must be installed on the smartcard.


## Configure Windows Enterprise Certificate Authority

The instructions for the NTP / Standalone CA walked thru in our test lab use the openssl standalone CA used to support our local certs. However, smartcard support has very specific requirements for a special â€œDomain Controller Certificateâ€ which is documented at Microsoft KB291010. Unfortunately, the openssl implementation as of this writing (11 FEB 13) does not support the extensions required for the Domain Controller Certificate. Thus, to use CAC authentication requires a Microsoft CA to be installed.

- On a dedicated VM (in our Lab we used a server named CALOCAL001CA) install the Active Directory Certificate Services. Because the external standalone openssl CA is used for all Web server certificates, there is no need for the CA Web Enrollment Role Service; just install the Certificate Authority.

- Run gpupdate /force on the domain controller after installing the CA. This should ensure that Kerberos will function correctly for a smartcard login.

- If you receive Event ID 29 (â€œThe Key Distribution Center (KDC) cannot find a suitable certificate to use for smart card logonsâ€¦â€) then simply open Computer certificates Personal store and select to request a new certificate.

- On the domain controller: open ADSI Edit and right-click the forest to edit Properties. Within properties, add a UPN suffix of â€œmilâ€ (by itself). The CAC certificates all reference a UPN of [edipi]@mil which must exist as a user on the Active Directory.

- OPTIONAL: Within ADUC, create a new OU for CAC users and add CAC logins. Each login will be identified by [edipi]@mil as the login although the Display Name can be anything.
This handles setup on local CA and domain controller.

## Configure Certificate Trusts

For CAC authentication to work, all signing CAs up to the root CA for *each certificate* on the CAC must be trusted. By default on an AGM machine the root DoD CA is trusted (â€œDOD CA-2â€ root). However, the intermediate certificates can be a pain. For example: On a current CAC as of 11 FEB 13, the signing CA is â€œDOD CA-30â€ which is relatively new and was not on many of the domain members. Get down the latest DoD root certs from DISA if necessary!
Follow these steps:

- On one computer within the domain, use the certutil -dspublish -f [cert_file] NtAuthCA command for all necessary intermediate CAs *and* the root CA. Once completed, run gpupdate /force on the local computer and then open regedit to check the value of the HKEY_LOCAL_MACHINE\Software\Microsoft\EnterpriseCertificates\NTAuth\Certificates entry for the certificate thumbprints. (Use the Certificates snapin to get the thumbprints for the DoD certs you mapped.)

- Within the Certificates snapin for the local computer, check both the intermediate CAs as well as the trusted root CAs containers to verify that all the necessary DoD certificates exist.

- IMPORTANT: The CAC has three certs on it, and Windows Logon may use *any* of these three. So be sure to look at the signing chain for each certificate and validate that all CAs are in both the NtAuthCA store (per step #1 above) as well as in the intermediate / root CAs in the Certificates snapin. This is only confusing if you do not remember that â€“ from an OS perspective â€“ all three certificates are exactly alike because all three have the same UPN of [edipi]@mil. Thus, any one of the three could be used for a given login attempt.

- Be sure to check the â€œAllow login from Remote Desktopâ€ security privilege; by default, only Administrators can login via RDP. Check that the CAC user within AD has RDP login privilege.

At this point it should be possible to login to the client box. First try logging in with the AD user [edipi]@mil and a password; if that works then try logging in with CAC. Both should function. 
