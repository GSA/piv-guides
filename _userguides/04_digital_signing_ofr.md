---
layout: default
navtitle: OFR Submission Guidelines
title: OFR Submission Guidelines
pubDate: July 17, 2018
collection: userguides
permalink: userguides/signworddoc-ofr/
description: This guide will walk you through the procedures for digitally signing a Microsoft Word document for submission to the Office of the Federal Register using your PIV credential or similar digital certificate.
---

This guide describes how you'll need to prepare and digitally sign a document to submit to the Office of the Federal Register (OFR).

## OFR Requirements

The name of a digital signatory must match the name typed in the signature block, or meet the accepted standards in the [Document Drafting Handbook (DDH)](https://www.archives.gov/files/federal-register/write/handbook/ddh.pdf){:target="_blank"}, chapter 1.6.

Use MS Word 2010 or later, and submit only *.docx* files. Older versions of MS Word lack a standard method to validate digital signatures, and the old file type *.doc* is not compatible with OFR's digital validation process, and not accepted in the web portal.

If multiple agencies submit a document for publication, they must submit one document that is signed by a representative from every issuing agency (DDH, 1.6). If one or more agencies are unable or unwilling to digitally sign, then the document must be submitted via the conventional paper-and-disk procedure (DDH, 6.3),

{% include alert-info.html content="The OFR web portal accepts only invisible digital signatures on MS Word documents. For instructions, see [Add an Invisible Digital Signature]({{site.baseurl}}/userguides/signworddoc/)." %}

## Submit a Jointly-Issued Document to OFR

If multiple agencies are submitting a document for publication, OFR recommends submitting one document that is digitally signed by every issuing agency.

In this process, signatory 1 signs and sends the document to signatory 2, who signs and sends the document to signatory 3, and so on. One of the signatories should serve as the lead coordinator.

{% include alert-info.html content="Making a change to a digitally signed document removes any prior signatures. If you need to make any changes after any parties have digitally signed the document, you’ll have to restart the signing process from scratch." %}

1. Coordinate the order of signatures among all the signatories.
2. In MS Word, signatory 1 should create a signature line for each subsequent signatory (steps 1-4 of [Add a Digital Signature Via a Signature Line]({{site.baseurl}}/userguides/signworddoc/)), and save the final version of the document as a .docx file.
3. Signatory 1 digitally signs the document using the process in [Add an Invisible Digital Signature]({{site.baseurl}}/userguides/signworddoc/).
4. Signatory 1 sends the signed document to signatory 2.
      Each signatory follows steps 3 and 4 until all issuing agencies have digitally signed the document.

{% include alert-info.html content="All signatories must confirm their names and titles appear in the signature block area of the document." %}

After all of the issuing agencies have signed the document, the lead coordinating agency submits the document to OFR via the web portal. The corrdinating agency should include a special handling letter that alerts OFR of the multi-agency submission with multiple signatories. Ensure the special handling letter is digitally signed by at least one party.

If you need assistance with digital signatures in MS Word, contact OFR at <ofrtechgroup@gpo.gov> or (202) 741-6020.

## Frequently Asked Questions

### We've been using the free GSA Digital Signing Tool to sign documents. Do we need to change?

Not right away, but you need to adopt the MS Word signing procedures sooner rather than later. The GSA Digital Signing Tool is no longer supported and may malfunction.

### Will the portal accept both *.p7m* and *.docx* files?

No. The portal accepts only signed MS Word files with the *.docx* extension. OFR stopped accepting *.p7m* files at the end of FY2018.

### What special software do we need to buy and install to make this work?

None. As a federal agency, you should already have MS Office 2010 or later installed. Simply follow the provided instructions to digitally sign your documents.

### Do you accept any MS Word file?

No. Your file must be saved as an XML-based MS Word document (*.docx*). If you're using MS Word 2010 or later, this is generally the default setting. Otherwise, when you save the file, in the **Save as type** drop-down, select **Word Document (*.docx)**.

### We save everything as a *.doc* file and/or we're still using MS Word 2007 (or earlier). What are our options?

Paper-and-disk submission (DDH, 6.3). Don't forget the CD and the signed certification letter?

### All we need is MS Word 2010 or later?

Yes, that and your signing credential, either the one on your PIV card or the one your agency purchased that is currently installed on your computer.

### We purchased our signing certificates from GPO or another vendor. We use them to sign, which creates the **.p7m** file. What do we do now?

If you use purchased certificates, such as from an Entrust vendor, you can continue to use them. Simply select the purchased certificate from the list in step 9 of [Add an Invisible Digital Signature]({{site.baseurl}}/userguides/signworddoc/.

### How do I identify the Purchased Certificates and PIV Card Certificates when signing a document?

In step 9 of [Add an Invisible Digital Signature]({{site.baseurl}}/userguides/signworddoc/, in the **Windows Security** window, you can identify certificate types using the corresponding icons. These icons may vary depending on your operating system.

![Certificate Icons]({{site.baseurl}}/img/CertificateIcons.png)

### Some of our signers use MS Word for Apple on iPad. Will this work for PKI submission?

MS Word for Mac does not support PKI-based digital signatures, however, we expect to run testing when this function becomes available.

### I already have a web portal submission account. Do I need to update it or reapply?

No.
