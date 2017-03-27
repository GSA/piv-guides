---
layout: page
title: Locally Trusted OCSP Configuration
permalink: /Locally Trusted OCSP Configuration/
---

# Locally Trusted OCSP Configuration

#### Table of Contents
#### [Introduction](#Introduction-1)
#### [Security Risks](#Security-Risks-1)
#### [Prerequisites](#Prerequisites-1)
#### [Install Microsoft OCSP Responder](#Install-Microsoft-OCSP-Responder-1)
#### [Windows Client Configuration](#Windows-Client-Configuration-1)
#### [End-to-End Testing](#End-to-End-Testing-1)

----------

## Introduction
In Public Key Infrastructure (PKI), Online Certificate Status Protocol (OCSP) is functionally a replacement for  Certificate Revocation Lists (CRLs). An OCSP response, like a CRL, provides the revocation status of a certificate. That is, it tells you whether a given certificate has been revoked by its issuer. If you rely on certificate status provided by external, Internet hosted sources for critical functionality within your local network, it may make sense to ensure availability by creating a locally hosted (and locally trusted) copy of critical revocation status information using a locally trusted OCSP responder. Hosting this service locally can ensure clients will operate normally in the event of Internet disruptions, outages, or problems related to the remote hosting of CRLs/OCSP.

Another important observation is that once configured, mobile clients such as laptops, tablets, and phones can leverage the locally trusted service even when remote, i.e. over the Internet, if the OCSP responder is exposed to the Internet. Given that clients should be able to fail over to the next revocation status source as necessary, this additional revocation source can add additional resiliency for your users both on and off the local network. If you wish to leverage this or possibly in the future, it is recommended that you choose a server name that can be associated with an Internet address.

## Security Risks
By operating a locally trusted OCSP responder, you are assuming all risks introduced by not depending directly on the authoritative revocation status sources. Certification Authorities (CAs) follow stringent requirements involving the multi-person control, extensive physical security, and hardware cryptographic modules. These policies and procedures are detailed in each CA's Certificate Policy (CP) and Certification Practices Statement (CPS).  If you do not implement equivalent security controls, then your local OCSP responder becomes the weak link in the chain; the overall assurance level should effectively be reduced to that of your local configuration. For example, if you are validating PIV authentication certificates (hardware), but you are using software cryptographic keys on your local OCSP responder, then the assurance level of the validated certificates may be viewed as software assurance rather than hardware. This may be perfectly acceptable for some use cases while for others it is not. This is a local risk decision that should receive careful consideration and shape your deployment design.

A locally trusted OCSP Responder should never be trusted by any clients that are not explicitly configured to trust it. Therefore, the CA you use should by private to your organization. The CA and issued OCSP Responder certificates should not be trusted outside of your intended pool of clients for any purposes. 

