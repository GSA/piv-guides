---
layout: default
navtitle: Additional Resources
title: Additional Resources
pubDate: October 28, 2019
collection: userguides
permalink: userguides/additionalresources/
description: This page includes additional policies, Microsoft documentation, and administrator instructions related to digital signatures.
---

For additional information about digital signatures and related policies, see the following resources:

- [Add or Remove a Digital Signature in Office Files](https://www.archives.gov/files/federal-register/write/handbook/ddh.pdf){:target="_blank"}
- [XML Digital Signatures](https://www.w3.org/TR/XAdES/){:target="_blank"}
- [Digital Signatures in Office 2010](https://blogs.technet.microsoft.com/office2010/2009/12/08/digital-signatures-in-office-2010/){:target="_blank"}
- [Plan Digital Signature Settings for Office 2013](https://docs.microsoft.com/en-us/previous-versions/office/office-2013-resource-kit/cc545900(v=office.15)?redirectedfrom=MSDN){:target="_blank"}
- [X.509 Certificate Policy for the U.S. Federal PKI Common Policy Framework](https://www.idmanagement.gov/wp-content/uploads/sites/1171/uploads/fpki-x509-cert-policy-common.pdf){:target="_blank"}
- [NIST Policy on Hash Functions](https://csrc.nist.gov/Projects/Hash-Functions/NIST-Policy-on-Hash-Functions){:target="_blank"}

## Software Configurations for Digital Signatures

{% include alert-info.html content="You must have administrative privileges to perform these steps." %}

By default, Microsoft Word generates digital signatures using the SHA-1 hash algorithm, which is no longer considered secure as researchers have produced hash collisions. You should us more secure hash algorithms, such as SHA-256. See the [NIST guidance on hash functions](https://csrc.nist.gov/Projects/Hash-Functions/NIST-Policy-on-Hash-Functions){:target="_blank"} for more information.

You can use either the **Group Policy** or **Computer Registry** settings to verify or change the hash algorithm settings for Microsoft Office. For additional information, see Microsoft's documentation on [Digital Signature Settings in Office 2013](https://docs.microsoft.com/en-us/previous-versions/office/office-2013-resource-kit/cc545900(v=office.15)?redirectedfrom=MSDN){:target="_blank"}.

**Change the Microsoft Office Signature algorithm as follows:**
- Word 2010: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\14.0\common\signatures
- Word 2013: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\15.0\common\signatures
- Word 2016: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\16.0\common\signatures

**Add or update the following fields:**
- Value Name: signaturehashalg
- Value Type: REG_SZ
- Value: Sha256

**Save the registry settings and restart your computer.**
