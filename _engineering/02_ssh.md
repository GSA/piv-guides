---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

**CB edit is in process.**

You can use your PIV/CAC credential for Secure Shell (SSH) to remotely access *nix servers. <!--Apple uses "macOS" pretty consistently.  We need to use what Apple uses.-->This guide gives you the steps... to enable your PIV/CAC for remote access from a Windows or macOS computer.<!--Still working on this. Need to condense intro-->

<!--Should this also be an info-alert box?-->Your Chief Information Security Officer must determine that security controls are in place and approve SSH scenarios. You should also review your agency's policies and use your physical or virtual jump servers to restrict users from using SSH directly from workstations. 

{% include alert-info.html content = "Your PIV/CAC contains an authentication certificate key pair (public and private) for smart card logon. Using a PIV/CAC key pair is very similar to using a self-signed key pair for SSH. The setup below is meant for PIV/CAC based authentication." %}

These procedures use PuTTY-CAC, OpenSC, and native smart card features. Other commercial options are available.    

- [Windows](#ssh-from-windows) 
- [MacOS](#ssh-from-macos)
- [Configure a *nix Server](#configure-a-*nix-server)

## SSH from Windows

These steps use PuTTY-CAC v0.70u2, which supports Crypto API (CAPI) integration. Pageant software is not required.

1. You need to download [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_ to **C:\ssh\putty.exe**, or similar. Download the 32-bit or 64-bit installer, based on your OS. You don't need the complete PuTTY MSI Installer.<!--It would be more clear to say which files they DO need; otherwise, they may have to guess at what we mean.-->
1. Launch PuTTY and insert your PIV/CAC into your smart card reader.
1. At the **PuTTY Configuration** window side bar, select **Connection &gt; SSH &gt; Certificate**, and click **Set CAPI Cert...** and **Open.**<!--Do you click on the Open button at the bottom of the screen?-->
![PuTTY Configuration Window]({{site.baseurl}}/img/ssh-putty-cac-1.png){:style="float:left"}
1. At the **Windows Security &gt; PuTTY: Select Certificate for CAPI Auth**, select your certificate. If you don't know which one is yours, view the certificate's properties. At the **PuTTY Certificate Display** window, click **Enhanced Key Usage**. If the _value_ says _Client Authentication_ or _Smart Card Logon_, then it's yours. Click _OK_. (**Note:**&nbsp;&nbsp&Your certificate's policy Object Identifiers (OIDs) also show up at the bottom of the window.)  
![PuTTY Certificate Display Details]({{site.baseurl}}/img/ssh-putty-cac-2.png){:style="float:left"} 
1. Back at the **PuTTY Configuration** window, click the _Copy to Clipboard_ button and paste your public key into a text file. Provide the file to the server administrator to set up your account. 

The public key will look like this:

    ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU1hSDi9rqcA1ACmU8nvg/mgPW1lIsj0zELzn8CiioQ+Mx7LGM2yCIK+fpVPYJnFKj5jTxe5Gzz7q5u946w/8Ge+J8hghzxooB5WsUF2vF92iyvy16XmNVYFSEKTOrkIM4PAvhIKcNUcogBB+M+W1rFpsGXZYGrA1xAU3kbw0mbVSdAYq4cZlX0JobQpxypELH5WojKTJaK7EyAY2hOHCAMuJIlvhIXtAY1eG/NabyPiAcv+yxsBWq2xwA96a1iivsBxO8VWEb8YBzwt6NIDALyCF+Fg546BzOLnDgPW7jHEdOttUfEjLwa17nAteQk9t CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
    ```    

1. You can now see that the **Attempt Certificate Authentication** box is checked. **How do you know that the authentication has been attempted and accepted?**
1. **Add explanation upfront -- purpose is to save this profile for use next time.** **Celeste stopped here** In PuTTY, you can create a new session profile for each target server. Click on **Session**, enter the server hostname or IP address, and select SSH (port 22) for connection type. You can now name this configuration in the _Saved Sessions_ and click '**Save**' to save this profile for use next time.
1. Once the administrator has set up your account with the public key that you provided, you can try the login by clicking '**Open** on the Sessions window in PuTTY.
1. You will be presented with the dialog displaying the server's key fingerprint as a hash value. Verify and accept the key and enter your username that has been setup by the server administrator.
1. The server will detect the smart card authentication and you will be prompted to enter the PIV/CAC card PIN. Once the PIN is validated, you will be logged into the server via SSH.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}

## SSH from MacOS <!--Apples uses "macOS" pretty consistently.  We should use what they use.-->

MacOS X Sierra (10.12.x) and High Sierra (10.13) provides native support for smart card readers. If you have an earlier macOS version, you'll need to install third-party software, such as OpenSC. 

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
