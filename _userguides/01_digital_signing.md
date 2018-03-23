---
layout: default
navtitle: Sign Microsoft Word
title: Digitally Sign Microsoft Word Document
pubDate: March 23, 2018
collection: userguides
permalink: userguides/signworddoc/
description: This guide will help you to digitally sign a Microsoft Word document with your PIV credential or similar digital certificate.
---

<!--Suggest that we add for the non-technical user: "A digital signature is [simple definition]."-->This guide will help you to digitally sign a Microsoft Word document with your PIV credential or similar digital certificate.<br/>

- [Add a Digital Signature Using Signature Line](#add-a-digital-signature-using-a-signature-line)
- [Add an Invisible Digital Signature](#add-an-invisible-digital-signature)
- [Add Multiple Digital Signatures](#add-multiple-digital-signatures)
- [Add Multiple Invisible Signatures](#add-multiple-invisible-signatures)
- [Remove a Digital Signature](#remove-a-digital-signature)
- [View Digital Signatures](#view-digital-signatures)
- [Change a Signature Algorithm](#change-a-signature-algorithm)
- [Additional Resources](#additional-resources)

## Add a Digital Signature Using a Signature Line
<!--For multiple approvers, couldn't we say "repeat these steps for multiple approvers to add their digital signatures"?-->
{% include alert-info.html content="These digital-signing steps may be used for Microsoft Word 2010, 2013 and 2016. Certain steps and screens may differ for older versions of Microsoft Word." %}

1. Open your Microsoft Word document. Click where you want to add your signature line. 
2. From the Word ribbon, select the **Insert** tab and then click **Signature Line** in the **Text** group.<br/>
![Insert Signature Line]({{site.baseurl}}/img/word-signature-1.png)

3. _A **Signature Setup** pop-up box appears._ Enter your information in the text fields and click **OK**.<br/>
![Signature Setup Box]({{site.baseurl}}/img/word-signature-2.png)

4. Double-click the _signature line_.<br/>
![Signature Line]({{site.baseurl}}/img/word-signature-3.png)

5. _A **Sign** pop-up box appears._ At the **X**, type your name. 

6. Next, look at the **Signing as:** field. _You should see your name and certificate information._ If you don't, click the **Change** button to select a different certificate and click **Sign**.<br/>
![Sign Box]({{site.baseurl}}/img/word-signature-4.png)

7. Enter your Smart Card (PIV) PIN and click **OK**.<br/>
![PIV PIN]({{site.baseurl}}/img/word-signature-5.png)

8. _The **Signature Confirmation** box tells you that Word saved your digital signature._ Click **OK**. <br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

![Marked as final]({{site.baseurl}}/img/word-signature-7.png)

{% include alert-info.html content="Once you digitally sign your document, if you edit it, Word will remove the digital signature. Don't worry! You can always go back to Step 1 and digitally sign it again." %}

<br/>

## Add an Invisible Digital Signature
<!--Where did the user here make his/her name invisible?  Don't see that step. Tested procedure and I can still see my name in the list of approvers and in the certificate information. Is it because the user didn't insert a signature line?  -->
You can add an _invisible digital signature_ to prevent your name from appearing in a document.  

1. Open your document and click the **File** tab.

2. Click **Info** and then click **Protect Document**.<br/>
![Protect Document]({{site.baseurl}}/img/word-signature-9.png)

3. From the **Protect Document** drop-down menu, click **Add a Digital Signature**.

4. Select a **Commitment Type**, such as _created and approved this document_, and then click **Sign**.<br/>
![Sign Document]({{site.baseurl}}/img/word-signature-10.png)

5. Enter your Smart Card (PIV) PIN and click **OK**.<br/>
![PIV PIN]({{site.baseurl}}/img/word-signature-5.png)

6. _The **Signature Confirmation** box tells you that Word saved your digital signature._ Click **OK**.<br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

<br/>

## Add Multiple Digital Signatures

If two or more approvers need to digitally sign a document, you can use either the _signature line_ or _invisible signature_ method.

### Add Multiple Signatures Using Signature Lines
**<NOTE: Whether the 1st approver creates all signature lines for all approvers and then sends to each one or whether each approver creates his/her own signature line is unclear. Steps seemed to say both.>**
Once you digitally sign a document, you can send it to other approvers for them to digitally sign. (**Note:**&nbsp;&nbsp; The first approver should create the signature lines for all approvers before sending the document to the second approver.)

1. If you are the second (or other) approver, open the document you've received. Double-click your signature line.  
2. From the Word ribbon, select the **Insert** tab and then click **Signature Line** in the **Text** group.<br/><br/>
![Signature Line]({{site.baseurl}}/img/word-signature-1.png)

3. _A **Signature Setup** pop-up box appears._ Enter your information in the text fields and click **OK**<br/>
![Signature Setup]({{site.baseurl}}/img/word-signature-13.png)

4. 4. Double-click the _signature line_ with your name.<br/> <!--Can the first approver create signature lines for all the approvers in advance? Before the 1st sends it to the 2nd and 3rd?--><br/>
![Signature Line]({{site.baseurl}}/img/word-signature-14.png)

5. _A **Sign** pop-up box appears._ At the **X**, type your name. 

6. Next, look at the **Signing as:** field. _You should see your name and certificate information._ If you don't, click the **Change** button to select a different certificate and click **Sign**.<br/>
![Signature Box]({{site.baseurl}}/img/word-signature-4.png)

7. Enter your Smart Card (PIV) PIN and click **OK**..<br/>
![Certificate PIN]({{site.baseurl}}/img/word-signature-5.png)

8. _The **Signature Confirmation** box tells you that Word saved your digital signature._ Click **OK**. <br/>
![Signature Confirm]({{site.baseurl}}/img/word-signature-6.png)

Now you can send the digitally signed document to the next approver. _Each successive approver will be able to open the document and double-click the **Signature Line** with his/her name and complete the signing process._

### Add Multiple Invisible Signatures
**<We don't need to repeat the procedures if we refer them to the previous "Invisible Signature" section. We can delete all but the very last statement: "Final approver will see multiple..." and final screenshot.>**
One or more approvers may sign a document by using the _invisible signature_ method: [Add an Invisible Digital Signature](#add-an-invisible-digital-signature). 

1. Open your document and click the **File** tab.

2. Click **Info** and then click **Protect Document**.<br/>
![Protect Document]({{site.baseurl}}/img/word-signature-9.png)

3. From the **Protect Document** drop-down menu, click **Add a Digital Signature**.

4. Complete the signing steps to add _invisible signatures_. _The final approver will see multiple invisible signatures in the document._
<!--Don't understand how user gets to this screen-->
![View Signature]({{site.baseurl}}/img/word-signature-12.png)

<br/>

## View Digital Signatures

{% include alert-warning.html content="If you use Word 2013 and open digitally signed Word 2007 or 2010 documents, you may encounter compatibility issues." %} 
**<Compatibility issues" means that the signatures will not be there?>**
You can view digital signatures in an incompatible Word document in one of two ways:

1. Click the **View Signatures** button just below the Word ribbon.
![View Signature]({{site.baseurl}}/img/word-signature-16.png)

**OR**

2. Click the **File** tab and select **Info**. Then click **View Signatures**.<br/>
![View Signature]({{site.baseurl}}/img/word-signature-11.png)

For either option, you will be able to see the digital signature details in the **Signatures** box.
![View Signature]({{site.baseurl}}/img/word-signature-17.png)

<br/>

## Remove a Digital Signature
**<Is this correct?>**
1. If you want to remove a digital signature, open your Word document and find the signature line. 
2. If there is no signature line, click the **View Signatures** button just below the Word ribbon.
3. From the **Signatures** box, select the signature you want to to delete.
![View Signature]({{site.baseurl}}/img/word-signature-17.png)

3. Right-click on the signature and then click **Remove Signature**.  
4. When prompted, click **Yes**.

![Remove Signature]({{site.baseurl}}/img/word-signature-8.png)

<br/>

## Change Signature Algorithm

By default, Microsoft Word uses the SHA-1 algorithm to encrypt digital signatures in a Word document. The SHA-1 algorithm is no longer considered secure. Other algorithms, such as SHA-256, are preferred.

{% include alert-info.html content="These instructions require administrator privileges." %} 

Two options are available for setting different signature algorithms: 

1. **Group Policy**<!--Object?--> settings. (See Microsoft TechNet articles on Group Policy settings.**<Provide link>**)
2. **Computer registry** settings. To change a signature algorithm to SHA-256, use the following:

- **Word 2010**: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\14.0\common\signatures
- **Word 2013**: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\15.0\common\signatures
- **Word 2016**: Computer\HKEY_CURRENT_USER\Software\Policies\Microsoft\Office\16.0\common\signatures

Add or update the values as specified below. Then, save the registry settings and restart your computer.

|**Value Name**|signaturehashalg|
|**Value Type**|REG_SZ|
|**Value**|sha256|

{% include alert-info.html content="You can also use even more secure algorithms, such as **SHA-384** or **SHA-512**." %}
 

## Additional Resources

1. [Add or Remove Digital Signature in Office Files](https://support.office.com/en-us/article/add-or-remove-a-digital-signature-in-office-files-70d26dc9-be10-46f1-8efa-719c8b3f1a2d){:target="_blank"}
1. [XML Digital Signature](https://www.w3.org/TR/XAdES/
){:target="_blank"}
1. [Digital Signatures in Office 2010](https://blogs.technet.microsoft.com/office2010/2009/12/08/digital-signatures-in-office-2010/){:target="_blank"}
1. [Digital Signature Settings in Office 2013](https://technet.microsoft.com/en-us/library/cc545900.aspx){:target="_blank"}
