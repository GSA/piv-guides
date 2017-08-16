---
layout: default
title: Configure Firefox for PIV Login
collection: userconfig
permalink: userconfig/firefox/
---

<!--Even though this Playbook is under Userconfig, it looks like these procedures are intended for an Admin who is setting up a user's computer? Is this correct? Clarify who the audience is?-->
Firefox doesn't allow for PIV login, which government employees and contractors need to access their important web applications. 

This guide is to help you configure Firefox for PIV login. <!--LaChelle prefers short, simple statements (plain language) for Playbooks, so I've shortened the intro, done some word reduction throughout, and tried to add a friendly tone.-->

{% include alert-info.html heading="DoD CAC Logins with Firefox" content=" The DoD recommends ActivClient. ActivClient isn't free but may be to DoD personnel: <!--Can we find out whether it is free to them or not? If free to them, they would need permission to load it on their government computers, correct? --> https://militarycac.com/activclientalternate.htm." %} <!--According to the contributing.md (terms and conditions), Playbooks should be "vendor-neutral," so this info may not be acceptable. Who at DoD recommends ActivClient to its personnel? NOTE: This "alert-info" formatting produces a blue bannered, Info box on website. Suggest "info-alert" because this text digresses from procedures and speaks to a DoD audience vs. GSA's broader audience (Federal Government).-->

### Install OpenSC

A simple way to configure Firefox for PIV login is to use **OpenSC**. <!--Should we add the Firefox version number--in case Firefox adds a PIV login option later on?-->

Before configuring Firefox, you will first need to download and install OpenSC: 

* Go to [OpenSC wiki](https://github.com/OpenSC/OpenSC/wiki) and follow the steps in the wiki. (The latest version is OpenSC-0.17.0-win32_vs12-Light-Release.msi.) 

> **Note:** Even if you are using a 64-bit OS, you will need to download _both the 64- and 32-bit versions_ of OpenSC.

### Configure Firefox for PIV Login

Once you have installed OpenSC, launch **Firefox** and load its certificate:

* Click _Options_ ("wheel" icon) on the _Firefox_ taskbar. <!--This is the way it looks for Firefox 55.0.1.-->
* Click the _Advanced_ tab **>** _Certificates **>** Security Devices_.

* At the _Device Manager_ window, click the _Load_ button and enter the certificate name: _OpenSC PKCS#11 Module_.
* Depending on your OS, select one of these certificate file locations:

  * **_Windows: C:\Windows\System32_**
  * **_MacOS: /Library/OpenSC/lib/_**
  * **_Linux: /usr/lib/_**
  
* Next, for a **Windows** OS, select the _opensc pkcs11.dll_ file.

**_OR_**

* For a **Linux** OS or **macOS**, select the _opensc pkcs11.so_ file. 
* Click _Open_ and verify that the module has been loaded. 
* Click _OK_ and restart _Firefox_. 
* Next, browse to one of your web applications that requires a PIV login.

> Firefox will prompt you to select the PIV card's certificate. <!--Is this being done by an Admin or user?-->

* Select the certificate and use your PIV card to log into your web application. <!--Is loading the certificate is a one-time step for a user's computer or does it need to be reloaded each time the user needs to login with PIV? Suggest we clarify this for users or Admin, depending on what audience the procedures are for.-->
