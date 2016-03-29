---
layout: page
title: Getting Started
permalink: /start/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Introduction</em>
</div>
</div>

You have a PIV credential and the next question is: **What do I need so I can use my PIV credential?**

To begin using your PIV credential, you need two items:  

*  A card reader (hardware)  
*  A driver (software) that works with your computer

#### Card Readers
A card reader is exactly what the name suggests: a piece of hardware which helps read the card.   

> *A card reader is the hardware that supplies power to the chip, and allows the computer operating system to talk to the PIV credential chip operating system.*

Card readers are available in many shapes and sizes - to fit both the credential, and to plug into your computers.

  * Do you have USB ports?
  * Do you have microUSB?
  * Do you have PMCIA slots?

There is a card reader that will work for any shape and size of the computer you would like to use.  There are fold-up readers, there are readers that sit on your desk, there are readers built into keyboards, and there are readers built into laptops.  

If you're new to using PIV credentials and need to buy a reader for home (or many for your agency), you will want to review card readers that specify the following:

* **ISO 7816** support

We also have an [Approved Products List](https://www.idmanagement.gov/IDM/IDMFicamProductSearchPage) for _US Federal Executive Branch Civilian Agencies_.  For the type of card reader you will need for computers, we identify these as "Transparent Card Readers" on the [Approved Products List](https://www.idmanagement.gov/IDM/IDMFicamProductSearchPage).  If you are buying card readers for your agency, you can use [GSA Advantage](https://www.gsaadvantage.gov/) and search for options using "ISO 7816" as one search term.

Before you buy a card reader, look around and make sure you don't already have one.  There are a number of laptops that have the card readers built-in.  The best option is to search for your laptop maker and version online, and review the technical specifications to determine if there is a smartcard reader installed.

If you have a Mac OSX laptop, you probably don't have a card reader built in! Find a card reader option that you like and let's move on to Drivers.

#### Drivers
_Drivers_ are software that allow your computer to communicate with hardware.  In the Standards and Specifications for PIV credentials, the term _middleware_ is used and a common question is "What is the difference between Middleware and Drivers?" _Middleware_ as a general computer term can encompass any software that provides integration points for an application.  To simplify, we'll define the two terms as they apply to PIV credentials in these guides:

*  PIV Middleware:   
  *  Client side software which implements the full set of application programming interfaces (APIs) as specified in the NIST Special Publication 800-73 series and has been defined as compliant to the NIST Special Publication 800-85A series testing procedures.  The PIV compliant middleware implements all _lifecycle_ functions including the ability for a user to perform PIN resets, activation, and renewals. The PIV compliant middleware may also implement common usage functions to support authentication, digital signatures, encryption, and integrations with multiple cryptographic libraries.   

*  Drivers:  
  *  

For common PIV credential usage scenarios, we outline the common Drivers.  

##### Windows  

| Type / Name               | Operating System | Considerations |
| -------------             |:----:|:----:|
| Windows mini-driver       | Windows 7, Windows 8, Windows 10, Windows 2008, Windows 2012  | Included in Windows and requires no installation or maintenance.  Does not include the functionality to manage a PIV credential.  May not support using your PIV credential with certain non-Microsoft developed software such as the Mozilla Firefox browser.   |
| OpenSC       | Yes  | Open source software.  Limited commercial support for maintenance and patching.  Support for     |
| Commercial options   | Yes  | Yes  |  


##### Mac

| Type / Name               | Operating System | Considerations |
| -------------             |:----:|:----:|
| OpenSC       | Yes  | Open source software.  Limited commercial support for maintenance and patching.  Support for     |
| Commercial options   | Yes  | Yes  |


##### Linux

| Type / Name               | Operating System | Considerations |
| -------------             |:----:|:----:|
| OpenSC       | Yes  | Open source software.  Limited commercial support for maintenance and patching.  Support for     |
| Commercial options   | Yes  | Yes  |


#### Next Steps
