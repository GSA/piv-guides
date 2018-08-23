---
layout: default
title: Configure Firefox
collection: engineering
permalink: engineering/firefox/
---

You may need to configure Firefox to enable your agency users to log into web applications using their PIV credentials. This can be tricky because Firefox supports a protocol (PKCS #11) that is not always natively supported by operating systems or OS default drivers. 

This guide will help you to configure Firefox by using an open source software package.  In addition to open source solutions, commercial software may be used. 

* [Install and Test OpenSC](#install-and-test-opensc)
* [Configure Firefox](#configure-firefox)

{% include alert-info.html heading="PKCS #11" content="You are interested in learning more? Search for PKCS #11 for other resources available." %} 

## Install and Test OpenSC
OpenSC will enable a user's PIV credential to work with Firefox and some signing and encryption applications.

First, you will need to install and test **OpenSC**. OpenSC has installers for multiple operating systems, including Windows, macOS, and Linux flavors. The installers can be downloaded directly from GitHub and the OpenSC wiki:

* [View instructions and installation procedures for OpenSC](https://github.com/OpenSC/OpenSC/wiki/){:target="_blank"}

When installing OpenSC, you need to consider some items that are specific for the U.S. Government: 

* You will need to download and install either the 64-bit or 32-bit version of OpenSC, depending on the OS.
* You do not need to install the full packages for OpenSC.<!--No need to be more specific?-->
* You can limit the packages for distribution to enterprise workstations to just support PKCS #11.
* You can push the packages to the enterprise workstations using your enterprise configuration management tools.

## Configure Firefox

### Load New Security Device

Launch **_Firefox_** and load a new _Security Device_ (i.e., the Security Device is your PIV credential) using the OpenSC PKCS #11 driver:
* From the _Firefox_ taskbar, click the _Options_ icon ("gear" shape). 
* Click the _Privacy & Security_ menu from the left-hand navigation.
* Scroll down until you see the _Certificates_ heading, and then click _Security Devices_.
* At the _Device Manager_ window, click the _Load_ button and enter this module name: _OpenSC PKCS#11 Module_.
* Select the directory where the OpenSC PKCS #11 driver is located. The default locations are:

| **OS** | **Default Driver Location** | **Driver File Name** | 
| ----- | -------| -------| 
| **Windows** | C:\Windows\System32 | pkcs11.dll | 
| **macOS**  | /Library/OpenSC/lib/ | pkcs11.so | 
| **Linux**  | /usr/lib/ | pkcs11.so | 

* Click _Open_ and verify that the module has been loaded. Then, click _OK_ to return to the _Privacy & Security_ options.

### Import PIV Issuer Certificate
* Click the _View Certificates_ button. If prompted, enter your PIV credential PIN.
* Click the _Authorities_ tab from the top navigation.
* Click the _Import_ button to import a copy of your PIV credential issuer's Certification Authority (CA) certificate. When prompted, trust the certificate for identifying websites _and_ email users.
* Click _OK_ and restart _Firefox_.

### Test Authentication
* Browse to a web application that requires authentication with a PIV credential.  A common web application to use as a test is [MAX.gov](https://max.gov/maxportal/home.action){:target="_blank"}. (**Note:** You'll need to have an existing MAX.gov account for this to work.)
* Firefox will prompt you to enter your PIV credential PIN and select a certificate for authentication.
