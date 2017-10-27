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

Next, you have to configure Firefox to recognize the OpenSC drivers.  

Launch **_Firefox_** and configure the driver:

* From the _Firefox_ taskbar, click the _Options_ icon ("wheel" shape). 
* Click the _Advanced_ tab **>**&nbsp;_Certificates **>** Security Devices_.
* At the _Device Manager_ window, click the _Load_ button and enter the certificate name: _OpenSC PKCS#11 Module_.
* Based on the OS, select the location of the pkcs11 driver.  The default locations include:

| OS | Default driver location | File name | 
| ----- | -------| -------| 
| Windows | C:\Windows\System32 | pkcs11.dll | 
| MacOS  | /Library/OpenSC/lib/ | pkcs11.so | 
| Linux  | /usr/lib/ | pkcs11.so | 


* Click _Open_ and verify that the module has been loaded. 
* Click _OK_ and restart _Firefox_. 
* Next, browse to a web application that requires a PIV to authenticate.  A common web application to use is **Max.gov**.
* Firefox will prompt you to select the PIV certificate
