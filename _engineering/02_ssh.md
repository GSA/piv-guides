---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

You can use your PIV credential for Secure Shell (SSH) to remotely access *nix servers by following these steps. This guide will help you SSH from a _Windows_, _Linux_, or _macOS_ computer.   

{% include alert-info.html content = "Your PIV/CAC contains an authentication certificate key pair (public and private) for smart card logon. Using a PIV/CAC key pair is very similar to using a self-signed key pair for SSH. The setup below is meant for PIV/CAC based authentication." %}

These procedures use PuTTY-CAC, OpenSC, and native smart card features. Other commercial options are available.    

- [Windows](#ssh-from-windows) 
- [Linux and macOS 10.12 Sierra](#ssh-from-linux-and-macos-10.12-sierra)
- [Configure a *nix Server](#configure-a-*nix-server)

## SSH from Windows

These procedures are based on PuTTY-CAC v0.70u2.

1. You need to download the [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_ (putty.exe) to a folder such as **C:\ssh\putty.exe** on your windows computer. You should choose either the 32 bit or 64 bit executable based on your Windows OS. You do not need to install the complete putty MSI Installer for this setup.
1. Run PuTTY by double clicking the putty.exe. It will open up the Putty window once you accept to run the application.
1. You should have a PIV card reader attached to your computer. Insert your PIV into the card reader.
1. and select **Add CAPI Cert**.
1. You will be prompted in a Windows security window to choose which certificate to use. Select your PIV _authentication_ certificate.  If you are not sure which certificate that is, view the certificate Properties and Enhanced Key Usage value.  Choose the one that says _Client Authentication_. 
1. In PuTTY, you can create a new session profile for the target server.  
1. The settings for using your PIV authentication certificate are under Connection -> SSH -> Certificate
??? Set the CAPI CERT directly from Connection -> SSH -> Certificate
1. Click the checkbox for **Attempt certificate authentication**.
1. At the **PuTTY Configuration** window, select **Connection &gt; SSH &gt; Auth**. 
1. **WHY??** Click the checkboxes for **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**. **Agent forwarding:  Chris Byron & Neil Bolin say this is necessary. May relate to Pageant (agent). Will follow-up further. --CB**

**For this next step - just use the copy to clipboard under Connection -> SSH -> Certificate
Insert screenshot**

3. Save your **SSH keystring&nbsp;_value_** (i.e., _SSH key_) and send it to the SSH server administrator to be added to your SSH server account. 

## SSH from Linux and macOS 10.12 Sierra 

**What Linux did we use--Debian, Red Hat, CentOS? --CB**

<!--Do we need to say which Linux and UNIX we are using?  The Linux and macOS X 10.12 Sierra procedures here are identical, as LaChelle pointed out. Rather than having 2 identical, consecutive procedures, use one procedure for both Linux and macOS X 10.12 Sierra--unless we don't need OpenSC for macOS? Can we use a title like "Linux-Based Systems" (which would include Mac)?  We could say these are based on macOS 10.12 Sierra.  What Linux system did Chunde use to test the Linux procedure?-->

1. Install [OpenSC](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}_.
1. Insert your **PIV** into your card reader.
1. To save your **public SSH key** to a file, enter:

    ```
			ssh-keygen -D /usr/lib64/opensc-pkcs11.so > mykey.pub
    ```  

1. Send the file to the SSH server administrator.
1. To log into the remote server, enter:

    ```
			ssh -I /usr/lib64/opensc-pkcs11.so <remote-host>
    ```    

3. At the PIV card password prompt, enter your **PIN** to open the **remote-host shell prompt**.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %} 



## SSH from macOS 10.12 Sierra 

**Delete this section unless OpenSC isn't needed for macOS X Sierra. Then we'll have to give specific details for what open-source or mac solution will be used to set up macOS X for SSH (similar to OpenSC).**

**TODO = check sierra and see if we need opensc? 10/11/2017: Information on Apple website and one open-source method for enabling smart card use without OpenSC for macOS Sierra. Sent to Indrajit for review. --CB**

macOS 10.12 Sierra 
  
1. Install [OpenSC](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}_.
1. Insert your PI into your card reader.
1. To save your **public SSH key** to a file, enter:

    ```
			ssh-keygen -D /usr/lib64/opensc-pkcs11.so > mykey.pub
    ```  

1. Send the file to the SSH server administrator.
1. To log into the remote server, enter:

    ```
			ssh -I /usr/lib64/opensc-pkcs11.so <remote-host>
    ```    

1. At the PIV card password prompt, enter your **PIN** to open the **remote-host shell prompt**.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}

## Configure a *nix Server

<!--Read procedures for accessing remote server and they say you need to have an SSH daemon installed on the remote server. Not in our procedures. Is this needed?-->

{% include alert-info.html content = "Other configuration options are available, including Pluggable Authentication Modules (PAM) that look up your user accounts and authorization by using directories." %}

<!--Since these procedures are for network engineers, we don't need to say this?-->These steps are performed by network engineers with root privileges. They can be automated for your servers through centralized configuration management tools. You can push or remove authorized_keys from the servers. 

1. Change the configuration in the **/etc/ssh/sshd_config** file and restart the **sshd**:

    ```
			AuthorizedKeysFile /etc/sshd/authorized_keys/%u  
			PasswordAuthentication No
    ```

1. Create the **/etc/sshd/authorized_keys** directory:

    ```
			mkdir /etc/sshd/authorized_keys
    ```

1. Place your PIV SSH public key in this directory, according to your username: **/~/sshd/authorized_keys/[login ID]**. Disable any alternative means of access (i.e., passwords), as needed.
   
