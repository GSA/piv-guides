---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

You can use your PIV credential for Secure Shell (SSH) to remotely access *nix servers by following these steps. This guide will help you SSH from a _Windows_ or _macOS_ computer.   

{% include alert-info.html content = "Your PIV/CAC contains an authentication certificate key pair (public and private) for smart card logon. Using a PIV/CAC key pair is very similar to using a self-signed key pair for SSH. The setup below is meant for PIV/CAC based authentication." %}

These procedures use PuTTY-CAC, OpenSC, and native smart card features. Other commercial options are available.    

- [Windows](#ssh-from-windows) 
- [Apple Mac OS](#ssh-from-macos)
- [Configure a *nix Server](#configure-a-*nix-server)

## SSH from Windows

These procedures are based on PuTTY-CAC v0.70u2. This version of PuTTY-CAC provides support for CAPI Certificates without requiring pageant.exe.

1. You need to download the [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_ (putty.exe) to a folder such as **C:\ssh\putty.exe** on your windows computer. You should choose either the 32 bit or 64 bit executable based on your Windows OS. You do not need to install the complete putty MSI Installer for this setup.
1. Run PuTTY by double clicking the putty.exe. It will open up the Putty window once you accept to run the application.
1. You should have a PIV card reader attached to your computer. Insert your PIV into the card reader.
1. In the Putty, you will navigate to Connection > SSH > Certificate. Click on **Set CAPI Cert...**. 
![PuTTY-CAC CAPI Screenshot]({{site.baseurl}}/img/ssh-putty-cac-1.png){:style="float:left"}
1. You will be prompted in a Windows security window to choose which certificate to use. Select your PIV _authentication_ certificate.  If you are not sure which certificate that is, view the certificate details and look for the 'Enhanced Key Usage' value. Choose the one that says _Client Authentication_ or _Smart Card Logon_. 
![PuTTY-CAC Certificate]({{site.baseurl}}/img/ssh-putty-cac-2.png){:style="float:left"} 
1. Once you select the certificate, you will see the certificate thumbprint displayed in PuTTY window. Click on '**Copy To Clipboard**' button to copy your PIV/CAC certificate's public key for server setup. You should paste this public key data into a text file and provide this public key to the server administrator for setting up your account on the server. The data will look similar to this.

    ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU1hSDi9rqcA1ACmU8nvg/mgPW1lIsj0zELzn8CiioQ+Mx7LGM2yCIK+fpVPYJnFKj5jTxe5Gzz7q5u946w/8Ge+J8hghzxooB5WsUF2vF92iyvy16XmNVYFSEKTOrkIM4PAvhIKcNUcogBB+M+W1rFpsGXZYGrA1xAU3kbw0mbVSdAYq4cZlX0JobQpxypELH5WojKTJaK7EyAY2hOHCAMuJIlvhIXtAY1eG/NabyPiAcv+yxsBWq2xwA96a1iivsBxO8VWEb8YBzwt6NIDALyCF+Fg546BzOLnDgPW7jHEdOttUfEjLwa17nAteQk9t CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
    ```    

1. You will find that the checkbox for '**Attempt Certificate Authentication**' is now checked.
1. In PuTTY, you can create a new session profile for the target server. You can click on '**Session**' and enter the server hostname or IP address, and select SSH (port 22) for connection type. You can now name this configuration in the 'Saved Sessions' and click '**Save**' to save this profile for use next time.
1. Once the server administrator has setup your account with the public key that you provided, you can try the login by clicking '**Open** on the Sessions window in PuTTY.
1. You will be presented with the dialog window displaying the server's certificate. Accept the certificate and enter your login username that has been setup by the server administrator.
1. The server will detect the certificate authentication and you will be prompted to enter the PIV/CAC card PIN. Once the PIN is validated, you will be logged into the server via SSH.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}

## SSH from Mac OS

Mac OS Sierra (10.12.x) and High Sierra (10.13) provides built in support for PIV/CAC readers. If you have any of the previous versions of Mac OS, you will need to install a third party smart card utility software such as OpenSC. 

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

{% include alert-info.html content = "Other configuration options are available, including Pluggable Authentication Modules (PAM) that look up your user accounts and authorization by using directories." %}

These steps are performed by a server administrator with root privileges to setup the user's account on the *nix server. They can be automated for your servers through centralized configuration management tools. You can push or remove authorized_keys from the servers. 

1. Change the configuration in the **/etc/ssh/sshd_config** file and restart the **sshd**. This step is only needed if the setting is not set by default.

    ```
	   AuthorizedKeysFile /etc/sshd/authorized_keys/%u  
	   PasswordAuthentication No
    ```

1. Create the **/home/&lt;user&gt;/.ssh** directory where <user> is the user login. Change the ownership to the user for .ssh directory. You should also create a file **authorized_keys** in the .ssh directory and copy the user's PIV/CAC public key in this **/home/&lt;user&gt;/.ssh/authorized_keys** file starting with ssh-rsa &lt;public key&gt; &lt;key_name&gt;.

    ```
	    mkdir /home/<user>/.ssh
	    chown <user> .ssh
	    chgrp <user> .ssh
	    cat authorized_keys 
	    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU1hSDi9rqcA1ACmU8nvg/mgPW1lIsj0zELzn8CiioQ+Mx7LGM2yCIK+fpVPYJnFKj5jTxe5Gzz7q5u946w/8Ge+J8hghzxooB5WsUF2vF92iyvy16XmNVYFSEKTOrkIM4PAvhIKcNUcogBB+M+W1rFpsGXZYGrA1xAU3kbw0mbVSdAYq4cZlX0JobQpxypELH5WojKTJaK7EyAY2hOHCAMuJIlvhIXtAY1eG/NabyPiAcv+yxsBWq2xwA96a1iivsBxO8VWEb8YBzwt6NIDALyCF+Fg546BzOLnDgPW7jHEdOttUfEjLwa17nAteQk9t CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
			
    ```

1. You should set the permissions on authorized_keys to 600 and change the ownership of authorized_keys to the user.

    ```
	     chmod 600 authorized_keys
	     chown <user> authorized_keys
	     chgrp <user> authorized_keys
    ```

1. Disable any alternative means of access (i.e., passwords), as needed.
   
