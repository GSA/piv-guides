---
layout: default
title: Configure Firefox
collection: engineering
permalink: engineering/firefox/
---

You may need to configure Firefox so your agency users can log into web applications using their PIV credentials.<!--"Configure agency users" doesn't make sense-->This can be tricky because Firefox supports a protocol (PKCS #11) that is not always natively supported by operating systems or their default drivers.  

This guide will help you configure Firefox for your users by using an open source software package.  In addition to open source solutions, commercial software may be used. 

* [Install and Test OpenSC](#install-and-test-opensc)
* [Configure Firefox](#configure-firefox)

{% include alert-info.html heading="PKCS #11" content="You are interested in learning more? Search for PKCS #11 for other resources available." %} 


## Install and Test OpenSC
OpenSC will enable a PIV credential to work with Firefox and some signing and encryption applications.  

First, you will need to install and test **OpenSC**. OpenSC has installers for multiple operating systems, including Windows, macOS, and Linux flavors. The installers can be downloaded directly from GitHub and the OpenSC wiki.<!--Are "installers" = modules?-->

* [View instructions and installation procedures for OpenSC](https://github.com/OpenSC/OpenSC/wiki/){:target="_blank"}

When downloading and installing OpenSC, you need to consider some items that are specific for the U.S. Government: 

* Even if the computer is running a 64-bit OS, you will need to download and install _both the 64- and 32-bit versions_ of OpenSC.
* You do not need to install the full packages for OpenSC.<!--Meaning -- Light-Release? Do we recommend one in particular?-->
* You can limit the packages for distribution to enterprise workstations to just support PKCS #11.
* You can push the packages to the enterprise workstations using your enterprise configuration management tools.

## Configure Firefox

### Load New Security Device

Launch **_Firefox_** and load a new _Security Device_ using the OpenSC PKCS #11 driver:
* From the _Firefox_ taskbar, click the _Options_ icon ("gear" shape). 
* Click the _Privacy & Security_ menu from the left-hand navigation.
* Scroll down until you see the _Certificates_ heading, and then click _Security Devices_.
* At the _Device Manager_ window, click the _Load_ button and enter the module name: _OpenSC PKCS#11 Module_.<!--Where is the module name listed in OpenSC downloads? Is the module the same thing as the driver? (We seem to use "driver" in other places)? Don't see that name in OpenSC download list. No space before "#11"?-->
* Select the location of the OpenSC PKCS #11 driver based on OS. The default locations include:

| **OS** | **Default Driver Location** | **Driver File Name** | 
| ----- | -------| -------| 
| _Windows_ | C:\Windows\System32 | pkcs11.dll | 
| _macOS_  | /Library/OpenSC/lib/ | pkcs11.so | 
| _Linux_  | /usr/lib/ | pkcs11.so | 

* Click _Open_ and verify that the module has been loaded<!--installed?-->. Then, click _OK_ to return to the _Privacy & Security_ options.

### Import PIV Issuer Certificate
* Click the _View Certificates_ button. If prompted, enter your PIV credential PIN.
* Click the _Authorities_ tab from the top navigation.
* Click the _Import_ button to import a copy of your PIV credential issuer's certification authority certificate. When prompted, trust the certificate for _both_ identifying websites and email users.
* Click _OK_ and restart _Firefox_.

### Restart and Test Authentication
* Browse to a web application that requires a PIV to authenticate.  A common web application to use is **Max.gov**.
* Firefox will prompt you to enter your PIV credential PIN and select a certificate for authentication.
