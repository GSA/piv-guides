---
layout: default
navtitle: Digitally Signing in Microsoft Word - Office of the Federal Register
title: Digitally Sign a Microsoft Word Document
pubDate: April 27, 2018
collection: userguides
permalink: userguides/signworddoc-ofr/
description: This guide will walk you through the Office of the Federal Register's procedures for digitally signing a Microsoft Word document with invisible digital signatures using your PIV credential or similar digital certificate.
---

**OFR WRITE-UP STARTS HERE**

The digital signatory of a document MUST be the same person whose name is typed in the signature block.  The names must match exactly or meet the accepted standards listed in the Office of the Federal Register's _Document Drafting Handbook_, Chapter 1.  To verify the name as applied to the digital certificate, follow the instructions below in the “View signature certificate in Word” section.

By using the native MS Word signing capability, it applies your Public Key Infrastructure (PKI) certificate to the document, guaranteeing the authenticity of the signer and the document.  Once applied, your document is protected and cannot be edited without removing the digital signature.  The Microsoft Word signing process saves the signed document under the same filename!

Do NOT use the Insert Signature function (under the INSERT tab in the Word ribbon).  Follow the instructions below to invisibly sign the document (i.e., add an invisible signature), as this is the format that OFR will accept.

- [Add Invisible Digital Signatures](#add-invisible-digital-signatures)
- [Multiple Digital Signatories](#multiple-digital-signatories)
- [Remove Invisible Digital Signatures](#remove-invisible-digital-signatures)
- [View Signature Certificate](#view-signature-certificate)

## Add Invisible Digital Signatures

1. Open your MS Word document in Word.
2. Insert PIV card into card reader. 
3. Click the **File** tab.
4. Click **Info**. 
5. Click **Protect Document**.
6. Click **Add a Digital Signature**.


**INSERT IMAGE-- INFO -- drop-down PROTECT DOCUMENT -> ADD A DIGITAL SIGNATURE**


7. In the **Sign** dialog box: 

![OFR Sign Box]({{site.baseurl}}/img/ofr_sign_box_no_name_2.png){:style="width:55%;float:left;"}

- Select a **Commitment Type** from the pull-down menu.
- In the **Purpose for signing this document**, type the purpose or leave blank.
- Click **Change** if you need to change the signer.
- Click **Sign**.
- Follow the prompt to enter your **PIN**, and then click **OK**.


**INSERT PIV CARD INSERTION DIALOG (WINDOWS SECURITY BOX)**

If the digital signature certificate and PIN are valid, the document is signed and automatically saved under the same filename!  This is the file you submit to OFR via the web portal.

For multiple-signatory documents (e.g., dual-agency submissions), the first signer forwards the signed document to the next signer, who repeats the signing process on the already-signed file.  See **Multiple digital signatories** section below.  All digital signatories must have their names and titles typed in the signature block of the document. 

A digital signature can be removed if necessary.  This might be handy if last-minute changes are needed or if a different signatory is desired.  Remember that the document will have to be re-signed prior to submission to OFR.  See “Remove invisible digital signatures in Word” section below.

## Multiple Digital Signatories

Multi-agency digital submissions are not only possible but recommended.  Exactly like paper-and-disk submissions, if multiple agencies are submitting a document for publication, OFR only receives one document, signed by all agencies.  For example, if six agencies are jointly issuing a rule, OFR does NOT get six submissions of the same rule.  Regardless of the method of submission, the legal requirements are the same; i.e., representatives from all the issuing agencies must sign the document (DDH 1.6).  If one or more of the agencies are unable or unwilling to digitally sign, the document must be submitted via the conventional paper-and-disk procedure described in the DDH.

One of the issuing agencies should serve as the primary or lead coordinating agency.  Follow these steps for jointly-issued digitally-signed documents:

1. Save the finalized version of the document as an MS Word file (*.docx).  Be sure that the digital signatories’ names and job titles are pre-printed in the signature block section of the document.
2. Coordinate among the issuing agencies the sequence of signing; i.e., who signs first and forwards the signed file on for the next signature.  Determine which agency will actually submit the signed file to OFR via the web portal once all signatures are completed.
3. The representative from the first agency digitally signs the file using the same method as a single-agency submission; see “Add invisible digital signatures in Word” above.  All signers must ensure that their names and job titles are pre-inserted in the signature block area of the document.
4. Email that signed file to the next agency for digital signature. 
5. The representative from the next agency in sequence ensures that their name and job title are pre-inserted in the signature block of the document, then digitally signs the already-signed file.  No changes can be made to the signed file without removing the existing signature(s).  If changes are required to the Word document, the whole process starts anew with the corrected unsigned Word document.
6. If there are more issuing agencies, repeat steps 4 and 5 until all agencies have digitally signed. 
7. Once all agency signatures have been applied to the file, the file is sent to the agency that will submit it to OFR via the web portal.  From OFR’s perspective, it doesn’t matter who submits the file; we’re concerned with validating the digital signatories.
8. The sending agency should include a special handling letter alerting OFR of the multi-agency submission with several signatories.  Be sure the special handling letter is digitally signed as well.  One signer is sufficient for the special handling letter.
9. The sending agency logs into the web portal, uploads the signed MS Word file and special handling letter, and submits.
10. The signatures are validated in the web portal.  We will also check each digital signatory against their printed signature block in the document.  The names must match exactly or meet the accepted standards listed in the DDH. (See Step 1.)

## Remove Invisible Digital Signatures

Open the Microsoft Word document that contains the invisible signature you want to remove.

**INSERT MS WORD RIBBON SCREEN CAPTURE THAT SHOWS FILE->MARKED AS FINAL (YELLOW) AND SIGNATURES (YELLOW)**

1. In the header, you may see the option to **View Signatures**.  Click that button and proceed to Step 5.
Otherwise:
2. Click the **File** tab.
3. Click **Info**.
4. Click **View Signatures**.
5. The **Signatures** pane appears.

**INSERT MS WORD RIBBON SCREEN CAPTURE WITH SIGNATURES PANE TO RIGHT OF DOC VIEW**


6. Next to the signature name, click the **drop-down arrow**.
7. Click **Remove Signature**.
8. Click **Yes**.

## View Signature Certificate

You can check the details of the digital certificate(s) used to sign a Microsoft Word document (e.g., the name assigned to the certificate or expiration date).

Open the signed MS Word document containing the certificate(s) you want to check, or have the signer sign a document via the instructions provided in the “Add invisible digital signatures in Word” section above.

1. In the header, you may see the option to **View Signatures**.  Click that button and proceed to Step 5.  
Otherwise:
2. Click the **File** tab.
3. Click **Info**.
4. Click **View Signatures**.
5. In the **Signatures** pane, hover over the name of the signer you want to check, and then click the drop-down arrow.
6. Click on **Signature Details**.
_The signer’s name as applied to the certificate is listed, along with the Certification Authority (CA)._  
7. Click the **View** button.
_A pop-up window appears._
8. Enure that the **General** tab is selected. _The valid dates of the certificate are listed._
_More technical details, such as the certification path and key usage values, are shown under other tabs._






------------------------------------------------------


OUR COPIED WRITE-UP IS BELOW IF NEEDED FOR WORK-IN-PROGRESS REUSE

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

