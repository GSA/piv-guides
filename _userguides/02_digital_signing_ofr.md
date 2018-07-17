---
layout: default
navtitle: Digitally Signing Documents for Submission to Office of the Federal Register
title: Digitally Signing Documents for Submission to Office of the Federal Register
pubDate: July 17, 2018
collection: userguides
permalink: userguides/signworddoc-ofr/
description: This guide will walk you through the procedures for digitally signing a Microsoft Word document for submission to the Office of the Federal Register using your PIV credential or similar digital certificate.
---

The digital signatory of a document MUST be the same person whose name is typed in the signature block.  The names must match exactly or meet the accepted standards listed in the DDH, Ch. 1.  To verify the name as applied to the digital certificate, follow the instructions below in the [View Signature Certificate in MS Word](#view-signature-certificate-in-ms-word) section.

Using the native Microsoft (MS) Word signing capability applies your Public Key Infrastructure (PKI) certificate to the document, guaranteeing the authenticity of the signer and the document.  Once applied, your document is protected and cannot be edited without removing the digital signature. The MS Word signing process saves the signed document _under the same filename_!

Use MS Word 2010 or later. Only submit ".docx" file types. Older versions of MS Word have no standard method to validate digital signatures.  The old file type ".doc" is not compatible with OFR's digital validation process and is not accepted in the web portal.

Do NOT use the _Insert Signature_ function (under the **INSERT** tab in the **Word** ribbon).  Follow the instructions below to sign the document invisibly as this is the format OFR will accept.

## Add Invisible Digital Signatures in MS Word

{% include alert-warning.html content = "IMPORTANT: The following instructions apply to MS Word 2013. The signing process for other MS Word versions (e.g., 2010, 2016, Office 365) may vary somewhat. If you have trouble with the signing process, contact OFR at ofrtechgroup@gpo.gov or (202) 741-6020 or your IT support." %}

1. Open your MS Word document in Word. Any changes must be saved before signing.
2. If you have a purchased PKI credential installed on your computer, proceed to Step 3. Otherwise, insert your Federal Government-issued Personal Identity Verification (PIV) card into your card reader.
3. Click the **File** tab.<br />
   ![Add Dig Sign]({{site.baseurl}}/img/ofr_word_add_digital_signature_1.PNG){:style="width:70%;"}
4. Click **Info**.
5. Click **Protect Document**.
6. Click **Add a Digital Signature**.
7. In the **Sign** dialog box:<br />
   ![OFR Sign Box]({{site.baseurl}}/img/ofr_sign_box_with_name_appears_here_3.png){:style="width:75%;"}
8. Select a **Commitment Type** from the pull-down menu.
9. In the **Purpose for signing this document**, type the purpose or leave blank.
10. To ensure the correct certificate is used, click the **Change** button.
11. In the Certification Selection box, there may be multiple certificates.  Select the first **unexpired** certificate with your name;  then _Click here to view the certificate properties_.<br />
    ![OFR Windows Security Certificate Type]({{site.baseurl}}/img/ofr_windows_sec_piv_or_purch_cert.png){:style="width:80%;"}  
12. The **Certificate Details** box appears. Go to the _Details_ tab and scroll down to _Key Usage_.  Single-click on it.  The lower text box should now display “Digital Signature, Non-Repudiation” (for PIV card certificate) or “Digital Signature” (for a purchased certificate).  If it does, then this is the right certificate. Click **OK** to close the window and proceed with signing.<br />
    ![OFR Certificate Details]({{site.baseurl}}/img/ofr_certificate_details.png){:style="width:60%;"} 
13. If this is the wrong certificate, click **OK**. Then select another certificate and repeat these steps until you find the correct certificate.
14. Click **Sign**.
15. Follow the prompt to enter your **PIN**; then click **OK**.<br />
    ![OFR Enter Your PIN]({{site.baseurl}}/img/ofr_enter_your_pin_3.png){:style="width:58%;"}
16. If the digital signature certificate and PIN are valid, the document is signed and automatically saved _under the same filename!_  This is the file you submit to OFR via the web portal.<br />
    ![OFR Signature Confirmation]({{site.baseurl}}/img/ofr_signature_confirmation.png){:style="width:58%;"}

If you are signing multiple documents, leave MS Word open and your PIV card inserted to sign without having to re-enter your PIN for each file.

For multiple-signatory documents (e.g., dual-agency submissions), the first signer forwards the signed document to the next signer, who repeats the signing process on the _already-signed file_. See the [Multiple Digital Signatories in MS Word](#multiple-digital-signatories-in-ms-word) section below.  All digital signatories must have their names and titles typed into a separate signature block in the signature block area of the document. 

A digital signature can be removed if necessary.  This might be handy if last-minute changes are needed or if a different signatory is desired. Remember that the document will have to be re-signed prior to submission to OFR.  See [Remove Invisible Digital Signatures in MS Word](#remove-invisible-digital-signatures-in-ms-word) below.

## Multiple Digital Signatories in MS Word

Multi-agency digital submissions are not only possible but recommended.  Exactly like paper-and-disk submissions, if multiple agencies are submitting a document for publication, OFR receives only one document, signed by all agencies. For example, if six agencies are jointly issuing a rule, OFR does NOT get six submissions of the same rule.  Regardless of the method of submission, the legal requirements are the same; i.e., representatives from all issuing agencies must sign the document (DDH, 1.6).  If one or more of the agencies are unable or unwilling to digitally sign, the document must be submitted via the conventional paper-and-disk procedure (DDH).

One of the issuing agencies should serve as the primary or lead coordinating agency. Follow these steps for jointly-issued, digitally-signed documents:

1. Save the finalized version of the document as an MS Word file (.docx).  Be sure that the digital signatories’ names and job titles are pre-inserted in the signature block area of the document.
2. Coordinate among the issuing agencies the sequence of signing; i.e., who signs first and forwards the signed file on for the next signature.  Determine which agency will actually submit the signed file to OFR via the web portal once all signatures are completed.
3. The representative from the first agency digitally signs the file using the same method as a single-agency submission. See [Add Invisible Digital Signatures in MS Word](#add-invisible-digital-signatures-in-ms-word) above.  All signers must ensure that their names and job titles are pre-inserted in the signature block area of the document.
4. Email that **signed** file to the next agency for digital signature. 
5. The representative from the next agency in sequence ensures that their name and job title are pre-inserted in the signature block area of the document and then digitally signs the _already-signed_ file.  No changes can be made to the signed file without removing the existing signature(s). If changes are required to the MS Word document, the whole process starts anew with the corrected, unsigned Word document.
6. If there are more issuing agencies, repeat Steps 4 and 5 until all agencies have digitally signed. 
7. Once all agency signatures have been applied to the file, the file is sent to the agency that will submit it to OFR via the web portal.  From OFR’s perspective, it doesn’t matter who submits the file; we’re concerned with validating the digital signatories.
8. The sending agency should include a special handling letter alerting OFR of the multi-agency submission with several signatories.  Be sure the special handling letter is digitally signed as well.  One signer is sufficient for the special handling letter.
9. The sending agency logs into the web portal, uploads the signed MS Word file and special handling letter, and submits.
10. The signatures are validated in the web portal.  We will also check all digital signatories against their printed signature block in the document.  The names must match exactly or meet the accepted standards listed in the DDH. (See Step 1.)

## Remove Invisible Digital Signatures in MS Word

1. Open the MS Word document that contains the invisible signature you want to remove.<br />
   ![Doc Invisible Signatures]({{site.baseurl}}/img/ofr_remove_invisible_sign_4.png){:style="width:90%;"}
2. In the header, you may see the option to **View Signatures**.  Click that button and proceed to Step 5. Otherwise:
3. Click the **File** tab.
4. Click **Info**.
5. Click **View Signatures**. The **Signatures** pane appears.<br />
   ![Signatures Pane]({{site.baseurl}}/img/ofr_signatures_pane_5.png){:style="width:120%;"}
6. Next to the signature name, click the arrow.
7. Click **Remove Signature**.
8. Click **Yes**.

## View Signature Certificate in MS Word

You can check the details of the digital certificate(s) used to sign an MS Word document (e.g., the name assigned to the certificate or expiration date).

Open the signed MS Word document containing the certificate(s) you want to check, or have the signer sign a document via the instructions provided in the [Add Invisible Digital Signatures in MS Word](#add-invisible-digital-signatures-in-ms-word) section above.

1. In the header, you may see the option to **View Signatures**.  Click that button and proceed to Step 5. Otherwise:
3. Click **Info**.
4. Click **View Signatures**. The **Signatures** pane appears.
5. In the **Signatures** pane, hover on the name of the signer you want to check; then click the small down arrow.
6. Click on **Signature Details**. 
7. The signer’s name as applied to the certificate is listed, along with the Certification Authority (CA). Click the **View** button.  
8. A pop-up window appears. Be sure that the **General** tab is selected. The valid dates of the certificate are listed. More technical details, such as the certification path and key usage values, are shown under other tabs.  

## FAQs

### We’ve been using the free GSA Digital Signing Tool to sign documents.  Do we need to change?
Not right away, but you need to follow the provided instructions to adopt the MS Word signing procedures sooner rather than later.  The GSA Digital Signing Tool is no longer supported and may malfunction.

### Will the portal accept both “p7m” and “.docx” files?
Yes, for the time being.  Many agencies still use the signing process that creates a “p7m” file for submission via the portal.  Since we will accept signed MS Word files with the “.docx” extension, the portal has been configured to accept both on an interim basis.

### So “p7m” files will eventually stop being accepted?
Exactly.  OFR encourages agencies to make the procedural migration to MS Word signing as soon as possible.

### When will you stop accepting “p7m” files?
The end of FY2018, September 30.  We’ll give plenty of advance notice, including a blurb on the portal website.

### But “p7m” files are how we do it now.  It’s worked for years; why change?
The signing process that creates the “p7m” file was adopted more than a decade ago as OFR’s technical and legal standard for ensuring the validity of submissions.  Now, the software used to create the “p7m” file is no longer updated or supported; subsequently, it is failing.  One of the options under consideration was procuring ongoing technical support for the software, an option that would easily run into hundreds of thousands of taxpayer dollars over the next few years.  However, technological and security improvements in MS Word allow OFR to adopt the native MS Word signing function as the secure standard for digitally signed documents.

### I don’t get it.  What’s a “p7m” file?
If you don’t know, don’t worry about it.  Just follow the provided instructions to sign using MS Word.

### What special software do we need to buy and install to make this work?
None.  As a federal agency, you should already have MS Office 2010 or later installed.  Simply follow the provided instructions to digitally sign your documents. 

### Do you accept any MS Word file?
No. Your file must be saved as an XML-based MS Word document (".docx"). If you're using MS Word 2010 or later, this is generally the default setting. Otherwise, when you save the file, choose "Word Document" (.docx) in the "Save as type" pull-down.

### We save everything as a ".doc" file and/or we're still using MS Word 2007 (or earlier). What are our options?
Paper-and-disk submission. Don't forget the CD and the signed certification letter!

### All we need is MS Word 2010 or later?
Yes, that and your signing credential, either the one on your PIV card or the one your agency purchased that is currently installed on your computer.  

### We purchased our signing certificates from GPO or another vendor.  We use them to sign, which creates the "p7m" file.  What do we do now?
If you are using purchased certificates, such as from an Entrust vendor, you can continue to use them.  Instead of being on a PIV card, your certificate is installed on your computer.  Follow the [Add Invisible Digital Signatures in MS Word](#add-invisible-digital-signatures-in-ms-word) instructions above to sign your MS Word file.

### How do I identify the Purchased Certificates and PIV Card Certificates when signing a document?
When checking for the correct certificate, as detailed in Step 7 of the [Add Invisible Digital Signatures in MS Word](#add-invisible-digital-signatures-in-ms-word) instructions above, note the different icons for the PIV and purchased certificates:<br/>
![Certificate Type Icons]({{site.baseurl}}/img/ofr_certificate_types.png){:style="width:40%;"}

### Some of our signers use MS Word for Apple on iPad.  Will this work for PKI submission?
Microsoft has not put that function (PKI-based digital signature) into the MS Word for Mac (Office for Mac) software.  We recognize that some agencies have signers who use the Mac platform. We expect to run testing when this function becomes available.  

### I already have a web portal submission account.  Do I need to update it or reapply?
No.
