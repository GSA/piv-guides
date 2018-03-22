---
layout: default
navtitle: Sign Microsoft Word
title: How To Digitally Sign Microsoft Word Document
pubDate: March 23, 2018
collection: userguides
permalink: userguides/signworddoc/
description: A digital signature will encrypt your Word document after validating your agency issued X.509 certificate. This will ensure that the document that you have submitted was not tampered with by someone else. This user guide will show you how to digitally sign a Microsoft Word Document.
---

A digital signature will encrypt your Word document after validating your agency issued X.509 certificate. This will ensure that the document that you have submitted was not tampered with by someone else. This user guide will show you how to digitally sign a Microsoft Word Document.

{% include alert-info.html content="You will require your agency issued X.509 certificate to sign a Word document. This certificate may reside in your GFE or your PIV card." %}

<br/>
You will find the following topics:
- [Sign Microsoft Word](#sign-microsoft-word)
- [Remove Signature From Microsoft Word](#remove-signature-from-microsoft-word)
- [Invisible Digital Signature](#invisible-digital-signature)
- [Change Signature Algorithm](#change-signature-algorithm)
- [Additional Resources](#additional-resources)

{% include alert-warning.html content="You may face compatibility issues with digital signature in Word 2013 document while opening in Word 2010 or 2007." %} 

<br/>

## Sign Microsoft Word

{% include alert-info.html content="These instructions are relevant to Microsoft Word 2010, 2013 and 2016. The steps and screenshots might be different for older versions of MS Word software." %}

- Open the Microsoft Word document and scroll down to the section where you want your signature to be displayed.
- Select '**Insert**' tab from the top menu and click on '**Signature Line**' in the '**Text**' group.<br/>
![Signature Line]({{site.baseurl}}/img/word-signature-1.png)

- Enter your information in the **Signature Setup** pop-up box and click '**OK**'.<br/>
![Signature Setup]({{site.baseurl}}/img/word-signature-2.png)

- Once you click '**OK**' you will find a signature line created in the Word document as shown below. <br/>
![Signature Line]({{site.baseurl}}/img/word-signature-3.png)

- Double click the signature link to display a pop-up box to sign. Type your name in the box. Verify that the '**Signing as:**' has your certificate information in the box. If not, you should switch certificate using the '_Change_' button. Click '**Sign**'.<br/>
![Signature Box]({{site.baseurl}}/img/word-signature-4.png)

- You will be prompted to enter your certificate PIN. Click '**OK**'.<br/>
![Certificate PIN]({{site.baseurl}}/img/word-signature-5.png)

- It will display the information that the document is now digitally signed. Click '**OK**'.<br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

- The document will now be marked as '**FINAL**' and editing the document will not be allowed.
![Marked as final]({{site.baseurl}}/img/word-signature-7.png)

{% include alert-info.html content="Once you have signed the document, you will not be able to modify the document without removing the signature line. You can repeat the signing process again after you complete editing the document." %}

<br/>
## Remove Signature From Microsoft Word

To remove a signature:
- Open the Word document and navigate to the signature line.
- Right click on the signature.
- Click '**Remove Signature**' and click '**Yes**' when prompted.

![Remove Signature]({{site.baseurl}}/img/word-signature-8.png)

<br/>
## Invisible Digital Signature

You can also digitally sign a Word document without any signature line in the document. This serves the same purpose as above, however, the signature is not visible within the document. 

- Open the Word document and click on the '**File**' tab.

- Click '**Info**' and then click '**Protect Document**'.<br/>
![Protect Document]({{site.baseurl}}/img/word-signature-9.png)

- From the drop down menu, click '**Add a Digital Signature**'.

- Select a '**Commitment Type**' and click '**Sign**'.<br/>
![Sign Document]({{site.baseurl}}/img/word-signature-10.png)

- You will be prompted to enter your certificate PIN. Click '**OK**'.<br/>
![Certificate PIN]({{site.baseurl}}/img/word-signature-5.png)

- It will display the information that the document is now digitally signed. Click '**OK**'.<br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

## Change Signature Algorithm

Microsoft Word uses SHA-1 algorithm to digitally sign a Word document. SHA-1 algorithm is not considered as secure as other preferred algorithms such as SHA-256.

{% include alert-info.html content="These instructions require administrator privileges on your computer." %} 
 
To change the signature algorithm to SHA-256, use the following registry setting:

- **Word 2010**: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\office\14.0\common\signatures
- **Word 2013**: Computer\HKEY_CURRENT_USER\software\policies\Microsoft\Office\15.0\common\signatures
- **Word 2016**: Computer\HKEY_CURRENT_USER\software\policies\microsoft\office\16.0\common\signatures

Add or update the values as specified below.

|**Value Name**|signaturehashalg|
|**Value Type**|REG_SZ|
|**Value**|sha256|

You can also use **sha384** or **sha512** for more secure algorithm. Save the registry settings and restart your computer.

## Additional Resources

1. [Add or remove digital signature in Office files](https://support.office.com/en-us/article/add-or-remove-a-digital-signature-in-office-files-70d26dc9-be10-46f1-8efa-719c8b3f1a2d){:target="_blank"}
1. [XML Digital Signature](https://www.w3.org/TR/XAdES/
){:target="_blank"}
1. [Digital Signatures in Office 2010](https://blogs.technet.microsoft.com/office2010/2009/12/08/digital-signatures-in-office-2010/){:target="_blank"}
1. [Digital Signature Settings in Office 2013](https://technet.microsoft.com/en-us/library/cc545900.aspx){:target="_blank"}