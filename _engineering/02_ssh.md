---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

For network engineers, this guide will help you to authenticate with your PIV/CAC and SSH to a linux server from your Windows or macOS computer. For server administrators, this guide will help you to configure a linux server for remote access.

This guide uses open-source, smart-card software for Windows (PuTTY-CAC) and OpenSC for MacOS. Commercial solutions are also available.

{% include alert-info.html content = "Your PIV/CAC contains an authentication certificate key pair (public and private) for smart card logon. Using a PIV/CAC key pair is very similar to using a self-signed key pair for SSH. The setup below is meant for PIV/CAC based authentication." %}

{% include alert-info.html content = "Your Chief Information Security Officer must determine that security controls are in place and approve SSH scenarios. You should also review your agency's policies and use your physical or virtual jump servers to restrict users from using SSH directly from workstations." %} <!--The 1st caveat is for the network engineer. The 2nd caveat is for server admnistrators only?--></BR> 

- [Windows](#ssh-from-windows) 
- [MacOS](#ssh-from-macos)
- [Configure a Linux Server](#configure-a-linux-server)

## SSH from Windows

These steps use PuTTY-CAC v0.70u2, which supports Crypto API (CAPI) integration. Pageant software is not required.

1. You'll need to download [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_ to **C:\ssh\putty.exe**, or a similar folder. Select the 32-bit or 64-bit installer, based on your Windows OS. You don't need to install the complete PuTTY using one of the MSI Installers. <!--Indrajit: For clarity, what PuTTY MSI Installer files does the engineer actually need so he/she doesn't need to guess?  -- Celeste: There are multiple MSI Installer. It is not required to install using the MSI Installer. -->
2. Launch **PuTTY** and insert your PIV/CAC card into your smart card reader.
3. At the **PuTTY Configuration** window side-bar, go to **Connection &gt; SSH &gt; Certificate**. Click **Set CAPI Cert...** and **Open.**<!--Celeste: Why did you change this to include **Open**? This is incorrect. Looks like you changed this from what I wrote originally. -->
![PuTTY Configuration Window]({{site.baseurl}}/img/ssh-putty-cac-1.png){:style="float:left"}
4. At the **Windows Security** window (**PuTTY:&nbsp;&nbsp;Select Certificate for CAPI Auth**), select your certificate. 
5. If you don't know which one is yours, click the link <!--Celeste: What link are you talking about? Looks like you changed this from what I wrote originally. --> to view its properties. At the **PuTTY Certificate Display** window, click the **Details** tab and then **Enhanced Key Usage**. If the certificate's _value_ is _Client Authentication_ or _Smart Card Logon_, then it's yours. The certificate details also appear in the inset window. <!--From the screenshot, it looks like you click on E.K.U. only to see the policy OIDs, not to see the E.K.U. value (displays automatically). (Tom H's steps kind of imply this.) Do you need to select something from the "Show" drop-down? (Screenshot shows "All" selected.) Celeste -- I do not know what you are looking at from Tom H's instructions. I would keep my instructions as I tested. -->
![PuTTY Certificate Display Details]({{site.baseurl}}/img/ssh-putty-cac-2.png){:style="float:left"} 
6. Back at the **PuTTY Configuration** window, click the _Copy to Clipboard_ button and paste your certificate's public key into a text file. The public key will look like this:

    ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOF... CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
    ```    
7. Provide the text file to the administrator to set up your account. Once your account has been set up with your public key on the linux server by the administrator (see the instructions for setting up the linux server below), you can proceed with the settings for SSH login below.
8. At the **PuTTY Configuration** window, you can now see that the **Attempt Certificate Authentication** box is _checked_.
9. Now you can create and save session profiles for each target server. Click **Session** and enter a remote server's **hostname** or **IP address**. For **Connection type**, click the **SSH** button and **22** will appear under **Port**. Enter a session name in **Saved Sessions** and click **Save**. 
10. Click **Open** to log into the linux server using the **Sessions** window. A dialog box opens and displays the server's key fingerprint as a _hash value_.
11. Verify and accept your public key and enter your username.
12. When the server detects the smart card authentication, it will prompt for your PIV/CAC credential PIN. Enter your PIN. Once the PIN is validated, you will be logged into the server via SSH.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV/CAC until the login process has been completed." %}

## SSH from macOS

To enable PIV/CAC authentication for your MacOS Desktop, you'll need to install third-party software, such as OpenSC:  

1. Install [OpenSC](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}_. 
2. Insert your **PIV/CAC** card into your card reader.
3. You can view the certificates from the smart card using the command below.

    ```
	    pkcs15-tool --list-public-keys
    ```  

This command will list all the certificates. You should note the ID for the **PIV AUTH pubkey** RSA key.

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

4. To view your **public SSH key**, use the command below. The <ID> value is the number from the ID of the certificate. Once prompted, you have to enter the PIV/CAC card PIN.

    ```
	pkcs15-tool --read-ssh-key <ID>
    ```  
The public key will look like this:

    ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU .... PIV AUTH pubkey
    ```    
    
5. Send the SSH key to the server administrator for setup of your access to the linux server.
6. To log into the remote server, enter:

    ```
	ssh -I /usr/lib64/opensc-pkcs11.so <username>@<remote-host>
    ```    
If you do not want to specify the opensc-pkcs11.so using the -I for ssh command, you can update the /etc/ssh_config file.

    ```
	PKCS11Provider /usr/lib64/opensc-pkcs11.so
    ```  

7. At the PIV card password prompt, enter your **PIN**. You will now be logged into the Linux server via SSH.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}

## Configure a Linux Server

Server administrators need to have root privileges for these steps. 

{% include alert-info.html content = "These SSH configurations are examples only. Other configuration options are available, including Pluggable Authentication Modules (PAM) that look up user accounts and authorizations through directories. You can automate setting up accounts by using centralized configuration management tools that can push or remove _authorized_keys_" %}

1. By default, SSH keys are read from the **.ssh/authorized_keys** file in your home directory. You will need to create a **/home/&lt;username&gt;/.ssh** directory and change it to the requestor's ownership. You will also need to create an **authorized_keys** file in the **.ssh** directory and copy the requestor's PIV/CAC public key to the **/home/&gt;user&gt;/.ssh/authorized_keys** file starting with **ssh-rsa &lt;public key&gt; &lt;key_name&gt;**.

    ```
	    mkdir /home/<user>/.ssh
	    chown <user> .ssh
	    chgrp <user> .ssh
	    chmod 700 .ssh
	    cat > authorized_keys 
	    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU1hSDi9rqcA1ACmU8nvg/mgPW1lIsj0zELzn8CiioQ+Mx7LGM2yCIK+fpVPYJnFKj5jTxe5Gzz7q5u946w/8Ge+J8hghzxooB5WsUF2vF92iyvy16XmNVYFSEKTOrkIM4PAvhIKcNUcogBB+M+W1rFpsGXZYGrA1xAU3kbw0mbVSdAYq4cZlX0JobQpxypELH5WojKTJaK7EyAY2hOHCAMuJIlvhIXtAY1eG/NabyPiAcv+yxsBWq2xwA96a1iivsBxO8VWEb8YBzwt6NIDALyCF+Fg546BzOLnDgPW7jHEdOttUfEjLwa17nAteQk9t CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
			
    ```

2. You should set the permissions on authorized_keys to 600 and change the ownership of authorized_keys to the user.

    ```
	     chmod 600 authorized_keys
	     chown <user> authorized_keys
	     chgrp <user> authorized_keys
    ```
   
3. This step is only needed if you want to change the default SSH setting. You can change the configuration for the key file in the **/etc/ssh/sshd_config** file and restart the **sshd**. You can also disable any alternative means of access (i.e., passwords), as needed.

    ```
	   AuthorizedKeysFile /etc/ssh/authorized_keys/%u  
	   PasswordAuthentication no
    ```
If you change the default settings, you have to create the corresponding directory for authorized_keys under /etc/ssh and setup the authorized keys in this folder instead of user's home folder.
