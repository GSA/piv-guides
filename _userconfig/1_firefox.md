---
layout: default
title: Configure Firefox for PIV Login
collection: userconfig
permalink: userconfig/firefox/
---

<!--Even though this Playbook is under Userconfig, it looks like these procedures are intended for an Admin who is setting up a user's computer? Is this correct?-->
Firefox doesn't allow for PIV login, which government employees and contractors need to access web applications. 

This guide is to help you configure Firefox for PIV login. <!--LaChelle prefers concise, simple statements (plain language) for Playbooks, so I've shortened the intro.-->

{% include alert-info.html heading="DoD CAC Logins with Firefox" content=" The DoD recommends ActivClient. ActivClient isn't free but may be to DoD personnel: <!--Can we find out whether it is free to them or not? If free to them, they would need permission to load it on their government computers, correct? --> https://militarycac.com/activclientalternate.htm." %} <!--According to the contributing.md (terms and conditions), Playbooks should be "vendor-neutral," so this info may not be acceptable. Who at DoD recommends ActivClient to its personnel? NOTE: This "alert-info" formatting produces a blue bannered, Info box on website. Suggest "info-alert" because this text digresses from procedures and speaks to a DoD audience vs. GSA's broader audience (Federal Government).-->

### Install OpenSC

A simple way to configure Firefox for PIV login is to use **OpenSC**. <!--Should we add the Firefox version number--in case Firefox adds a PIV login option later on?-->

Before configuring Firefox, you'll first need to download and install OpenSC: 

* Go to: [OpenSC wiki](https://github.com/OpenSC/OpenSC/wiki). (The latest version is OpenSC-0.17.0-win32_vs12-Light-Release.msi.) 
* Download and install OpenSC.

>> **Note:** Even if you're using a 64-bit OS, you'll need to download _both the 64- and 32-bit versions_ of OpenSC. <!--State the reason, unless they will understand?-->

### Configure Firefox for PIV Login

Once you've installed OpenSC, launch **Firefox** and load its certificate:

* Click _Options_ on the Firefox taskbar. <!--This is the way it looks for Firefox 55.0.1.-->
* Click the _Advanced_ tab **>** _Certificates **>** Security Devices_.

* At the _Device Manager_ window, click the _Load_ button and enter the certificate name: _OpenSC PKCS#11 Module_.
* Select a certificate file location (depending on your OS):

  * **_Windows: C:\Windows\System32_**
  * **_MacOS: /Library/OpenSC/lib/_**
  * **_Linux: /usr/lib/_**
  
* Next, for **Windows**, select the _opensc pkcs11.dll_ file.

**_OR_**

* For **Linux** or **macOS**, select the _opensc pkcs11.so_ file. 
* Click _Open_ and verify that the module has been loaded. 
* Click _OK_ and then restart Firefox. 
* Next, browse to a PIV-card-required website.

>> Firefox will prompt you to select the PIV card's certificate. <!--Is this an Admin or the computer user/PIV-card owner?-->

* Select the certificate and proceed with PIV login. <!--Is loading the certificate is a one-time step for a user's computer or does it need to be reloaded each time the user needs to login with PIV? Suggest we clarify this for users or Admin, depending on what audience the procedures are for.-->
