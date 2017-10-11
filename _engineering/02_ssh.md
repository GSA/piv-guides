---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

You can use your PIV credential for Secure Shell (SSH) to remotely access *nix servers by following these steps. This guide will help you do this from a _Windows_, _Linux_, or _macOS_ computer.   

{% include alert-info.html content = "Your PIV contains an authentication key pair and public certificate. Using a PIV key pair and public certificate is very similar to using a self-signed key pair for SSH." %}

These procedures use PuTTY-CAC, OpenSC, and native smart card features. Other commercial options are available.    

- [Windows](#ssh-from-windows) 
- [Linux and macOS 10.12 Sierra](#ssh-from-linux-and-macos-10.12-sierra)<!--Changed heading if Linux and macOS X Sierra both use the same set of instructions. Why don't we just say here and in section below: "Linux-Based Systems"? We can add statement below that this includes macOS and that we tested macOS 10.12 Sierra and _____ (what Linux did we test?) Linux system.)...-->
- [Configure a *nix Server](#configure-a-*nix-server)

## SSH from Windows

These procedures are based on PuTTY-CAC v0.70u2.<!--These steps need to be validated since this is a newer version of PuTTY-CAC than the version that Chunde tested some months ago.-->

1. Download and install [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_. You need to install both the PuTTY client (putty.exe) and pageant (pageant.exe) at **C:\Program Files\PuTTY**.
1. **DO WE ACTUALLY NEED to use pageant for 0.70u2?** 
1. Run both PuTTY and Pageant, and insert your PIV into the card reader.
1. Click the Pageant icon from the Windows taskbar, and select **Add CAPI Cert**.
1. You will be prompted in a Windows security window to choose which certificate to use. Select your PIV _authentication_ certificate.  If you are not sure which certificate that is, view the certificate Properties and Enhanced Key Usage value.  Choose the one that says _Client Authentication_. 
1. The public key will be stored. Close the Pageant window.  
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
   
