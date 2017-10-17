---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

**CB edit is in process. Updated 10/16/2017.**

You need to authenticate with your PIV/CAC to remotely access *nix servers using Secure Shell (SSH). This guide will help you to do this from your Windows or macOs computer.<!--Apple uses "macOS" pretty consistently.  We should use what Apple uses.-->

<!--Should this also be an info-alert box?-->Your Chief Information Security Officer must determine that security controls are in place and approve SSH scenarios. You should also review your agency's policies and use your physical or virtual jump servers to restrict users from using SSH directly from workstations. 

{% include alert-info.html content = "Your PIV/CAC contains an authentication certificate key pair (public and private) for smart card logon. Using a PIV/CAC key pair is very similar to using a self-signed key pair for SSH. The setup below is meant for PIV/CAC based authentication." %}

To enable PIV/CAC authentication for Windows 10<!--Are the steps for Windows 10? I think LaChelle indicated that government users are still using Windows 7. Should our steps address both Windows 10 and Windows 7?-->, this guide uses PuTTY-CAC and OpenSC. For macOS 10.12.x (Sierra) and 10.31 (High Sierra), this guide uses native smart-card features. Other commercial options are available.    

- [Windows](#ssh-from-windows) 
- [MacOS](#ssh-from-macos)
- [Configure a *nix Server](#configure-a-*nix-server)

## SSH from Windows

These steps use PuTTY-CAC v0.70u2, which supports Crypto API (CAPI) integration. Pageant software is not required.

1. You'll need to download [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_ to **C:\ssh\putty.exe**, or a similar folder. Download either the 32-bit or 64-bit installer, based on your Windows OS<!--Should we say Windows 10, 8, or 7? All have 32-bit and 64-bit.-->). You don't need the complete PuTTY MSI Installer.<!--Unclear what this means. It would be more clear to say which files the engineer actually needs.-->
1. Launch PuTTY and insert your PIV/CAC into your smart card reader.
1. At the **PuTTY Configuration** window side bar, select **Connection &gt; SSH &gt; Certificate**. Click **Set CAPI Cert...** and **Open.**<!--Do you click on the Open button at the bottom of the screen?-->
![PuTTY Configuration Window]({{site.baseurl}}/img/ssh-putty-cac-1.png){:style="float:left"}
1. At the **Windows Security &gt; PuTTY: Select Certificate for CAPI Auth**, select your certificate. 
1. If you don't know which certificate is yours, click the link to view the certificate properties. At the **PuTTY Certificate Display** window, click the **Details** tab. Then, click **Enhanced Key Usage** (EKU). The certificate is yours if its _value_ is _Client Authentication_ or _Smart Card Logon_. You'll also see the certificate's details in the inset window. Click **OK** to close.<!--From the screenshot, it looks like you click on E.K.U. only to see the policy OIDs, not to see the E.K.U. value (displays automatically). (Tom H's steps kind of imply this.) Do you need to select something from the "Show" drop-down? (Screenshot shows "All" selected.)-->
![PuTTY Certificate Display Details]({{site.baseurl}}/img/ssh-putty-cac-2.png){:style="float:left"} 
1. At the **PuTTY Configuration** window, click the _Copy to Clipboard_ button and paste your public key into a text file. The public key will look like this:

    ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU1hSDi9rqcA1ACmU8nvg/mgPW1lIsj0zELzn8CiioQ+Mx7LGM2yCIK+fpVPYJnFKj5jTxe5Gzz7q5u946w/8Ge+J8hghzxooB5WsUF2vF92iyvy16XmNVYFSEKTOrkIM4PAvhIKcNUcogBB+M+W1rFpsGXZYGrA1xAU3kbw0mbVSdAYq4cZlX0JobQpxypELH5WojKTJaK7EyAY2hOHCAMuJIlvhIXtAY1eG/NabyPiAcv+yxsBWq2xwA96a1iivsBxO8VWEb8YBzwt6NIDALyCF+Fg546BzOLnDgPW7jHEdOttUfEjLwa17nAteQk9t CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
    ```    
1. Provide the text file to the server administrator to set up your account. Once your gotten your account, you can continue with these steps. <!--Once he/she has gotten an account, what is the process to resume these steps? Can the engineer create a session profile and save it until he/she has an account or would that be _after_ the account is granted?-->
1. <!--This step is after the engineer has gotten an account?-->Back at the **PuTTY Configuration** window, the **Attempt Certificate Authentication** box is now checked. <!--How do you know that the authentication has been attempted and accepted?--> You'll know that the certificate authentication was successful when...
1. You can create a session profile for each target server. Click **Session** and enter the remote server's **hostname** or **IP address**. For **Connection type**, click the **SSH** button and **22** will appear under **Port**. Give the file a name in **Saved Sessions** and click **Save**.
1. Once your account has been set up with your public key, click **Open** to log in using the Sessions window in PuTTY. **Celeste stopped here.**
1. You will be presented with the dialog displaying the server's key fingerprint as a hash value. Verify and accept the key and enter your username that has been setup by the server administrator.
1. The server will detect the smart card authentication and you will be prompted to enter the PIV/CAC card PIN. Once the PIN is validated, you will be logged into the server via SSH.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}

## SSH from macOS <!--Apples uses "macOS" pretty consistently.  We should use what they use.-->

MacOS X Sierra (10.12.x) and High Sierra (10.13) provide native support for smart card readers. If you have an earlier macOS version, you'll need to install third-party software, such as OpenSC. <!--Since Yosemite 10.10 also includes native smart card features, we should list that also, to give the reader full information. "Earlier versions" would be earlier than Yosemite 10.10.-->

1. Install [OpenSC](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}_. **Replace with macOs native smart card feature steps.**
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

## Configure a *nix Server

{% include alert-info.html content = "The following SSH configurations are for illustration purposes only. You should verify the options available for your server *nix version. Other configuration options are available, including Pluggable Authentication Modules (PAM) that look up your user accounts and authorization by using directories." %}

These steps are performed by a server administrator with root privileges to setup the user's account on the *nix server. They can be automated for your servers through centralized configuration management tools. You can push or remove authorized_keys from the servers. 

1. By default, the SSH keys are set to be read from the .ssh/authorized_keys file in the user's home directory. You have to create the **/home/&lt;user&gt;/.ssh** directory where &lt;user&gt; is the user login. You should change the ownership to the user for .ssh directory. You should also create a file **authorized_keys** in the .ssh directory and copy the user's PIV/CAC public key in this **/home/&lt;user&gt;/.ssh/authorized_keys** file starting with ssh-rsa &lt;public key&gt; &lt;key_name&gt;.

    ```
	    mkdir /home/<user>/.ssh
	    chown <user> .ssh
	    chgrp <user> .ssh
	    cat > authorized_keys 
	    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU1hSDi9rqcA1ACmU8nvg/mgPW1lIsj0zELzn8CiioQ+Mx7LGM2yCIK+fpVPYJnFKj5jTxe5Gzz7q5u946w/8Ge+J8hghzxooB5WsUF2vF92iyvy16XmNVYFSEKTOrkIM4PAvhIKcNUcogBB+M+W1rFpsGXZYGrA1xAU3kbw0mbVSdAYq4cZlX0JobQpxypELH5WojKTJaK7EyAY2hOHCAMuJIlvhIXtAY1eG/NabyPiAcv+yxsBWq2xwA96a1iivsBxO8VWEb8YBzwt6NIDALyCF+Fg546BzOLnDgPW7jHEdOttUfEjLwa17nAteQk9t CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
			
    ```

1. You should set the permissions on authorized_keys to 600 and change the ownership of authorized_keys to the user.

    ```
	     chmod 600 authorized_keys
	     chown <user> authorized_keys
	     chgrp <user> authorized_keys
    ```
   
1. This step is only needed if you want to change the default SSH setting. You can change the configuration for the key file in the **/etc/ssh/sshd_config** file and restart the **sshd**. You can also disable any alternative means of access (i.e., passwords), as needed.

    ```
	   AuthorizedKeysFile /etc/sshd/authorized_keys/%u  
	   PasswordAuthentication no
    ```
If you change the default settings, you have to create the corresponding directory for authorized_keys under /etc and setup the authorized keys in this folder instead of user's home folder.
