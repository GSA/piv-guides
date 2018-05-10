---
layout: default
navtitle: Digitally Signing in Microsoft Word
title: Digitally Sign a Microsoft Word Document
pubDate: March 23, 2018
collection: userguides
permalink: userguides/signworddoc/
description: This guide will walk you through the steps for digitally signing a Microsoft Word document with your PIV credential or similar digital certificate.
---

{% include alert-info.html content="Before you begin digitally signing documents, please ask your Technical Support team to verify the digital signature settings on your computer by following the steps in the Verify Digital Signature Settings section below." %}

This guide will walk you through the steps for digitally signing a document in Microsoft Word 2010, 2013, or 2016 using your PIV credential or digital certificate.

To begin, choose the method you'd like to use for applying your digital signature:
- [Add a Digital Signature Using a Signature Line](#add-a-digital-signature-using-a-signature-line)
- [Add an Invisible Digital Signature](#add-an-invisible-digital-signature)
- [Add Multiple Digital Signatures Using Signature Lines](#add-multiple-digital-signatures-using-signature-lines)
- [Add Multiple Invisible Digital Signatures](#add-multiple-invisible-digital-signatures)

The following links provide guidance to some related functionality and resources:
- [Remove a Digital Signature](#remove-a-digital-signature)
- [View Digital Signatures](#view-digital-signatures)
- [Verify Digital Signature Settings](#verify-digital-signature-settings)
- [Additional Resources](#additional-resources)

## Add a Digital Signature Using a Signature Line

1. To add a digital signature, open your Microsoft Word document and click where you'd like to add your signature line. 
2. From the Word ribbon, select the **Insert** tab and then click **Signature Line** in the **Text** group.<br/>
![Insert Signature Line]({{site.baseurl}}/img/word-signature-1.png)

3. _A **Signature Setup** pop-up box appears._ Enter your information in the text fields and click **OK**.<br/>
![Signature Setup Box]({{site.baseurl}}/img/word-signature-2.png)

4. Double-click the _signature line_.<br/>
![Signature Line]({{site.baseurl}}/img/word-signature-3.png)

5. _A **Sign** pop-up box appears._ At the **X**, type your name. Next, look at the **Signing as:** field. Select the signing certificate. To ensure that this is the correct certificate, click the **Change** button. <br/>
![Sign Box]({{site.baseurl}}/img/word-signature-4.png)

6. Click on **Click here to view certificate properties**. <br/>
![Sign Box]({{site.baseurl}}/img/word-signature-18.png)

7. _The **Certificate Details** box appears._ Go to the **Details** tab and scroll down to **Key Usage**. Single-click on it. The lower text box should now display _Digital Signature, Non-Repudiation_. If it does, then this is the right certificate. Click **OK**.<br/>
![Sign Box]({{site.baseurl}}/img/word-signature-20.png)

8. If this is the _wrong_ certificate, click **OK**. Then click **More Choices** to see other certificates. Select another certificate and repeat these steps until you find the correct certificate. <br/> 
![Sign Box]({{site.baseurl}}/img/word-signature-19.png)

9. Click the **Sign** button to sign the document. Insert your PIV card into the card reader. Enter your Smart Card (PIV) PIN and click **OK**.<br/>
![PIV PIN]({{site.baseurl}}/img/word-signature-5.png)

10. _The **Signature Confirmation** box tells you that Word saved your digital signature._ Click **OK**. <br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

![Marked as final]({{site.baseurl}}/img/word-signature-7.png)

{% include alert-info.html content="Once you've digitally signed your document, if you edit it, Word will remove the digital signature. Don't worry. You can always go back to Step 1 and digitally sign it again." %}

<br/>

## Add an Invisible Digital Signature

You can add an _invisible digital signature_ to prevent your name from appearing in a document.  

1. Open your document and click the **File** tab.

2. Click **Info** and then click **Protect Document**.<br/>
![Protect Document]({{site.baseurl}}/img/word-signature-9.png)

3. From the **Protect Document** drop-down menu, click **Add a Digital Signature**.

4. Select a **Commitment Type**, such as _created and approved this document_, and then click **Sign**.<br/>
![Sign Document]({{site.baseurl}}/img/word-signature-10.png)

5. Insert your PIV card into the card reader. Enter your Smart Card (PIV) PIN and click **OK**.<br/>
![PIV PIN]({{site.baseurl}}/img/word-signature-5.png)

6. _The **Signature Confirmation** box tells you that Word saved your digital signature._ Click **OK**.<br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

<br/>

## Add Multiple Digital Signatures Using Signature Lines

Once you digitally sign a document, you can have others also digitally sign it. (**Note:**&nbsp;&nbsp; If you are the first approver, you should create the signature lines for all of the approvers. Then, send the document to the second approver.)

1. If you are the second (or other) approver, open the document you've received. Double-click your signature line to sign. Follow Steps 4-10 from [Add a Digital Signature Using a Signature Line](#add-a-digital-signature-using-a-signature-line). <br/>
![Signature Line]({{site.baseurl}}/img/word-signature-1.png) 

3. _A **Signature Setup** pop-up box appears._ Enter your information in the text fields and click **OK**<br/>
![Signature Setup]({{site.baseurl}}/img/word-signature-13.png)

4. Double-click your _signature line_.<br/> 
![Signature Line]({{site.baseurl}}/img/word-signature-14.png)

5. _A **Sign** pop-up box appears._ At the **X**, type your name. 

6. Next, look at the **Signing as:** field. _You should see your name and certificate information._ If you don't, click the **Change** button to select a different certificate and click **Sign**.<br/>
![Signature Box]({{site.baseurl}}/img/word-signature-4.png)

7. Insert your PIV card and enter your Smart Card (PIV) PIN. Click **OK**.<br/>
![Certificate PIN]({{site.baseurl}}/img/word-signature-5.png)

8. _The **Signature Confirmation** box tells you that Word saved your digital signature._ Click **OK**. <br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

9. Send the digitally signed document to the next approver. 

_Each successive approver will be able to open the document and double-click the **Signature Line** with his/her name and complete the signing process._

## Add Multiple Invisible Digital Signatures

Multiple approvers may digitally sign a document. Use the same procedures as you would to add one invisibile digital signature: [Add an Invisible Digital Signature](#add-an-invisible-digital-signature). 

_The final approver will see multiple "invisible" signatures in the document._<br/>
![View Signature]({{site.baseurl}}/img/word-signature-12.png)

<br/>

## View Digital Signatures

{% include alert-warning.html content="If you use Word 2013 and open a digitally signed Word 2007 or 2010 document, you may have compatibility issues." %} 
<br/>
You can view digital signatures in an incompatible Word document in one of two ways:

1. Click the **View Signatures** button just below the Word ribbon.<br/>
![View Signature]({{site.baseurl}}/img/word-signature-16.png)

**_OR_**

2. Click the **File** tab and select **Info**. Then click **View Signatures**.<br/>
![View Signature]({{site.baseurl}}/img/word-signature-11.png)

For either option, you will be able to see the digital signature details in the **Signatures** box.<br/>
![View Signature]({{site.baseurl}}/img/word-signature-17.png)

<br/>

## Remove a Digital Signature

1. If you want to remove a digital signature, open your Word document and go to the signature line. 
2. If there is no signature line, click the **View Signatures** button just below the Word ribbon.
3. From the **Signatures** box, select the signature you want to to delete.<br/>
![View Signature]({{site.baseurl}}/img/word-signature-17.png)
<br/>
4. Right-click on the signature and then click **Remove Signature**.  
5. When prompted, click **Yes**.<br/>
![Remove Signature]({{site.baseurl}}/img/word-signature-8.png)

<br/>

## Verify Digital Signature Settings

{% include alert-info.html content="Please ask your Technical Support staff for help. Administrator privileges are required for these steps." %} 

By default, Microsoft Word uses the SHA-1 hash algorithm to generate digital signatures. The SHA-1 hash algorithm is no longer considered secure. More secure hash algorithms, such as SHA-256, should be used. [(See NIST's guidance on hash functions)](https://csrc.nist.gov/Projects/Hash-Functions/NIST-Policy-on-Hash-Functions)

You can use either option below to verify/change the hash algorithm settings for Microsoft Office: 

1. **Group Policy** settings:  [Digital Signature Settings in Office 2013](https://technet.microsoft.com/en-us/library/cc545900.aspx){:target="_blank"}.  (For additional information, consult Microsoft's technical documents.)
2. **Computer registry** settings. Change the Microsoft Office signature algorithm, as follows:

```
Word 2010:  Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\14.0\common\signatures
Word 2013:  Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\15.0\common\signatures
Word 2016:  Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\16.0\common\signatures
```
* Add or update these values: 

|**Value Name**|signaturehashalg|
|**Value Type**|REG_SZ|
|**Value**|sha256|

* Save the registry settings and restart the computer.

(For additional information, consult Microsoft's technical documents.)

## Additional Resources

1. [Add or Remove Digital Signature in Office Files](https://support.office.com/en-us/article/add-or-remove-a-digital-signature-in-office-files-70d26dc9-be10-46f1-8efa-719c8b3f1a2d){:target="_blank"}
1. [XML Digital Signature](https://www.w3.org/TR/XAdES/
){:target="_blank"}
1. [Digital Signatures in Office 2010](https://blogs.technet.microsoft.com/office2010/2009/12/08/digital-signatures-in-office-2010/){:target="_blank"}
1. [Digital Signature Settings in Office 2013](https://technet.microsoft.com/en-us/library/cc545900.aspx){:target="_blank"}
1. [X.509 Certificate Policy for the U.S. Federal PKI Common Policy Framework](https://www.idmanagement.gov/wp-content/uploads/sites/1171/uploads/fpki-x509-cert-common-policy.pdf){:target="_blank"}
1. [NIST Policy on Hash Functions](https://csrc.nist.gov/Projects/Hash-Functions/NIST-Policy-on-Hash-Functions){:target="_blank"}
