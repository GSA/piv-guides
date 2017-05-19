---
layout: default
title: Basics of a PIV Credential
permalink: /elements/
---

There are two main categories for the features of a PIV credential: [_physical_ features](#physical-features) and [_electronic_ features](#electronic-features).

## Physical Features

![Example of a PIV credential and its physical components]({{site.baseurl}}/img/elements.png){:style="float:left"}

An example of a PIV credential can be seen to the left.

The image shows the standard placement for information such as photograph, name, affiliation, expiration date, organization, and the **chip**.   

PIV credentials also contain at least one security feature that aids in reducing counterfeiting, is resistant to tampering, and provides visual evidence of tampering attempts such as optical varying structures or inks, laser etching, holographic images, and watermarks.  


## Electronic Features
What is the chip on your PIV credential?  In the easiest terms: it is a computer.  It holds information **very securely** and can process data.  The chip is also called a _secure element_.

{% include alert-info.html heading = "Do you have a debit card with a chip or a smartphone with a SIM card?" content="These are both examples of similar technology that we use every day in our daily lives and help us secure information.  You can't use your PIV credential to withdraw money, nor do you use your debit card to login to your computer or Federal applications - but you can see how similar technology is used every day." %}

Most applications that use PIV credentials leverage information stored on the chip and we call this information the _logical elements_.  These elements are defined in the [NIST Special Publication 800-73 series document.](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-73-4.pdf){:target="_blank"}

The following electronic elements authenticate the PIV credential as a Device:  

- **Cardholder Unique Identifier (CHUID)**, which is a digitally signed Federal Agency Smart Card Number (FASC-N) plus other data that can be used.
- **Card Authentication**, which is a certificate and key pair that can be used to verify that the PIV credential was issued by an authorized entity, has not expired, and has not been revoked.

The following electronic elements authenticate YOU as the user:

- **Photograph**, which is stored on the chip, signed digitally and allows a person to confirm that the printed photo on the card has not been altered.
- **Biometric Identity Information** such as fingerprints or iris/eye templates, which can be used to verify you.
- **PIV Authentication**,  which is a certificate and key pair and can be used to verify that the PIV credential was issued by an authorized entity, has not expired, has not been revoked, and holder of the credential (YOU) is the same individual it was issued to.

The following electronic elements are for usage by YOU:

- **Digital Signature**, which is a certificate and key pair allows the YOU to digitally sign a document or email, providing both integrity and non-repudiation.
- **Encryption**, which is a certificate and key pair and allows YOU to digitally encrypt documents or email with your colleagues in the US Federal Government or with government Partners, providing confidentiality through ensuring that only authorized parties can read the document or email.

The Card Authentication, PIV Authentication, Digital Signature, and Encryption all leverage four separate certificates and key pairs, issued from certificate authorities that are audited and certified by the Federal Public Key Infrastructure (FPKI).
