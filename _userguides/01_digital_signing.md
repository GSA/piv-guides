---
layout: default
navtitle: Sign Microsoft Word
title: How To Digitally Sign Microsoft Word Document
pubDate: March 23, 2018
collection: userguides
permalink: userguides/signworddoc/
description: A digital signature will encrypt your Word document after validating your agency issued certificate. This will ensure that the document that you have submitted was not tampered with by someone else. This user guide will show you how to digitally sign a Microsoft Word Document.
---

A digital signature will encrypt your Word document after validating your agency issued certificate. This will ensure that the document that you have submitted was not tampered with by someone else. This user guide will show you how to digitally sign a Microsoft Word Document.

{% include alert-info.html content="You will require your agency issued certificate to sign a Word document. This certificate may reside in your GFE or your PIV card." %}

- [Sign Microsoft Word](#sign-microsoft-word)
- [Remove Signature From Microsoft Word](#remove-signature-from-microsoft-word)
- [Change Signature Algorithm](#change-signature-algorithm)
- [Additional Resources](#additional-resources)

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


## Remove Signature From Microsoft Word

To remove a signature:
- Open the Word document and navigate to the signature line.
- Right click on the signature.
- Click '**Remove Signature**' and click '**Yes**' when prompted.

![Remove Signature]({{site.baseurl}}/img/word-signature-8.png)

## Change Signature Algorithm

Microsoft Word uses SHA-1 algorithm to digitally sign a Word document. SHA-1 algorithm is not considered as secure as other preferred algorithms such as SHA-256. You will find the steps to change the signature algorithm for your desktop.

{% include alert-info.html content="These instructions require administrator privileges on your computer." %} 
<br/>
- Update the following registry settings: <br/>
Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\office\14.0\common\signatures

## Additional Resources

1. [Add or remove digital signature in Office files](https://support.office.com/en-us/article/add-or-remove-a-digital-signature-in-office-files-70d26dc9-be10-46f1-8efa-719c8b3f1a2d){:target="_blank"}
1. [Signature Algorithm & Group Policy Setup](https://technet.microsoft.com/en-us/library/cc545900.aspx#Anchor_2
){:target="_blank"}
1. [XML Digital Signature](https://www.w3.org/TR/XAdES/
){:target="_blank"}
