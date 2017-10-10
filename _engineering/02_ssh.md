---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

You can use your PIV credential for Secure Shell (SSH) to remotely access *nix servers.  

{% include alert-info.html content = "Your PIV contains an authentication key pair and public certificate. Using a PIV key pair and public certificate is very similar to using a self-signed key pair for SSH." %}

This guide will help you to enable your environment to use your PIV for SSH to *nix servers from a _Windows_, _Linux_, or _macOS_ computer. These procedures use PuTTY-CAC or OpenSC. Other commercial options are available.    

- [SSH from Windows](#ssh-from-windows) 
- [SSH from Linux](#ssh-from-linux)
- [SSH from macOS](#ssh-from-macOS)
- [Configure the *nix Server](#configure-a-unix-like-server)

## SSH from Windows

These procedures are based on PuTTY-CAC v0.70-2. 

1. Download and install [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_. You need to install both the PuTTY client (putty.exe) and pageant (pageant.exe) at **C:\Program Files\PuTTY**.
1. DO WE ACTUALLY NEED to use pageant for 0.70-2? 
1. Run both PuTTY and Pageant, and insert your PIV into the card reader.
1. Click the Pageant icon from the Windows taskbar, and select **Add CAPI Cert**.
1. You will be prompted in a Windows security window to choose which certificate to use. Select your PIV _authentication_ certificate.  If you are not sure which certificate that is, view the certificate Properties and Enhanced Key Usage value.  Choose the one that says _Client Authentication_. 
1. The public key will be stored. Close the Pageant window.  
1. In PuTTY, you can create a new session profile for the target server.  
3. The settings for using your PIV authentication certificate are under Connection -> SSH -> Certificate
??? Set the CAPI CERT directly from Connection -> SSH -> Certificate
4. Click the checkbox for **Attempt certificate authentication**.
5. At the **PuTTY Configuration** window, select **Connection &gt; SSH &gt; Auth**. 
6. WHY?? Click the checkboxes for **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**.

For this next step - just use the copy to clipboard under Connection -> SSH -> Certificate
Insert screenshot

3. Save your **SSH keystring**&nbsp;**_value_** (i.e., "SSH key") in a **Notepad** file. Send it to the SSH server administrator to be added to your SSH server account. 

## SSH from Linux

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



## SSH from macOS
TODO = check sierra and see if we need opensc?

macOS 10.12 Sierra 
  
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

1. At the PIV card password prompt, enter your **PIN** to open the **remote-host shell prompt**.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}

## Configure a UNIX-like Server

{% include alert-info.html content = "Other configuration options are available including using Pluggable Authentication Modules (PAM) to look up your user accounts and authorization using directories." %}

These steps are performed by a privileged user with root privileges and can be automated for the servers by your centralized configuration management tools.  You can push or remove authorized_keys from the servers. 

1. Change the configuration in the **/etc/ssh/sshd_config** file and restart the **sshd**:

    ```
			AuthorizedKeysFile /etc/sshd/authorized_keys/%u  
			PasswordAuthentication No
    ```

2. Create the **/etc/sshd/authorized_keys** directory:

    ```
			mkdir /etc/sshd/authorized_keys
    ```

3. To allow one person to have access, place his/her PIV's SSH public key in this directory, according to username: **/etc/sshd/authorized_keys/[login ID]**. Disable any alternative means of access (i.e., passwords), as needed.
   
