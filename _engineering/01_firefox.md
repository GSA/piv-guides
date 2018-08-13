---
layout: default
title: Configure Firefox
collection: engineering
permalink: engineering/firefox/
---

You may need to configure your agency users to use their PIV credentials with Firefox to log into web applications. This can be tricky because Firefox supports a protocol (PKCS #11) that is not always natively supported by operating systems or the default drivers on operating systems.  

This guide will help you configure Firefox for your users using an open source software package.  In addition to open source solutions, commercial software may be used. 

* [Install Open Smart Card (OpenSC)](#install-and-test-opensc)
* [Configure Firefox](#configure-firefox)

{% include alert-info.html heading="PKCS #11" content="You are interested in learning more? Search for PKCS #11 for other resources available." %} 


## Install and Test OpenSC
First, you will need to install and test **OpenSC**. OpenSC will enable a PIV credential to work with the Firefox browser and some signing and encryption applications.  

OpenSC has installers for multiple operating systems including Windows, MacOS, and Linux flavors.  

* The installers and instructions can be downloaded directly from GitHub and the OpenSC wiki.
* [View instructions and installation procedures for OpenSC](https://github.com/OpenSC/OpenSC/wiki){:target="_blank"}

You need to consider some items that are specific for the US Government. 

* Even if the computer is running a 64-bit OS, you will need to download _both the 64- and 32-bit versions_ of OpenSC.
* You do not need to install the full packages for OpenSC.  
* You can limit the packages to distribute to your enterprise workstations to just support PKCS#11.  
* You can push the packages to the enterprise workstations using your enterprise configuration management tools.

## Configure Firefox
Perform the steps below to configure Firefox to enable PIV authentication.

### Load New Security Device

Launch **_Firefox_** and load a new security device using the OpenSC PKCS #11 driver:
* From the _Firefox_ taskbar, click the _Options_ icon ("gear" shape). 
* Click the _Privacy & Security_ menu from the left-hand navigation.
* Scroll down until you see the _Certificates_ heading, then click _Security Devices_.
* At the _Device Manager_ window, click the _Load_ button and enter the certificate name: _OpenSC PKCS#11 Module_.
* Based on the OS, select the location of the pkcs11 driver.  The default locations include:

| OS | Default driver location | File name | 
| ----- | -------| -------| 
| Windows | C:\Windows\System32 | pkcs11.dll | 
| MacOS  | /Library/OpenSC/lib/ | pkcs11.so | 
| Linux  | /usr/lib/ | pkcs11.so | 

* Click _Open_ and verify that the module has been loaded. Then, click _OK_ to return to the _Privacy & Security_ options.

### Import PIV Issuer Certificate
* Click the _View Certificates_ button. If prompted, enter your PIV credential PIN.
* Click the _Authorities_ tab from the top navigation.
* Click the _Import_ button to import a copy of your PIV credential issuer's certification authority certificate. Trust the certificate for _both_ identifying websites and email users.
* Click _OK_ and restart _Firefox_.

### Restart and Test Authentication
* Browse to a web application that requires a PIV to authenticate.  A common web application to use is **Max.gov**.
* Firefox will prompt you to enter your PIV credential PIN and select a certificate for authentication.
