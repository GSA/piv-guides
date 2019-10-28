---
layout: default
navtitle: Digitally Sign a Microsoft Word Document
title: Digitally Sign a Microsoft Word Document
pubDate: March 23, 2018
collection: userguides
permalink: userguides/signworddoc/
description: This guide will walk you through the steps for digitally signing a Microsoft Word document with your PIV credential or similar digital certificate.
---

You can add visible (those included with a signature line) or invisible digital signatures to MS Word documents.

In this section, you'll find instructions for the following procedures:

- [Add a Digital Signature Via a Signature Line](#add-a-digital-signature-via-a-signature-line)
- [Add an Invisible Digital Signature](#add-an-invisible-digital-signature)
- [Add Multiple Digital Signatures](#add-multiple-digital-signatures)
- [Verify Your Signing Certificate](#verify-your-signing-certificate)

## Add a Digital Signature Via a Signature Line

1. Open the document you want to sign in MS Word, and save any changes.
2. Insert your Federal Government-issued Personal Identity Verification (PIV) card into your card reader.
3. On the **Insert** tab, in the **Text** group, click **Signature Line**.

    ![Signature Setup]({{site.baseurl}}/img/SignatureSetup.png)

4. Type your information, then click **OK**.

    The signature line appears in the document.
    
    ![Signature Line]({{site.baseurl}}/img/SignatureLine.png)

5. Double-click the signature line.

    The **Sign** window appears.
    
6. (Optional) If you want to verify that you selected the correct certificate, follow the [Verify Your Signing Certificate](#verify-your-signing-certificate) instructions on this page.
7. Click **Sign**.
8. Follow the prompt to enter your PIN, then click **OK**.

    If the digital signature and PIN are valid, the document is signed and saved with the same file name.

## Add an Invisible Digital Signature

{% include alert-info.html content="This is the only type of digital signature that is accepted by the Office of the Federal Register (OFR) web portal." %}

1. Open the document that you want to sign in MS Word, and save any changes.

    If you have a purchased PKI credential installed on your computer, proceed to step 3.

2. Insert your Federal Government-issued PIV card into your card reader.
3. In the ribbon, click **File**.
4. In the left bar, click **Info**.

    ![Add Digital Signature]({{site.baseurl}}/img/AddDigitalSignature.png)
    
5. Click **Protect Document** > **Add a Digital Signature**.

    The **Sign** window appears.
    
    ![Sign Window]({{site.baseurl}}/img/SignWindow.png)
    
6. In the **Commitment Type** box, select the nature of your involvement with the document.
7. In the **Purpose for signing this document** box, enter an optional short description.
8. (Optional) If you want to verify that you selected the correct certificate, follow the [Verify Your Signing Certificate](#verify-your-signing-certificate) instructions on this page.
9. Click **Sign**.
10. Follow the prompt to enter your PIN, then click **OK**.

    If the digital signature and PIN are valid, the document is signed and asved with the same file name.
    
{% include alert-success.html heading = "Lesson Learned" content="If you want to sign multiple documents without having to reenter your pin, keep MS Word open and your PIV card in the card reader between signing each document." %}

## Add Multiple Digital Signatures

These steps describe how to add multiple digital signatures to a document, for example, if multiple agencies need to sign one jointly-issued document to submit to OFR.

In this process, signatory 1 signs and sends the document to signatory 2, who signs and sends the document to signatory 3, and so on. One of the signatories should serve as the lead coordinator.

{% include alert-info.html content="Making a change to a digitally signed document removes any prior signatures. If you need to make any changes after any parties have digitally signed the document, you'll have to restart the signing process from scratch." %}
    
1. Coordinate the order of signatures among all the signatories.
2. In MS Word, signatory 1 should create a signature line for each subsequent signatory (steps 1-4 of [Add a Digital Signature Via a Signature Line](#add-a-digital-signature-via-a-signature-line)), and save the final version of the document as a .docx file.
3. Signatory 1 digitally signs the document using one of the following processes:

    a. [Add a Digital Signature Via a Signature Line](#add-a-digital-signature-via-a-signature-line)
    b. [Add an Invisible Digital Signature](#add-an-invisible-digital-signature)
    
4. Signatory 1 sends that signed document to signatory 2.

    Each signatory follows steps 3 and 4 until all issuing agencies have digitally signed the document.
    
If your agency is submitting a jointly-issued document to OFR via the web portal, follow the instructions for submitting a signed document on the [OFR Submission Guidelines]({{site.baseurl}}/userguides/signworddoc-ofr/) page.
    
## Verify Your Signing Certificate

You want to ensure that you use the correct certificate when you sign a document. Use these steps to confirm your signing certificate.

1. When you sign a document using any of the methods above, you'll see the **Sign** window.

    ![Sign Window]({{site.baseurl}}/img/SignWindow.png)
    
2. Click **Change**.

    The **Windows Security** window appears.
    
3. In the list of certificates, select the first unexpired certificate with your name.

    ![Certificate List]({{site.baseurl}}/img/CertificateList.png)
    
4. Click **Click here to view certificate properties**.

    The **Certificate Details** window appears.
    
5. Click the **Details** tab.

    The value for the **Key Usage** field should include **Digital Signature** at a minimum or **Digital Signature, Non-Repudiation**. If this is not the correct certificate, go to step 3 and follow these steps with a different certificate.
    
    ![Signature Details]({{site.baseurl}}/img/SignatureDetails.png)
    
6. Click **OK**.
