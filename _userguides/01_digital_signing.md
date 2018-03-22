---
layout: default
navtitle: Sign Microsoft Word
title: How To Digitally Sign Microsoft Word Document
pubDate: March 23, 2018
collection: userguides
permalink: userguides/signworddoc/
description: This user guide will show you how to digitally sign a Microsoft Word document with your PIV credential or similar digital certificates.
---

This user guide will show you how to digitally sign a Microsoft Word document with your PIV credential or similar digital certificates.

You will find the following topics:
- [Sign Microsoft Word Using Signature Line](#sign-microsoft-word-using-signature-line)
- [Invisible Digital Signature](#invisible-digital-signature)
- [Multiple Digital Signatures](#multiple-digital-signatures)
- [Remove Signature From Microsoft Word](#remove-signature-from-microsoft-word)
- [Verify Digital Signature](#verify-digital-signature)
- [Change Signature Algorithm](#change-signature-algorithm)
- [Additional Resources](#additional-resources)

## Sign Microsoft Word Using Signature Line

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

<br/>

## Multiple Digital Signatures

You can choose to digitally sign a Word document by multiple approvers either using the invisible signature or a signature line.

### Multiple Signatures Using Signature Line

If you want another person to sign your document, you will have to add a new signature line for that person to sign.

- Open the Microsoft Word document and scroll down to the section where you want the approver's signature to be displayed.
- Select '**Insert**' tab from the top menu and click on '**Signature Line**' in the '**Text**' group.<br/>
![Signature Line]({{site.baseurl}}/img/word-signature-1.png)

- Enter your information for the approver in the **Signature Setup** pop-up box and click '**OK**'.<br/>
![Signature Setup]({{site.baseurl}}/img/word-signature-13.png)

- Once you click '**OK**' you will find a signature line created in the Word document as with the approver's name. You should create all the signature lines before you sign the document.<br/>
![Signature Line]({{site.baseurl}}/img/word-signature-14.png)

- Double click your signature link to display a pop-up box to sign. Type your name in the box. Verify that the '**Signing as:**' has your certificate information in the box. If not, you should switch certificate using the '_Change_' button. Click '**Sign**'.<br/>
![Signature Box]({{site.baseurl}}/img/word-signature-4.png)

- You will be prompted to enter your certificate PIN. Click '**OK**'.<br/>
![Certificate PIN]({{site.baseurl}}/img/word-signature-5.png)

- It will display the information that the document is now digitally signed. Click '**OK**'.<br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

- Now you can send this digitally signed document to the approver. 

- The approver will be able to open the document and double click the '**Signature Line**' corresponding to their name, and complete their signing process.

### Multiple Signatures Using Invisible Signature

You can allow another user to sign the document without the signature line using the 'Invisible Signature' method. You can follow the same steps as provided for the invisible signature. 

- Open the Word document and click on the '**File**' tab.

- Click '**Info**' and then click '**Protect Document**'.<br/>
![Protect Document]({{site.baseurl}}/img/word-signature-15.png)

- From the drop down menu, click '**Add a Digital Signature**'.

- Complete the signature steps for invisible signature.

- You will now see multiple signatures in the document.

![View Signature]({{site.baseurl}}/img/word-signature-12.png)

<br/>

## Verify Digital Signature

{% include alert-warning.html content="You may face compatibility issues with digital signature in Word 2013 document while opening in Word 2010 or 2007." %} 

You can view the signatures for a Word document by either one of these two ways.

- You can click the '**View Signatures**' button on top of the document.
![View Signature]({{site.baseurl}}/img/word-signature-16.png)

- Click on the '**File**' tab and then click '**View Signatures**' in the '**Info**' section.<br/>
![View Signature]({{site.baseurl}}/img/word-signature-11.png)

- In the '**Signatures**' box, you will be able to see the signature details and status.
![View Signature]({{site.baseurl}}/img/word-signature-17.png)

<br/>

## Remove Signature From Microsoft Word

To remove a signature:
- Open the Word document and navigate to the signature line. If there is no signature line, you can select the signature to delete from the '**Signatures**' box.
- Right click on the signature.
- Click '**Remove Signature**' and click '**Yes**' when prompted.

![Remove Signature]({{site.baseurl}}/img/word-signature-8.png)

<br/>

## Change Signature Algorithm

Microsoft Word uses SHA-1 algorithm by default to digitally sign a Word document. SHA-1 algorithm is not considered as secure as other preferred algorithms such as SHA-256.

{% include alert-info.html content="These instructions require administrator privileges on your computer." %} 

You can set signature algorithm using either **Group Policy** settings or changing the registry settings on each individual computer. You can refer to the guides provided by Microsoft for Group Policy settings.
 
To change the signature algorithm to SHA-256 using registry update, use the following registry setting:

- **Word 2010**: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\office\14.0\common\signatures
- **Word 2013**: Computer\HKEY_CURRENT_USER\software\policies\Microsoft\Office\15.0\common\signatures
- **Word 2016**: Computer\HKEY_CURRENT_USER\software\policies\Microsoft\office\16.0\common\signatures

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