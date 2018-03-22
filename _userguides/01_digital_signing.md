---
layout: default
navtitle: Sign Microsoft Word
title: Digitally Sign Microsoft Word Document
pubDate: March 23, 2018
collection: userguides
permalink: userguides/signworddoc/
description: This guide will help you to digitally sign a Microsoft Word document with your PIV credential or similar digital certificate.
---

<!--Suggest that we add for the non-technical user: "A digital signature is [simple definition]."-->This guide will help you to digitally sign a Microsoft Word document with your PIV credential or similar digital certificate.  

- [Add a Digital Signature Using Signature Line](#add-a-digital-signature-using-a-signature-line)
- [Add an Invisible Digital Signature](#add-an-invisible-digital-signature)
- [Add Multiple Digital Signatures](#add-multiple-digital-signatures)
- [Remove a Signature](#remove-a-signature)
- [Verify a Digital Signature](#verify-a-digital-signature)
- [Change a Signature Algorithm](#change-a-signature-algorithm)
- [Additional Resources](#additional-resources)

## Add a Digital Signature Using a Signature Line

{% include alert-info.html content="These digital-signing steps may be used for Microsoft Word 2010, 2013 and 2016. Certain steps and screen contents may differ for older versions of Microsoft Word." %}

1. Open your Microsoft Word document and scroll to the area where you want to add your signature line.
2. At the Word ribbon, first select the **Insert** tab and then click **Signature Line** in the **Text** group.<br/>
![Insert Signature Line]({{site.baseurl}}/img/word-signature-1.png)

3. _A **Signature Setup** pop-up box appears._ Enter your information in the text fields and click **OK**.<br/>
![Signature Setup Box]({{site.baseurl}}/img/word-signature-2.png)

4. _A signature line appears._ Double-click on it. <br/>
![Signature Line]({{site.baseurl}}/img/word-signature-3.png)

5. _A **Sign** pop-up box appears._ At the **X**, type your name. Next, look at the **Signing as:** field. _You should see your name and certificate information._ If you don't, click the **Change** button to switch certificates and click **Sign**.<br/>
![Sign Box]({{site.baseurl}}/img/word-signature-4.png)

6. Enter your Smart Card (PIV) PIN and click **OK**.<br/>
![PIV PIN]({{site.baseurl}}/img/word-signature-5.png)

7. _The **Signature Confirmation** box lets you know that your digital signature was saved._ Click **OK**. <br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

![Marked as final]({{site.baseurl}}/img/word-signature-7.png)

{% include alert-info.html content="Once you've digitally signed your document, if you edit the document, it will remove the digital signature. Don't worry--if editing _is_ needed, you can repeat the digital signing process above again." %}

<br/>

## Add an Invisible Digital Signature

If you don't want your name to appear in your Microsoft Word document, you can add an _invisible digital signature_.  

1. Open your Word document and click the **File** tab.

2. Click **Info** and then click **Protect Document**.<br/>
![Protect Document]({{site.baseurl}}/img/word-signature-9.png)

3. From the **Protect Document** drop-down menu, click **Add a Digital Signature**.

4. Select a **Commitment Type** and click **Sign**.<br/>
![Sign Document]({{site.baseurl}}/img/word-signature-10.png)

5. Enter your Smart Card (PIV) PIN and click **OK**.<br/>
![PIV PIN]({{site.baseurl}}/img/word-signature-5.png)

6. _The **Signature Confirmation** box lets you know that your digital signature was saved._ Click **OK**.<br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

<br/>

## Add Multiple Digital Signatures

If you need multiple approvers to digitally sign your Microsoft Word document, you can use either the signature line or invisible signature method.

### Add Multiple Signatures Using Signature Lines

If, after you've digitally signed your Word document, a second approver _also needs to digitally sign it, you can add a second signature line_.<!--How many total signers can be added to a document? We could say "up to X approvers may sign a document."  These instructions assume that the first approver has already digitally signed the document. Not so clear.-->

1. For the second approver, open your Word document and scroll to the area where you want to add the approver's signature line.<!--Shouldn't the second approver be taking these actions himself?-->
2. At the Word ribbon, first select the **Insert** tab and then click **Signature Line** in the **Text** group.<br/><br/>
![Signature Line]({{site.baseurl}}/img/word-signature-1.png)

3. Enter your information for the approver in the **Signature Setup** pop-up box and click '**OK**'.<br/>
![Signature Setup]({{site.baseurl}}/img/word-signature-13.png)

- Once you click '**OK**' you will find a signature line created in the Word document as with the approver's name. You should create all the signature lines before you sign the document.<br/>
![Signature Line]({{site.baseurl}}/img/word-signature-14.png)

- Double click your signature link to display a pop-up box to sign. Type your name in the box. Verify that the '**Signing as:**' has your certificate information in the box. If not, you should switch certificate using the '_Change_' button. Click '**Sign**'.<br/>
![Signature Box]({{site.baseurl}}/img/word-signature-4.png)

- You will be prompted to enter your Smart Card (PIV) PIN. Click '**OK**'.<br/>
![Certificate PIN]({{site.baseurl}}/img/word-signature-5.png)

- _The **Signature Confirmation** box lets you know that your digital signature was saved._ Click **OK**..<br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

- Now you can send this digitally signed document to the approver. 

- The approver will be able to open the document and double-click the '**Signature Line**' corresponding to their name, and complete their signing process.

### Multiple Signatures Using Invisible Signature

You can allow another user to sign the document without the signature line using the 'Invisible Signature' method. You can follow the same steps as provided for the invisible signature. 

- Open your Word document and click on the '**File**' tab.

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

Microsoft Word uses SHA-1 algorithm by default to digitally sign a Word document. The SHA-1 algorithm is no longer considered secure. Other algorithms such as SHA-256 are preferred.

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

You can also use **SHA-384** or **SHA-512** for more secure algorithms. Save the registry settings and restart your computer.

## Additional Resources

1. [Add or remove digital signature in Office files](https://support.office.com/en-us/article/add-or-remove-a-digital-signature-in-office-files-70d26dc9-be10-46f1-8efa-719c8b3f1a2d){:target="_blank"}
1. [XML Digital Signature](https://www.w3.org/TR/XAdES/
){:target="_blank"}
1. [Digital Signatures in Office 2010](https://blogs.technet.microsoft.com/office2010/2009/12/08/digital-signatures-in-office-2010/){:target="_blank"}
1. [Digital Signature Settings in Office 2013](https://technet.microsoft.com/en-us/library/cc545900.aspx){:target="_blank"}
