---
layout: default
navtitle: Digitally Signing in Microsoft Word - Office of the Federal Register
title: Digitally Sign a Microsoft Word Document - Office of the Federal Register
pubDate: April 27, 2018
collection: userguides
permalink: userguides/signworddoc-ofr/
description: This guide will walk you through the Office of the Federal Register's procedures for digitally signing a Microsoft Word document with invisible digital signatures using your PIV credential or similar digital certificate.
---

The digital signatory of a document MUST be the same person whose name is typed in the signature block.  The names must match exactly or meet the accepted standards listed in the Office of the Federal Register's _Document Drafting Handbook_, Chapter 1.  To verify the name as applied to the digital certificate, follow the instructions below in the [View Signature Certificate](#view-signature-certificate) section.

By using the native Microsoft Word digital-signing capability, it will apply your Public Key Infrastructure (PKI) certificate to the document, guaranteeing the authenticity of the signer and the document.  Once applied, your document is protected and cannot be edited without removing the digital signature.  (**Note:**&nbsp;&nbsp;The Microsoft Word digital-signing process saves the signed document under the same filename.)

Do NOT use the Insert Signature function (under the **INSERT** tab in the Microsoft Word ribbon).  Follow the instructions below to invisibly sign your document (i.e., add an invisible signature), as this is the format that OFR will accept.

- [Add Invisible Digital Signatures](#add-invisible-digital-signatures)
- [Multiple Digital Signatories](#multiple-digital-signatories)
- [Remove Invisible Digital Signatures](#remove-invisible-digital-signatures)
- [View Signature Certificate](#view-signature-certificate)

## Add Invisible Digital Signatures

1. Open your Microsoft Word document.
2. Insert your PIV card into your card reader. 
3. Click the **File** tab.
4. Click **Info**. 
5. Click **Protect Document**.
6. From the drop-down list, click **Add a Digital Signature**.

![Add Dig Sign]({{site.baseurl}}/img/ofr_word_add_digital_signature_1.PNG){:style="width:60%;"}

In the **Sign** dialog box: 

![OFR Sign Box]({{site.baseurl}}/img/ofr_sign_box_with_no_name_2.PNG){:style="width:50%;"}

1. Select a **Commitment Type** from the pull-down menu.
2. In the **Purpose for signing this document**, type the purpose or leave blank.
3. Click **Change** if you need to change the signer.
4. Click **Sign**.
5. Follow the prompt to enter your **PIN**, and then click **OK**.

![Enter Your PIN]({{site.baseurl}}/img/ofr_enter_your_pin_3.png){:style="width:40%;"}

If the digital signature certificate and PIN are valid, the document is signed and automatically saved under the same filename.  This is the file that you submit to OFR via the web portal.

For multiple-signatory documents (e.g., dual-agency submissions), the first signer forwards the signed document to the next signer, who repeats the signing process for the already-signed file.  (See the [Multiple Digital Signatories](#multiple-digital-signatories) section.)  All digital signatories' names and job titles must appear in the signature block of the document. 

A digital signature can be removed if necessary.  This might be handy if last-minute changes are needed or if a different signatory is desired. If the digital signature has been removed, remember that the document will have to be re-signed prior to submission to OFR.  (See [Remove Invisible Digital Signatures](#remove-invisible-digital-signatures) section.)

## Multiple Digital Signatories

Multi-agency digital submissions are not only possible but recommended.  Exactly like paper-and-disk submissions&mdash;if multiple agencies are submitting a document for publication, OFR receives only one document, signed by all agencies.  For example, if six agencies are jointly issuing a rule, OFR does NOT get six submissions of the same rule.  Regardless of the method of submission, the legal requirements are the same (i.e., representatives from all of the issuing agencies must sign the document, per DDH, Chapter 1.6).  If one or more of the agencies are unable or unwilling to digitally sign the document, it must be submitted via the conventional paper-and-disk procedure described in the DDH.

One of the issuing agencies should serve as the primary or lead coordinating agency. For jointly-issued digitally-signed documents, follow these steps:

1. Save the final version of the document as a Microsoft Word file (*.docx).  Be sure that the digital signatories’ names and job titles are pre-printed in the signature block section of the document.
2. Coordinate among the issuing agencies the sequence of signing (i.e., the agency that signs first forwards the signed file on for the next signature.  Determine which agency will actually submit the signed file to OFR via the web portal once all signatures are completed.
3. The representative from the first agency digitally signs the file using the same method as a single-agency submission. (See [Add Invisible Digital Signatures](#add-invisible-digital-signatures).)  All signers must ensure that their names and job titles are pre-printed in the signature block section of the document.
4. Email that signed file to the next agency for digital signature. 
5. The representative from the next agency in sequence ensures that his/her name and job title is pre-printed in the signature block section of the document and then digitally signs the already-signed file.  No changes can be made to the signed file without removing the existing signature(s).  If changes are required to the Microsoft Word document, the whole process starts anew with the corrected, unsigned Word document.
6. If additional issuing agencies must sign the document, repeat steps 4 and 5 until all agencies have digitally signed it. 
7. Once all agency signatures have been applied to the file, the file is sent to the agency that will submit it to OFR via the web portal.  From OFR’s perspective, it doesn’t matter who submits the file; we’re concerned with validating the digital signatories.
8. The sending agency should include a special handling letter alerting OFR of the multi-agency submission with several signatories.  Be sure that the special handling letter is digitally signed as well.  One signer is sufficient for the special handling letter.
9. The sending agency logs into the web portal, uploads the signed Microsoft Word file and special handling letter and submits.
10. The signatures are validated in the web portal.  We will also check each digital signatory against their printed signature block in the document.  The names must match exactly or meet the accepted standards listed in the DDH. (See Step 1.)

## Remove Invisible Digital Signatures

Open the Microsoft Word document that contains the invisible signature you want to remove.

![Doc Invisible Signatures]({{site.baseurl}}/img/ofr_remove_invisible_sign_4.png){:style="width:65%;"}

1. In the header, you may see the option to **View Signatures**.  Click that button and proceed to step 5; otherwise:
2. Click the **File** tab.
3. Click **Info**.
4. Click **View Signatures**. 
_The **Signatures** pane appears._

![Signatures Pane]({{site.baseurl}}/img/ofr_signatures_pane_5.png){:style="width:90%;"}&nbsp;

6. Next to the signature name, click the drop-down arrow.
7. Click **Remove Signature**.
8. Click **Yes**.

## View Signature Certificate

You can check the details of the digital certificate(s) used to sign a Microsoft Word document (e.g., the name assigned to the certificate or expiration date).

Open the signed Word document containing the certificate(s) you want to check, or have the signer sign a document via the instructions provided in the [Add Invisible Digital Signatures](#add-invisible-digital-signatures) section.

1. In the header, you may see the option to **View Signatures**.  Click that button and proceed to step 5; otherwise:
2. Click the **File** tab.
3. Click **Info**.
4. Click **View Signatures**.
5. In the **Signatures** pane, hover over the signer's name that you want to check, and then click the drop-down arrow.
6. Click on **Signature Details**. _The signer’s name, as applied to the certificate, is listed, along with the Certification Authority (CA)._  
7. Click the **View** button.  _A pop-up window appears._
8. Ensure that the **General** tab is selected. _The valid dates of the certificate are listed. More technical details, such as the certification path and key usage values, are shown under other tabs._


