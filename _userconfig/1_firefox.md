---
layout: default
title: Configure Firefox for PIV Login
collection: userconfig
permalink: userconfig/firefox/
---

Government employees and contractors need to use their PIV cards with Firefox to log into their important web applications. Firefox doesn't currently allow for PIV login without added middleware.  

This guide will help you configure Firefox for PIV login. 

{% include alert-info.html heading="Commercial software packages are available." content=" In addition to open-source solutions like OpenSC, commercial software may be used. Commercial software procedures will be similar to those for OpenSC." %} 

## Install and Test OpenSC

Before you configure Firefox, you will need to install and test OpenSC. OpenSC will enable a PIV card to work with security applications (cryptographic, authentication, etc.).  

Go to:  [OpenSC](https://github.com/OpenSC/OpenSC/wiki){:target="_blank"}_ and follow the wiki steps for the OS (Windows, macOS, or Linux).

### Notes: 
* The latest version is OpenSC-0.17.0-win32_vs12-Light-Release.msi.
* Even if the computer is running a 64-bit OS, you will need to download _both the 64- and 32-bit versions_ of OpenSC.

## Configure Firefox for PIV Login

Once you have installed and tested OpenSC, launch **_Firefox_** (Firefox version 55.0.1 is the latest, as of August 2017) and load its certificate:

* From the _Firefox_ taskbar, click the _Options_ icon ("wheel" shape). 
* Click the _Advanced_ tab **>**&nbsp;_Certificates **>** Security Devices_.
* At the _Device Manager_ window, click the _Load_ button and enter the certificate name: _OpenSC PKCS#11 Module_.
* Based on the OS, select a certificate file location:

  * **_Windows: C:\Windows\System32_**
  * **_MacOS: /Library/OpenSC/lib/_**
  * **_Linux: /usr/lib/_**
  
* For **_Windows_**, select the _opensc pkcs11.dll_ file.

  **_OR_**

* For **_macOS_** or **_Linux_**, select the _opensc pkcs11.so_ file. 
* Click _Open_ and verify that the module has been loaded. 
* Click _OK_ and restart _Firefox_. 
* Next, browse to a web application that requires a PIV login.

> _Firefox will prompt you to select the PIV card's certificate._

* Select the certificate and use a test PIV card to log into the web application. <!--Is loading the certificate is a one-time step for a user's computer or does cert need to be reloaded each time the user needs to log in with a PIV?-->
