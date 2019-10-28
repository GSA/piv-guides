---
layout: default
navtitle: Additional Resources
title: Additional Resources
pubDate: July 17, 2018
collection: userguides
permalink: userguides/additionalresources/
description: This guide will walk you through the procedures for digitally signing a Microsoft Word document for submission to the Office of the Federal Register using your PIV credential or similar digital certificate.
---

For additional information about digital signatures and related policies, see the following resources:

- Add or Remove a Digital Signature in Office Files
- XML Digital Signatures
- Digital Signatures in Office 2010
- Plan Digital Signature Settings for Office 2013
- X.509 Certificate Policy for the U.S. Federal PKI Common Policy Framework
- NIST Policy on Hash Functions

## Software Configurations for Digital Signatures

{% include alert-info.html content="You must have administrative privileges to perform these steps." %}

By default, Microsoft Word generates digital signatures using the SHA-1 hash algorithm, which is no longer considered secure as researchers have produced hash collisions. You should us more secure hash algorithms, such as SHA-256. See the NIST guidance on hash functions for more information.

You can use either the **Group Policy** or **Computer Registry** settings to verify or change the hash algorithm settings for Microsoft Office. For additional information, see Microsoft's documentation on Digital Signature Settings in Office 2013.

**Change the Microsoft Office Signature algorithm as follows:**
- Word 2010: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\14.0\common\signatures
- Word 2013: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\15.0\common\signatures
- Word 2016: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\16.0\common\signatures

**Add or update the following fields:**
- Value Name: signaturehashalg
- Value Type: REG_SZ
- Value: Sha256

**Save the registry settings and restart your computer.**
