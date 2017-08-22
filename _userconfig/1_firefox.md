---
layout: default
title: Configure Firefox for PIV Login
collection: userconfig
permalink: userconfig/firefox/
---

Firefox doesn't allow for PIV login, which government employees and contractors need to access their important web applications. 

This guide will help you configure Firefox for PIV login. 

{% include alert-info.html heading="DoD CAC Logins with Firefox" content=" Commercial software packages can also be used, in addition to open-source solutions, like OpenSC. With these solutions, the procedures for configuring Firefox will be similar to those for the OpenSC software." %} 

### Install and Test OpenSC

Before you configure Firefox, you will need to install and test OpenSC. OpenSC will enable your PIV card to work with security applications (cryptographic, authentication, etc.).  

Go to:  [OpenSC](https://github.com/OpenSC/OpenSC/wiki) and follow the steps in the wiki for your OS (Windows, macOS, or Linux).

> **Notes:** 
  * The latest version is OpenSC-0.17.0-win32_vs12-Light-Release.msi.
  * Even if you are using a 64-bit OS, you will need to download _both the 64- and 32-bit versions_ of OpenSC.
  * To test the install, you will need to use the OS command prompt. If you haven't done this before, check with your system administrator or support help desk for help. 

### Configure Firefox for PIV Login

Once you have installed and tested OpenSC, launch **_Firefox_** (the latest version is 55.0.1, as of August 2017) and load its certificate:

* From the _Firefox_ taskbar, click the _Options_ icon ("wheel" shape) . 
* Click the _Advanced_ tab **>** _Certificates **>** Security Devices_.

* At the _Device Manager_ window, click the _Load_ button and enter the certificate name: _OpenSC PKCS#11 Module_.
* For your OS, select a certificate file location:

  * **_Windows: C:\Windows\System32_**
  * **_MacOS: /Library/OpenSC/lib/_**
  * **_Linux: /usr/lib/_**
  
* Next, for a **_Windows OS_**, select the _opensc pkcs11.dll_ file.

**_OR_**

* For a **_Linux OS_** or **_macOS_**, select the _opensc pkcs11.so_ file. 
* Click _Open_ and verify that the module has been loaded. 
* Click _OK_ and restart _Firefox_. 
* Next, browse to one of your web applications that requires a PIV login.

> Firefox will prompt you to select the PIV card's certificate. <!--Is this being done by an Admin or user?-->

* Select the certificate and use your PIV card to log into your web application. <!--Is loading the certificate is a one-time step for a user's computer or does it need to be reloaded each time the user needs to login with PIV? Suggest we clarify this for users or Admin, depending on what audience the procedures are for.-->
