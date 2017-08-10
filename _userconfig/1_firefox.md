---
layout: default
title: Configure Firefox for PIV Login
collection: userconfig
permalink: userconfig/firefox/
---
8/10/2017 NEW VERSION (UNEDITED)
## Configure Firefox for PIV Login

The Firefox browser does not provide an out of the box functionality to validate a Personal Identity Verification (PIV) card using a Common Access Card (CAC) reader. Many web applications used in various U.S. Agencies require support for Firefox as either a default browser or as a supported browser.

There are numerous options to enable CAC readers for Firefox. For example, the Department of Defense (DoD) recommends the ActivClient software. This software is not free at this moment. However, the software may be available to active DoD personnel. You can visit this link for more information https://militarycac.com/activclientalternate.htm.

Among the various options available to enable PIV login in Firefox, we will discuss the following methods.

1.	Installing OpenSC Software
2.	Enabling Kerberos for Firefox for GFE


### Installing OpenSC Software

The OpenSC Software provides the code libraries to implement the PIV card reader interface for Firefox. The steps for setting up the software is provided below.

* Download the latest version of the OpenSC software (e.g. OpenSC-0.17.0-win32_vs12-Light-Release.msi) from https://github.com/OpenSC/OpenSC/wiki.
* If you want to install on a 64 bit operating system, you will have to download both the 64 and 32 bit versions of the software.
* Install the software on the workstation.
* Open Firefox browser and click on Tools > Options.
* Navigate to ‘Advanced’ tab.
* Under ‘Certificates’ > ‘Security Devices’, click on ‘Load’ button to load a new security device.
* Enter the name as ‘OpenSC PKCS#11 Module’.
* For the file location, select:

  * _Windows: C:\Windows\System32_
  * _MacOS: /Library/OpenSC/lib/_
  * _Linux: /usr/lib/_
  
* Select the file opensc pkcs11.dll (Windows) or opensc pkcs11.so (Linux, macOS). 
* Click ‘Open’.
* Verify that the module is loaded and click ‘OK’.
* Restart the Firefox browser and access a PIV card required website. The Firefox browser will prompt for selecting the smart card certificate. Select the certificate and proceed with the authentication.

### Enabling Kerberos for Firefox

When a government furnished equipment (GFE) is used, the GFE may be configured to validate the PIV card during login to the GFE. This PIV authentication will be available to the application to use via a Kerberos token. In many cases the Firefox browser is unable to send the Kerberos data to the application. To enable Kerberos authentication for an application,  follow the steps mentioned below.

* In Firefox, type ‘about:config’ in the url window.
* Confirm any warning that Firefox presents related to voiding the warranty.
* In the search box, enter ‘negotiate’ to view the property name to set.
* Double click the property ‘network.negotiate-auth.trusted-uris’ and enter the value as http://,https://.
* Restart the Firefox browser.
