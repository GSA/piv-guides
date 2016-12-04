---
layout: default
title: Getting Started
permalink: /start/
---

You need two items to begin using your PIV credential:

*  A [card reader](#card-readers) (hardware)
*  [Middleware](#middleware) (software) that works with your computer

#### Card Readers
A card reader is exactly what the name suggests: a piece of hardware which helps read the card.

> *A card reader is the hardware that supplies power to the chip, and allows the computer operating system to talk to the PIV credential chip operating system.*

Card readers are available in many shapes and sizes - to fit both the PIV credential, and to plug into your computers.  There is a card reader that will work for any shape and size of the computer you use including card readers for USB and microUSB ports.  There are fold-up readers, there are readers that sit on your desk, there are keyboards with readers, there are readers that connect to tablets, and there are readers built into laptops.

If you need to buy a reader for home use (or many for your agency), you will want to review card readers that specify:

* **ISO 7816** support

You can buy a card reader for personal use from a number of commercial online retailers.  When buying card readers for your agency, you can use [GSA Advantage](https://www.gsaadvantage.gov/) to directly purchase the card readers.

Before you buy a card reader, look around and ensure you don't already have one.  A large portion of government laptops have the card readers already, and desktops may have keyboards with readers built-in.

If you have a Mac OSX or Linux based computer, you probably don't have a card reader built in. Find a card reader option that you like and let's move on to Middleware.

#### Middleware
_Middleware_ as a general computer term can encompass any software that provides integration points for an application. In the Standards for PIV credentials, the term _PIV middleware_ is used and a common question is "What is the difference between PIV Middleware and general smartcard middleware?" To simplify, we'll define the two terms as we use them for PIV credentials in these guides:

*  PIV Middleware:

> _Client side software which implements the full set of application programming interfaces and card functions as specified in NIST Special Publication 800-73-4, and has been certified as compliant to the NIST Special Publication 800-85A series testing procedures.  The PIV compliant middleware implements all lifecycle functions including the ability for a user to perform PIN resets, activation, and renewals. The PIV compliant middleware may also implement common usage functions to support authentication, digital signatures, encryption, and integrations with multiple operating system cryptographic libraries._

*  General smartcard middleware:

> _Client side software which implements common functions for an operating system and cryptographic libraries to interface with PIV credentials or other smartcards for usage.  The general smartcard middleware may implement functions to support authentication, digital signatures, encryption, and integrations with multiple operating system cryptographic libraries._

For common PIV credential usage scenarios, we outline the _general smartcard middleware_ available as open or government source or included in operating systems for use scenarios.  Commercial options for PIV Middleware are available and the list of NIST certified PIV Middleware can be viewed [here on the NIST website](http://csrc.nist.gov/groups/SNS/piv/npivp/validation.html).


| Name              | Operating System and Versions | Support | Considerations |
| -------------             |----|----|----|
| Windows mini-driver       | Windows 7, Windows 8, Windows 10, Windows 2008, Windows 2012  | Yes | Included in Windows operating systems and requires no installation.  Does not include the functionality to perform full lifecycle management of a PIV credential.  Does not support using your PIV credential with non-Microsoft cryptographic service providers such as those used by Mozilla Firefox browser.   |
| OpenSC       | Mac OSX 10.5, Mac OSX 10.6, Mac OSX 10.7, Mac OSX 10.9, Mac OSX 10.10, Windows (32-bit and 64-bit), Linux, *nix versions vary  | Open Source | Open source software.  Limited commercial support for maintenance and patching.  Supports PKCS#11; for example, as used by Mozilla Firefox browser. |
| Smart Card Services   | Mac OSX 10.6, Mac OSX 10.7, Mac OSX 10.9, Mac OSX 10.10  | Open Source  | Open source software. Limited commercial support for maintenance and patching.   |
| CoolKey   | Linux, *nix versions vary  | Open Source  |   |
| CACKey   | Linux, *nix versions vary  | US Government Source  | Available from Forge.mil |
| **Commercial options**   | Varies  | Yes  |  Review support for your usage needs such as email signing, encryption, network authentication, VPNs, and website authentication  |


You may need to consider Network authentication, Virtual Private Network (VPN), email signing, email encryption, document signing, document encryption and website authentication when choosing one or more middleware options for yourself or your users.  In most cases, you can choose a middleware option that works for the most common uses for your purposes or mix and match based on operating systems and devices. 

### Next Steps
You have a PIV credential, you have card reader(s), and you have middleware for your computers. **Now what?**

* You can authenticate to websites that are PIV enabled for authentication, digitally sign email and documents and files, and encrypt!

If you want to learn more about details of PIV credentials, certificates, and how to configure a network or web application, the next [section](../details) is for you.
