---
layout: default
title: Configure Firefox for PIV Login
collection: userconfig
permalink: userconfig/firefox/
---

## Configure Firefox for PIV Login

Many agencies use Firefox to access web applications, but Firefox doesn't allow for PIV logins. This guide is to help you configure Firefox, so employees can log into web applications with a PIV card. <!--Add the Firefox version number in case Firefox adds an option later on?-->

{% include alert-info.html heading="Option for DoD Personnel" content=" The Department of Defense (DoD) recommends the ActivClient software for Firefox CAC logins. ActivClient isn't free but may be available to DoD personnel: <!--May be available is uncertain. Does this mean free?--> https://militarycac.com/activclientalternate.htm." %} <!--According to the contributing.md (terms and conditions, as LaChelle calls it), Playbooks are supposed to be "vendor-neutal," so this info. may not be acceptable. To say "DoD recommends" is kind of broad; who at DoD? This formatting is for an info-alert box (a blue banner, Info box on website) because this info digresses by referring to specific commercial software, that isn't described herein, and a specific audience [DoD] vs. GSA's broader audience (Federal Government).-->

### Install OpenSC

An easy way to configure Firefox for a PIV card reader interface is to use OpenSC: 

* Download the latest version of OpenSC: [OpenSC wiki](https://github.com/OpenSC/OpenSC/wiki) (e.g., OpenSC-0.17.0-win32_vs12-Light-Release.msi).

> **Note:**  To install OpenSC on a 64-bit OS, you'll need to download both the 64- and 32-bit versions.

* Install OpenSC.
* Open Firefox and click on _Tools **>** Options_.
* Go **?Click on?** to the _Advanced_ tab and then _Certificates **>** Security Devices_ <!--Are the last 2 from a drop-down?-->
* To load the certificate, click the _Load_ and enter the name, _OpenSC PKCS#11 Module_.
* Select a certificate <!--certificate??-->file location for your OS:

  * _Windows: C:\Windows\System32_
  * _MacOS: /Library/OpenSC/lib/_
  * _Linux: /usr/lib/_
  
* Select a file:  (for Windows) _opensc pkcs11.dll_ or (for Linux or macOS) _opensc pkcs11.so_. Click _Open_.
* Verify that the module has been loaded and click _OK_.
* Restart Firefox and browse to a PIV-card-required website.

> Firefox will prompt you to select the PIV card certificate. 

* Select the certificate and proceed with authentication.
