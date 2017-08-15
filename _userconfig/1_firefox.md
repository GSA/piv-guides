---
layout: default
title: Configure Firefox for PIV Login
collection: userconfig
permalink: userconfig/firefox/
---

## Configure Firefox for PIV Login

Firefox doesn't natively allow for PIV logins, which the agencies need to access web applications. This guide is to help you configure Firefox for PIV logins. <!--I'm not sure whether LaChelle will like this intro, but she likes concise, simple statements ("plain language"). Maybe we should add the Firefox version number--in case Firefox adds a PIV login option later on?-->

{% include alert-info.html heading="DoD CAC Logins with Firefox" content=" The DoD recommends ActivClient. ActivClient isn't free to agencies but may be to DoD personnel: <!--Can we find out whether it is free to them or not? If free to them, they would need permission to load it on their government computers, correct? --> https://militarycac.com/activclientalternate.htm." %} <!--According to the contributing.md (terms and conditions), Playbooks should be "vendor-neutal," so this info may not be acceptable. Who at DoD recommends ActivClient to its personnel? NOTE: This "alert-info" formatting produces a blue bannered, Info box on website. Suggest "info-alert" because this text digresses from procedures and speaks to a DoD audience vs. GSA's broader audience (Federal Government).-->

### Install OpenSC

OpenSC is a simple way to configure Firefox for PIV logins: 

* Download the latest version of OpenSC: [OpenSC wiki](https://github.com/OpenSC/OpenSC/wiki) (e.g., OpenSC-0.17.0-win32_vs12-Light-Release.msi).

> **Note:**  For a 64-bit OS, you'll need to download both the 64- and 32-bit versions. <!--Why is that?-->

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
