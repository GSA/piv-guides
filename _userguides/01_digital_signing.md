---
layout: default
navtitle: Sign Microsoft Word
title: How To Digitally Sign Microsoft Word Document
pubDate: March 16, 2018
collection: userguides
permalink: userguides/signworddoc/
description: A digital signature will encrypt your Word document after validating your certificate information. This will ensure that the document that you submit has not been tampered with by someone else. This user guide will show you how to digitally sign a Microsoft Word Document.
---

A digital signature will encrypt your Word document after validating your certificate information. This will ensure that the document that you submit has not been tampered with by someone else. This user guide will show you how to digitally sign a Microsoft Word Document.

{% include alert-info.html content="You will require your Federal agency issued credential certificate to sign a Word document." %}

- [Sign Microsoft Word](#sign-microsoft-word)
- [Change Signature Algorithm](#change-signature-algorithm)
- [Additional Resources](#additional-resources)

## Sign Microsoft Word

{% include alert-info.html content="These instructions are relevant to Microsoft Word 2010, 2013 and 2016. The steps and screenshots might be different for older versions of MS Word software." %}

- Open the Microsoft Word document and scroll down to the section where you want your signature to be displayed.
- Select '_Insert_' from the top menu and click on '_Signature Line_'.<br/>
![Signature Line]({{site.baseurl}}/img/word-signature-1.png)

- Enter your name in the signature pop-up window and click '_OK_'.<br/>
![Signature Pop-up]({{site.baseurl}}/img/word-signature-2.png)

- Once you click '_OK_' you will find a signature box created in the Word document as shown below. <br/>
![Signature Box]({{site.baseurl}}/img/word-signature-3.png)

- Double click the signature box to display a pop-up box to sign. Type your name in the box. Verify that the '_Signing as:_' has your certificate information in the box. If not, you should switch certificate using the '_Change_' button. Click '_Sign_'.<br/>
![Signature Box]({{site.baseurl}}/img/word-signature-4.png)

- You will be prompted to enter your certificate PIN. Click '_OK_'.<br/>
![Signature Box]({{site.baseurl}}/img/word-signature-5.png)

- It will display the information that the document is now digitally signed. Click '_OK_'.<br/>
![Signature Box]({{site.baseurl}}/img/word-signature-6.png)

## Change Signature Algorithm

Microsoft Word uses SHA-1 algorithm to digitally sign a Word document. Since the SHA-1 algorithm is not considered as secure as other new algorithms, you will find the steps to change the signature algorithm for your desktop. You will also find some information in this article on SHA-1.

{% include alert-info.html content="These instructions require administrator privileges for your computer." %} 
<br/>
- Update the following registry settings: <br/>
Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\office\14.0\common\signatures

## Additional Resources

1. [Add or remove digital signature in Office files](https://support.office.com/en-us/article/add-or-remove-a-digital-signature-in-office-files-70d26dc9-be10-46f1-8efa-719c8b3f1a2d){:target="_blank"}
1. [Managing Certificates with Certificate Stores](https://technet.microsoft.com/en-us/library/cc545900.aspx#Anchor_2
){:target="_blank"}
1. [XML Digital Signature](https://www.w3.org/TR/XAdES/
){:target="_blank"}