A common misunderstanding is viewing an OCSP check is the same thing as certificate validation - this is a dangerous and completely inaccurate assumption. The proper procedures for certificate path validation can be found in section 6 of [RFC 5280](https://www.ietf.org/rfc/rfc5280.txt).

## Prerequisites
#### Required
 - A locally trusted CA to issue OCSP responder certificates
 - Windows 2012 R2 server

Owing to its' limited, local only, scope and special requirements on its' content, it is recommended that a new, dedicated Root CA be used for issuing the locally trusted responder certificates. Some additional details can be found in the procedures below and in [Appendix 2 - Using Microsoft CA as the self signed root](#Appendix-2---Using-Microsoft-CA-as-the-self-signed-root-1)

#### Recommended:
 - Hardware Security Module (HSM)
 - Certificate Policy (CP) and Certification Practices Statement (CPS):  Documented security policies and procedures for deployment and operation OCSP responder certificate issuing CA and the OCSP responder(s).
	 - Recommend leveraging one or more relevant CP(s) published by a CA(s) you rely on for requirements.

> <i class="icon-info"></i>  CA installation, HSM configuration, and policy documents are not covered in detail by this document.

Before you begin, it is recommended that you review the [Implementing an OCSP responder](https://blogs.technet.microsoft.com/askds/2009/06/24/implementing-an-ocsp-responder-part-i-introducing-ocsp/) series on Microsoft TechNet. These documents include supporting information that has been omitted from this document.

## Install Microsoft OCSP Responder
Microsoft Windows Server 2012 R2 was chosen for inclusion in this document because it is generally available across Federal agencies. Please note that other products may be configured to provide locally trusted service and until such time as additional guidance is available you are encouraged to speak directly with these product vendors regarding configuration. 

### Software Installation
Before beginning the installation, ensure your server is named and joined to the appropriate domain. Changing the server name or domain after installation can corrupt the configuration. Your server will also need outbound Internet access to download remote CRLs. In most cases, CRLs are available over HTTP/80.

Use the *Add Roles and Features Wizard* to add the *Active Directory Certificate Services* (ADCS) role to Windows 2012 R2.

![Select Active Directory Certificate Services (ADCS)](../img/local-ocsp-cfg-adcs.png)

The wizard will prompt you add required features, add them, and then continue through the wizard until you reach *Role Services*. At this point, ensure you remove Certification Authority, and add Online Responder.

![Select Online Responder](../img/local-ocsp-cfg-role-services2.png)

The wizard will prompt you to *Add features that are required for Online Responder*, click *Add features*, then continue with the wizard and click *Install*. After the wizard finishes installing, click *Configure Active Directory Certificate Services on the destination server* inside the Results window.

![Click Configure Active Directory Certificate Services](../img/local-ocsp-cfg-configure.png)

Assuming you are logged on the the server with (at least) local administrator rights, it is not be necessary to change the credentials in the *AD CS Configuration* wizard. Click through the wizard, click *Configure* then *Close* when it finishes. You can now close the *Add Roles and Features Wizard*. As a best practice, you may wish to reboot the server before continuing.

### Obtain OCSP Responder Certificate

There are primarily two different approaches for obtaining certificates for the Microsoft OCSP Responder implementation. In one approach, the Online Responder has permissions to automatically request certificates from an online Microsoft CA on the same domain. If done in a dedicated, network isolated domain with hardware security modules, this approach can be relatively secure. The other option, which is described to a an extent below, is to manually install a certificate which you obtain from an offline CA.

> <i class="icon-info"></i>  Regardless of the certificate issuance approach, Windows clients require every certificate in the chain, *including the self signed root*, to express OCSP Signing (1.3.6.1.5.5.7.3.9) in the Extended Key Usage extension.

The first step is to generate a new signing key and certificate request file. You will need to create an INF file that specifies the details to include in the request. See [Appendix 1 - Sample OCSP INF file](#Appendix-1---Sample-OCSP-INF-file-1) for an example. Once you've created your INF file, open an administrative command window on the server and use the following command:

	certreq -new <inf_filename>.inf ocsp.req

This command should generate a new signing key and output a signed certificate request to *ocsp.req*.  Deliver this request file to your CA and obtain your OCSP Responder certificate. Note that this file is PEM encoded - you can open it in notepad and copy/paste the content.

After obtaining your new certificate, ensure it meets the requirements of an OCSP Responder certificate before proceeding:

- OCSP Signing (1.3.6.1.5.5.7.3.9) in the Extended Key Usage
	- This *should* be marked critical
- The id-pkix-ocsp-nocheck (1.3.6.1.5.5.7.48.1.5) extension is present
	- including this prevents clients from checking the OCSP Responder certificates revocation status
- Key Usage must contain Digital Signature (80)
	- This *should* be marked critical
- The Subject Alternative Name *should* contain DNS Name = OCSP Server DNS name

### Install OCSP Responder Certificate
Copy the new certificate as well as the issuing CA certificate (or chain) to the OCSP Responder server. If you haven't already done so, install the issuing CA root certificate in the **Computer** Trust Root Certification Authorities store. Use the following command to accept the OCSP Responder certificate:

	certreq -accept <ocsp_responder_certificate_filename>.cer

When successful, certreq will exit and provide no feedback.

> <i class="icon-info"></i>  An error message stating "*Certificate Request Processor: A certificate chain could not be built to a trusted root authority. 0x800b010a (-2146762486 CERT_E_CHAINING)*" indicates the self signed root (and intermediate CA certificates, if applicable) are not available or not in the correct certificate stores on the server. Ensure the required CA certificates are imported to the correct *Computer account* stores.

To confirm the certificate was properly imported, open mmc.exe, load the Certificates snap-in, and target it to the Computer Account. Expand the Personal->Certificates tree and confirm the newly accepted certificate is listed there.

![Locate OCSP Responder Certificate in MMC](../img/local-ocsp-cfg-mmc.png)

Double click the certificate and confirm it appears valid, lists *OCSP Signing* under purpose(s), and indicates *You have a private key that corresponds to this certificate*. Close the certificate.

![Locate OCSP Responder Certificate in MMC](../img/local-ocsp-cfg-cert-key.png)

Right click the certificiate in MMC and select All Tasks -> Manage Private Keys

![Manage Private Keys in MMC](../img/local-ocsp-cfg-manage-private-keys.png)

When the permissions dialog appears, click the Add button.

![Default Private Key Permissions](../img/local-ocsp-cfg-default-permissions.png)

If this server is on a domain, click Locations and select the local server. Type "NETWORK SERVICE" into the object names box. Click Check Names and OK when finished.

![Add NETWORK SERVICE Permissions](../img/local-ocsp-cfg-add-network-service.png)

With NETWORK SERVICE selected, clear the check mark from *Full control* then click OK.

![Allow only Read for NETWORK SERVICE](../img/local-ocsp-cfg-read-only-rights.png)

The certificate and private key should now be usable by the OCSP Responder service.

### Configure Revocation Sources
Every issuing and intermediate CA certificate to be supported by the OCSP Responder must have their own entry in "Revocation Configuration"  You can allow the OCSP Responder to automatically schedule CRL downloads (default) or specify intervals at which the CRL should be downloaded.

> **tbd / need to test how the default crl validity period refresh option works and does configuring an interval always download on the interval or checks for a changed file?**

#### Manually Adding a Revocation Source
In the example images below, the Federal Bridge CA 2016 is added as a revocation source.

Open the Online Responder Management console, right click Revocation Configuration, then select Add Revocation Configuration.

![Add Revocation Configuration](../img/local-ocsp-cfg-add-revocation-configuration.png)

Click Next to Name the Revocation Configuration. It is recommended that you always use the common name of the CA plus any other identifying information that may be necessary. Click Next.

![Name the Revocation Configuration](../img/local-ocsp-cfg-add-rev-conf-1.png)

> <i class="icon-info"></i>  You will need to configure separate Revocation Configurations for CAs that have more than one key pair. Name your Revocation Sources such that you can easily identify these cases.

On the next step, you can choose either Local certificate store or from a File. Click Next, select the CA certificate, then click Next again.

![Select Import From File](../img/local-ocsp-cfg-add-rev-conf-2.png)

Select Manually select a signing certificate, then click Next.

![Select Manual Signing Certificate](../img/local-ocsp-cfg-add-rev-conf-4.png)

An error will appear complaining that you have not yet configured the revocation provider settings. Click OK.

![Revocation Provider Error Message](../img/local-ocsp-cfg-add-rev-conf-5.png)

Click the Provider button to open the Revocation Provider Properties dialog.

![Click the Provider Button](../img/local-ocsp-cfg-add-rev-conf-6.png)

Click Add then copy and paste the CA's CRL distribution point URL into the edit field. Click OK to return to the Revocation Provider Properties dialog.

![Enter the CRL DP URL](../img/local-ocsp-cfg-add-rev-conf-7.png)

If you are unsure how to configure refresh interval, leave the Refresh CRLs based on their validity periods selected. Otherwise, clear that check box and enter the desired interval. Click OK.

![Configure the CRL update internal](../img/local-ocsp-cfg-add-rev-conf-8.png)

After completing the above steps, you will need to assign the OCSP Responder Certificate to the configuration. Until this is done, you will "Signing Certificate: &nbsp;Not Found" listed in the Status panel for this Revocation Configuration:

![OCSP Signing Certificate Not Found](../img/local-ocsp-cfg-signing-certificate-not-found.png)

Right click on the Revocation Configuration Name, then select Assign Signing Certificate

![Assign OCSP Signing Certificate](../img/local-ocsp-cfg-assign-signing-certificate.png)

A dialog will appear allowing you to select the OCSP Responder certificate. Click the correct certificate and click OK.

![Select Signing Certificate](../img/local-ocsp-select-signing-certificate.png)

After selecting the certificate, you will notice that the statu panel still displays an error stating *The data necessary to complete this operation is not yet available." What this really means is it hasn't yet downloaded the CRL.

![CRL not yet downloaded](../img/local-ocsp-crl-not-downloaded.png)

After waiting a few minutes, simple right click Array Configuration and select Refresh.

![Refresh](../img/local-ocsp-cfg-refresh.png)

At this point, the CRL should have been automatically downloaded and your status panel should look like the below example.

![OCSP Revocation Configuration working correctly](../img/local-ocsp-cfg-working-correctly.png)

Repeat this process for every CA you want to add to the OCSP Responder.

#### Using PowerShell to Add a Revocation Source

	include code sample

## Windows Client Configuration 

### Manual Client Configuration
A locally trusted OCSP Responder is configured using the Certificates Snap-In in Microsoft Management Console. To begin, open MMC (mmc.exe)  and add the Certificates Snap-In for the Local Computer Account.

![MMC Certificates Snap-In](../img/local-ocsp-client-1.png)

Navigate to the certificate store and CA certificate for which you want to enable locally trusted OCSP, then right click the certificate and select Properties.

![Select certificate properties in MMC](../img/local-ocsp-client-2.png)

Click the OCSP tab, then enter the URL of your locally trusted OCSP Responder. Click the adjacent Add URL button. 

![Add a custom OCSP URL](../img/local-ocsp-client-3.png)

Confirm the URL appears in the list.

![Custom OCSP URL added to certificate properties](../img/local-ocsp-client-4.png)

> <i class="icon-info"></i>  You can configure multiple OCSP Responder URLs

Click OK when satisfied with your modifications. All applications that leverage Windows certificate validation APIs will now attempt to use your configured OCSP Responder when validating certificates *issued* by this CA.


### Group Policy Configuration
group policy editor

## End-to-End Testing

### Windows certutil
Use certutil and CAPI 2 event logging to test and debug operation

### Common problems and solutions
Event log entries, what they means, how to fix them


## Appendix 1 - Sample OCSP INF file
Below INF file is an example of the configuration file you can use to generate a new certificate signing request for your OCSP Responder.

 - Customize the Subject field in keeping with your Issuing CAs name
	 - The example below could be submitted to CA "CN=OCSP Issuing CA,DC=agency,DC=local"
 - Ensure KeyLength is set in keeping with the CA key sizes for which you intend to provide OCSP responses
 - If you are using an HSM, the ProviderName will need to be modified appropriately per the HSM documentation

Sample CaPolicy.inf :

	[NewRequest]
	Subject = "CN=Local OCSP Server,DC=agency,DC=local"
	PrivateKeyArchive = FALSE
	UserProtected = FALSE
	MachineKeySet = TRUE
	ProviderName = "Microsoft Enhanced Cryptographic Provider v1.0"
	UseExistingKeySet = FALSE
	KeyLength = 2048
	RequestType = PKCS10
	
	[EnhancedKeyUsageExtension]
	OID="1.3.6.1.5.5.7.3.9"
	
	[Extensions]
	; id-pkix-ocsp-nocheck
	1.3.6.1.5.5.7.48.1.5 = "{hex}05 00"
	; the following is only needed if submitting to a CA that has multiple keys
	; uncomment and set the example hex string to the Subject Key ID of the CA
	; 2.5.29.35="{hex}30 16 80 86441F15A89DA7CA3F09F643FFE31EE9C6FC0CD6"
	
	[ApplicationPolicyStatementExtension]
	Policies = OCSPSigning
	Critical = FALSE
	
	[OCSPSigning]
	OID = 1.3.6.1.5.5.7.3.9



## Appendix 2 - Using Microsoft CA as the self signed root

Prior to configuring Certificate Services and generating the new Root CA key pair, the below CaPolicy.inf file should be placed in %SYSTEMROOT%.  Below will create a self signing root certificate with a 2048 bit RSA key and a ten year validity period with OCSP Signing (1.3.6.1.5.5.7.3.9) in the Extended Key Usage extension. 

	[Version]
	Signature="$Windows NT$"

	[AuthorityInformationAccess]
	; This extension will be omitted

	[CRLDistributionPoint]
	; This extension will be omitted

	[Extensions]
	; Key Usage = CertSign & CrlSign
	2.5.29.15=AwIBBg==
	Critical=2.5.29.15 

	[EnhancedKeyUsageExtension]
	OID=1.3.6.1.5.5.7.3.9 	; ocsp signing
	Critical=No

	[certsrv_server]
	LoadDefaultTemplates=0
	RenewalKeyLength=2048
	RenewalValidityPeriod=Years
	RenewalValidityPeriodUnits=10

	[BasicConstraintsExtension]
	PathLength=0
	Critical=True

> <i class="icon-info"></i>  When configuring a new CA, the setup wizard may default to using 2048 bit RSA with SHA1. At a minimum, this should be changed to 2048 bit RSA with SHA256.

Prior to issuing OCSP Responder Certificates, you must enable the OCSP-No-Check extension using the following commands:

	certutil -v -setreg policy\EnableRequestExtensionList +1.3.6.1.5.5.7.48.1.5
	-or-
	certutil -v -setreg policy\editflags +EDITF_ENABLEOCSPREVNOCHECK
	
	net stop certsvc
	net start certsvc

If this CA is dedicated to issuing OCSP responder certificates, you may also wish to disable the CDP and AIA extensions inside the Certification Authority MMC Snap-In. Simply uncheck the "Include in the CDP/AIA extension of issued certificates" boxes for each URL in the Extensions tab. These extensions are not needed by the OCSP clients and removal improves efficiency.
