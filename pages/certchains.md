---
layout: default
title: Certificate Trust
permalink: /pivcertchains/
redirect_to: https://playbooks.idmanagement.gov/piv/cert-trust/
---

One of the most common questions is "What are all these certificates and how do I configure my applications to use them?"  Answering this question involves explaining trust, certificate chains and revocation.  

- [Trust](#trust)
- [Certificate *chains*](#certificate-chains)
- [Revocation](#revocation)

If you are looking for the root certificates, you can quickly jump to the end of the page for instructions!

- [Download root and intermediate certificates](#download-root-and-intermediate-certificates)


## Trust
Identity certificates are issued and digitally signed by a _certification authority_.  The _certification authority_ that signed your PIV certificates is called an _**intermediate** certification authority_ because it was issued a certificate by another _certification authority_.  This process of issuing and signing continues until there is one  _certification authority_ that is called the _**root** certification authority_.

The full process of proving identity when issuing the certificates, auditing the certification authorities, and the cryptographic protections of the digital signatures establish the basis of Trust for PIV credentials and certificates.

![Example of an identity certificate with intermediate and root]({{site.baseurl}}/img/certificatechain_small.png){:style="float:center"}

For the US Federal Government Executive branch agencies, there is one root certification authority named _Federal Common Policy Certification Authority (COMMON)_, and dozens of intermediate certification Authorities.  The US Federal Government has also established trust with other certification authorities which serve business communities, State and Local government communities, and international government communities.

* [FPKI GRAPH: A graph of the federal public key infrastructure, including the business communities](https://fpki.idmanagement.gov/tools/fpkigraph/){:target="_blank"}
* [PIV CAs and Agenices: A list of the certification authorities currently used to issue Personal Identity Verification (PIV) authentication certificates for federal government departments and agencies.](https://fpki.idmanagement.gov/crls/pivcas/){:target="_blank"}

The participating certification authorities and the policies, processes, and auditing is referred to as the [*Federal Public Key Infrastructure (FPKI)*](https://www.idmanagement.gov/topics/fpki/){:target="_blank"}

## Certificate Chains
To digitally trust YOU and your PIV credential certificates, the workstations, servers, applications and network domains will be configured. Understanding and managing certificate chains are one of the methods to configure trust.

The certificate chain includes intermediate certification authority certificates and the Federal Common Policy Certification Authority (COMMON) root certificate.

![Example of a PIV certificate chain to Common]({{site.baseurl}}/img/pivcertificatechain_small.png){:style="float:center"}


{% include alert-info.html heading = "Federal PKI Person Root - COMMON" content="The current Federal Common Policy Certification Authority (COMMON) root certificate is included in Microsoft, Adobe and some Apple trust stores by default.  It is not included by default in Mozilla, Java, all mobile device operating systems, or Linux based operating systems." %}

If you are an engineer working on implementing PIV authentication, you may need to download and install the root certificate (COMMON) for your workstations, servers, applications and network domains.

Many applications may require intermediate certificates to successfully trust ALL PIV credentials, and may not support the automatic retrieval of certificate chains.  You should consider the possible unintended consequences of installing intermediate certificates which _only_ represent intermediate certificate chains for your agency users.  You may want to be able to Trust all PIV credentials from agencies, and credentials from our trusted partners.  It is increasingly more common for users from other agencies or partners to _authenticate_ to your networks or applications, and this usage is the foundation of PIV to promote trust, interoperability, authentication, and efficiency across the US Federal Government.  

General recommendations for trust and certificate chain management include:

- COMMON should be used as the trusted root certification authority
- Management of root and intermediate certification authority certificates and distribution to network domains, workstations, servers and applications should be managed with group policy objects, secure automated distributions mechanisms, and enterprise policies and procedures to ensure updates are managed effectively.
- NIST published an [Information Technology Laboratory (ITL) bulletin](http://csrc.nist.gov/publications/nistbul/july-2012_itl-bulletin.pdf){:target="_blank"} in July 2012 which includes general practices to consider.

Installation of the trusted root certificate and intermediate certificates is dependent upon operating systems and applications. Instructions for [downloading](#download-root-and-intermediate-certificates) are at the end of this page.

{% include alert-info.html content= "Upcoming changes to the Federal Common Policy Certification Authority will impact your agency.  Learn more about this update <a href=\"https://fpki.idmanagement.gov/common/\" target=\"_blank\" rel=\"noreferrer\">here</a>." %}

In <strong>October 2020</strong>, the Federal Government created a new FPKI root certification authority.  The new root is named the <strong>Federal Common Policy CA G2</strong>. Between December 2020 and May 2021, the intermediate certification authorities signed by the old root will be migrated to be signed by this new root: Federal Common Policy CA G2.  Once the migration is complete, the old root will be decommissioned.

{% include alert-info.html content="We are collaborating with CISA on a series of webinars to communicate the upcoming changes and answer your questions.  Email fpkirootupdate@gsa.gov to join our next webinar on <strong>January 28, 2021 at 11 AM ET</strong>." %} 


## Revocation
Revocation is the process and technology to identify a certificate as no longer valid - to tell computers and applications _"do not trust this certificate anymore"_.

PIV credential certificates will be _revoked_ when a user terminates employment or a contract with an agency, is issued a new credential, is issued an updated PIV credential, or has a lost, stolen or damaged PIV credential.  The revocation of PIV credential certificates occurs with the PIV credential issuer and certification authority.

There are two protocols available to verify if a PIV credential certificate has been revoked:

- Online Certificate Status Protocol (OCSP)
- Certificate Revocation Lists (CRLs)

Some implementations also validate whether the intermediate certification authority certificates have been _revoked_.  While a revocation of an intermediate certification authority certificate does not occur often, this is a safeguard in place and each intermediate certification Authority and COMMON also publishes Certificate Revocation Lists for the certificates signed next in the chain.   

The table below outlines general information on each protocol, the certificate extension which contains the reference, and design considerations.

| Type | Certificate Extension | Protocol (Port) | Considerations|
| ----- | -------| -------| ------|
| OCSP | Authority Information Access | HTTP (80) | All PIV certificates have OCSP references and OCSP responder web services which are internet accessible and provided by the issuing certification authority. Intermediate certification authorities are **not** required to have OCSP available for the _intermediate_ certificates.|
| CRL  | CRL Distribution Point (CDP) | HTTP (80) | All PIV certificates have CRL references and CRLs files published to internet accessible web services by the issuing certification authority.  All intermediate certification authority certificates also have CRL references, files and internet accessible web services.  CRL files have an expiration time which varies between 6 hours to 18 hours. CRL file sizes distributed by issuing certification authorities as of the date of this guide range from a few kilobytes to **over 30 megabytes (MB)**.

For a portion of your implementations such as network authentication, the _revocation_ checks will occur as part of the operating system or server native functionality.  Other implementations may want to consider services such as implementing Server Certificate Validation Protocol (SCVP).  These are advanced topics to consider and will be covered in other areas of guides soon.  

## Download root and intermediate certificates

The Federal Common Policy Certification Authority (COMMON) and Federal Common Policy CA G2 root certificates can be retrieved via two methods: online or out of band.  We recommend the out of band (email) method for engineers working in production environments.

#### Download root using out-of-band email
- Send an email to: _fpki-help at gsa dot gov_
- Subject line: _Common root needed_
- Please _digitally sign_ the email if you have the capabilities available; if not, the request will still be received and processed
- A signed version of the certificate or email will be sent back to you

#### Download root using online site

##### Federal Common Policy CA
- http://http.fpki.gov/fcpca/fcpca.crt
- cn=Federal Common Policy CA, ou=FPKI, o=U.S. Government, c=US
- SHA1 Hash: 90 5f 94 2f d9 f2 8f 67 9b 37 81 80 fd 4f 84 63 47 f6 45 c1

##### Federal Common Policy CA G2
- http://repo.fpki.gov/fcpca/fcpcag2.crt
- cn=Federal Common Policy CA G2, ou=FPKI, o=U.S. Government, c=US
- SHA1 Hash: 99 B4 25 1E 2E EE 05 D8 29 2E 83 97 A9 01 65 29 3D 11 60 28

{% include alert-warning.html heading = "Verify the hash of the files" content="Verify the hash of the root certificate file matches the entry above before using.  If the hash does not match, do NOT use the certificate file and please use the out-of-band email method." %}

You can verify the hash using common utilities on operating systems, including:

```
	certutil -hashfile fcpca.crt SHA1
```

```
	openssl dgst -sha1 fcpca.crt
```

```
	sha1sum fcpca.crt
```

#### Download any additional Intermediate Certification Authority certificates

You can contact your agency's information security teams for help on additional intermediate certificates, or find the intermediate certificates by using information in your PIV certificates directly.

- View your PIV Authentication certificate. To review how to view your PIV Authentication certificate go to the [Details of a PIV Credential]({{site.baseurl}}/details)
- In the **Authority Information Access (AIA)** extension, there is a URL (http://) which references a file with a .p7b or .p7c extension
- Download the file, open it, and view the intermediate certification authority certificates
- Repeat the process using the AIA extension of the intermediate certification authority certificates until the final reference finds an intermediate certification authority certificate that is issued and signed by COMMON

Many products and implementations may automatically retrieve the intermediate certificates during a process called _certificate path building_ or _certificate path discovery_.   You will encounter varying implementations of the _certificate path discovery_ process based on differences in client operating systems, browsers, mobile devices, programming languages, and even applications directly. It can be challenging to understand all the options that impact your users and applications and we are seeking input and contributions to expand this information for you.     

We want to add more information to help you so check back often, or review the Issues posted and consider contributing!
