---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

For network engineers, this guide will help you to authenticate with your PIV/CAC and SSH to a Linux server from your Windows or macOS computer.&nbsp;&nbsp;For server administrators, this guide will help you to configure a Linux server for remote access.

This guide uses open-source, smart-card software for Windows (PuTTY-CAC) and macOS (OpenSC). Commercial solutions are also available.

{% include alert-info.html content = "Your PIV/CAC contains an authentication certificate key pair (public and private) for smart card logon. Using a PIV/CAC key pair is very similar to using a self-signed key pair for SSH. The setup below is meant for PIV/CAC based authentication." %}

{% include alert-info.html content = "Your Chief Information Security Officer must determine that security controls are in place and approve SSH scenarios. You should also review your agency's policies and use your physical or virtual jump servers to restrict users from using SSH directly from workstations." %} 

- [Windows](#ssh-from-windows) 
- [MacOS](#ssh-from-macos)
- [Configure a Linux Server](#configure-a-linux-server)

## SSH from Windows

These steps use PuTTY-CAC v0.70u2, which supports Crypto API (CAPI) integration. Pageant software is not required.

1. You'll need to download [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_ to **C:\ssh\putty.exe**, or a similar folder. Select the 32-bit or 64-bit executable, based on your Windows OS. You don't need the MSI Installers. 
1. Double-click on **putty.exe** to launch **PuTTY-CAC** and insert your **PIV/CAC** into your smart card reader.
1. At the **PuTTY Configuration** window side-bar, go to **Connection &gt; SSH &gt; Certificate**. Click **Set CAPI Cert...**.  
![PuTTY Configuration Window]({{site.baseurl}}/img/ssh-putty-cac-1.png){:style="float:left"}  
1. At the **Windows Security** window, select your certificate.   
1. If you don't know which certificate to choose, view its properties. At the **Certificate Details** tab, click **Enhanced Key Usage**. Select the one whose _value_ is _Client Authentication_ or _Smart Card Logon_ and click **OK**.  
![PuTTY Certificate Display Details]({{site.baseurl}}/img/ssh-putty-cac-2.png){:style="float:left"}  
1. Back at the **PuTTY Configuration** window, you'll see the certificate thumbprint. Click the _Copy to Clipboard_ button and paste your certificate's SSH key into a text file. The key will look like this:

    ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOF... CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
    ```    
1. Provide the text file to the administrator to set up your account. 
1. At the **PuTTY Configuration** window, you'll now see that the **Attempt Certificate Authentication** box is _checked_.
1. You can create and save session profiles for each target server. Click **Session** and enter a remote server's **hostname** or **IP address**. For **Connection type**, click **SSH** and **22** will appear under **Port**. Enter a session name in **Saved Sessions** and click **Save**. 
1. Once you have an account, select a **Saved Session** and click **Load** to load the server configuration. Click **Open** to connect to the Linux server. A dialog box will open and display the server's key fingerprint as a _hash value_. Verify and accept the server key and enter your username.
1. When the server detects your smart card authentication, it will prompt for your PIV/CAC PIN. Enter your PIN. Once it's validated, you'll be logged into the server via SSH.

{% include alert-warning.html heading = "The card reader may flash. Do not remove the PIV/CAC until the login process has been completed." %}

## SSH from macOS

To enable PIV/CAC authentication for your macOS, you'll need to install third-party software, such as OpenSC:  

1. Install [OpenSC](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}. 
1. Insert your **PIV/CAC** into your card reader.
1. To view all of the certificates on your Mac, enter:  
    ```
	    pkcs15-tool --list-public-keys
    ```  
1. Note the **ID** for the **PIV AUTH pubkey** RSA key:

   ```
	Using reader with a card: SCR35xx Smart Card Reader
	Public RSA Key [PIV AUTH pubkey]
		Object Flags   : [0x0]
		Usage          : [0xD1], encrypt, wrap, verify, verifyRecover
		Access Flags   : [0x2], extract
		ModLength      : 2048
		Key ref        : 154 (0x9A)
		Native         : yes
		ID             : 01
		DirectValue    : <absent>

	Public RSA Key [SIGN pubkey]
		Object Flags   : [0x0]
		Usage          : [0x2C1], encrypt, verify, verifyRecover, nonRepudiation
		Access Flags   : [0x2], extract
		ModLength      : 2048
		Key ref        : 156 (0x9C)
		Native         : yes
		ID             : 02
		DirectValue    : <absent>
   ```  
1. To view your **public SSH key**, enter: 

   ```
	pkcs15-tool --read-ssh-key 01
   ```  
**Note:**&nbsp;&nbsp;The _01_ value is the ID from above. When prompted, enter your PIV/CAC PIN. The SSH key will look like this:  

   ```
   ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU .... PIV AUTH pubkey
   ```    
    
1. Send the SSH key to the server administrator to set up your account.
1. Once you have your account, you can log into the Linux server. Enter: 

    ```
	ssh -I /usr/lib64/opensc-pkcs11.so <username>@<remote-host>  
    ```  
**Note:**&nbsp;&nbsp;If you don't want to specify the _opensc-pkcs11.so_ using **-I**, you can update the setting in the **/etc/ssh_config** file to:  

   ```
	PKCS11Provider /usr/lib64/opensc-pkcs11.so
   ```  

1. The server will prompt for your PIV/CAC PIN. Enter your PIN. Once it's validated, you'll be logged into the server via SSH.

{% include alert-warning.html heading = "The card reader may flash. Do not remove the PIV until the login process has been completed." %}

## Configure a Linux Server

Server administrators need to have root privileges for these steps. 

{% include alert-info.html content = "These SSH configurations are examples only. Other configuration options are available, including Pluggable Authentication Modules (PAM) that look up user accounts and authorizations through directories. You can automate account set-ups by using centralized configuration management tools that can push or remove authorized_keys." %}

1. By default, SSH keys are read from the **.ssh/authorized_keys** file in your home directory. You'll need to create a **/home/&lt;username&gt;/.ssh** directory and change it to the requestor's ownership. Then, create an **authorized_keys** file in the **.ssh** directory and copy the requestor's SSH key to the **/home/&gt;user&gt;/.ssh/authorized_keys** file starting with **_ssh-rsa &lt;public key&gt; &lt;key_name&gt;_**:

   ```
	    mkdir /home/<user>/.ssh
	    chown <user> .ssh
	    chgrp <user> .ssh
	    chmod 700 .ssh
	    cat > authorized_keys 
	    ssh-rsa AAAAB3NzaC1yc2EAAAADAQA... CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
	    
   ```

1. Set the permissions for **authorized_keys** to _600_ and change the **authorized_keys** ownership to the user:

   ```
	     chmod 600 authorized_keys
	     chown <user> authorized_keys
	     chgrp <user> authorized_keys
   ```
   
1. This step is only needed if you want to change the default SSH settings. You can change the location for the **authorized_keys** file in the **/etc/ssh/sshd_config** file and restart the **sshd**. You can also disable any alternative means of access (i.e., passwords), as needed:

   ```
	   AuthorizedKeysFile /etc/ssh/authorized_keys/%u  
	   PasswordAuthentication no
   ```
**Note:**&nbsp;&nbsp;If you change the default settings, you'll need to create a corresponding directory for **authorized_keys** under **/etc/ssh** and place the **authorized_keys** there instead of in the user's home folder.
