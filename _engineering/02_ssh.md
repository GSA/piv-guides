---
layout: default
title: Enable PIV/CAC for SSH
collection: engineering
permalink: engineering/ssh/
---

**CB edit is in process. Updated 10/17/2017. Please review "coder" comments/questions, as well as in-line questions.**
<**WE NEED TO SAY SOMETHING ABOUT DUAL AUDIENCES LIKE: This guide is in two parts: Part 1 is for administrators who need to remotely access *nix servers. Part 2 is for server administrators who need to configure *nix servers for remote access.**>

To use Secure Shell (SSH) for remote access, you need to authenticate with your PIV/CAC credential. This guide will help you to do this from your Windows or macOs computer.<!--Apple uses "macOS" pretty consistently.--></BR>

{% include alert-info.html content = "Your Chief Information Security Officer must determine that security controls are in place and approve SSH scenarios. You should also review your agency's policies and use your physical or virtual jump servers to restrict users from using SSH directly from workstations." %} </BR> 

{% include alert-info.html content = "Your PIV/CAC contains an authentication certificate key pair (public and private) for smart card logon. Using a PIV/CAC key pair is very similar to using a self-signed key pair for SSH. The setup below is meant for PIV/CAC based authentication." %}

To enable PIV/CAC authentication for Windows, this guide uses PuTTY-CAC. For macOS 10.12.x (Sierra), this guide uses native smart-card features. Other commercial options are available. <!--I don't see OpenSC here any longer, so I deleted reference here.-->   

- [Windows](#ssh-from-windows) 
- [MacOS](#ssh-from-macos)
- [Configure a *nix Server](#configure-a-*nix-server)

## SSH from Windows

These steps use PuTTY-CAC v0.70u2, which supports Crypto API (CAPI) integration. Pageant software is not required.

1. You'll need to download [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_ to **C:\ssh\putty.exe**, or a similar folder. Select the 32-bit or 64-bit installer, based on your Windows OS. You don't need the complete PuTTY MSI Installer. <_Indrajit: For clarity, what PuTTY MSI Installer files does the engineer actually need so he/she doesn't need to guess?_>
2. Launch **PuTTY** and insert your PIV/CAC into your smart card reader.
3. At the **PuTTY Configuration** window side-bar, go to **Connection &gt; SSH &gt; Certificate**. Click **Set CAPI Cert...** and **Open.**
![PuTTY Configuration Window]({{site.baseurl}}/img/ssh-putty-cac-1.png){:style="float:left"}
4. At the **Windows Security** window (**PuTTY:&nbsp;&nbsp;Select Certificate for CAPI Auth**), select your certificate. 
5. If you don't know which one is yours, click the link to view its properties. At the **PuTTY Certificate Display** window, click the **Details** tab and then **Enhanced Key Usage**. If the certificate's _value_ is _Client Authentication_ or _Smart Card Logon_, then it's yours. The certificate details also appear in the inset window. <!--From the screenshot, it looks like you click on E.K.U. only to see the policy OIDs, not to see the E.K.U. value (displays automatically). (Tom H's steps kind of imply this.) Do you need to select something from the "Show" drop-down? (Screenshot shows "All" selected.)-->
![PuTTY Certificate Display Details]({{site.baseurl}}/img/ssh-putty-cac-2.png){:style="float:left"} 
6. Back at the **PuTTY Configuration** window, click the _Copy to Clipboard_ button and paste your certificate's public key into a text file. The public key will look like this:

    ```
        ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU1hSDi9rqcA1ACmU8nvg/mgPW1lIsj0zELzn8CiioQ+Mx7LGM2yCIK+fpVPYJnFKj5jTxe5Gzz7q5u946w/8Ge+J8hghzxooB5WsUF2vF92iyvy16XmNVYFSEKTOrkIM4PAvhIKcNUcogBB+M+W1rFpsGXZYGrA1xAU3kbw0mbVSdAYq4cZlX0JobQpxypELH5WojKTJaK7EyAY2hOHCAMuJIlvhIXtAY1eG/NabyPiAcv+yxsBWq2xwA96a1iivsBxO8VWEb8YBzwt6NIDALyCF+Fg546BzOLnDgPW7jHEdOttUfEjLwa17nAteQk9t CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
    ```    
7. Provide the text file to the remote server administrator to set up your account. 
8. <_Indrajit: Is this steps **after** the engineer has gotten an account or **before**?_> At the **PuTTY Configuration** window, you can now see that the **Attempt Certificate Authentication** box is _checked_.<!--How does the engineer know whether the *Attempt* was successful? System message?-->
9. Now you can create and save session profiles for each target server. Click **Session** and enter a remote server's **hostname** or **IP address**. For **Connection type**, click the **SSH** button and **22** will appear under **Port**. Enter a session name in **Saved Sessions** and click **Save**. 
10. <_Indrajit: The engineer completes the above steps but only now at Step 10 has an established acount?_> Once your account has been set up with your public key, click **Open** to log into the remote server using the **Sessions** window. <_Indrajit: Does the engineer first select a Saved Session and then log in?_>
> A dialog box opens and displays the server's key fingerprint as a _hash value_.
11. <_Indrajit: What screen is the engineer looking at here? Both the server key and the engineer's public key are displayed in the previous dialog?_>Verify and accept your public key and enter your username.
12. When the server detects the smart card authentication, it will prompt for your PIV/CAC credential PIN. Enter your PIN. Once the PIN is validated, you will be logged into the server via SSH.<_Indrajit: PIV/CAC was used in Step 2 above. Is this still the same occurrence of PIV/CAC insertion as done in Step 2 or is this a 2nd time?>

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV/CAC until the login process has been completed." %}

## SSH from macOS <!--Apples uses "macOS" pretty consistently.  We should use what they use.-->

**Celeste has not edited this section. Pending testing.**

MacOS X Sierra (10.12.x) and High Sierra (10.13) provide native support for smart card readers. If you have an earlier macOS version, you'll need to install third-party software, such as OpenSC. <!--Since Yosemite 10.10 also includes native smart card features, we should list that also, to give the reader full information. -->

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

Server administrators need to have root privileges for these steps. 

{% include alert-info.html content = "These SSH configurations are examples only. Other configuration options are available, including Pluggable Authentication Modules (PAM) that look up user accounts and authorizations through directories. You can automate setting up accounts by using centralized configuration management tools that can push or remove _authorized_keys_" %}

1. By default, SSH keys are read from the **.ssh/authorized_keys** file in your home directory. You will need to create a **/home/&lt;username&gt;/.ssh** directory and change it to the requestor's ownership. You will also need to create an **authorized_keys** file in the **.ssh** directory and copy the requestor's PIV/CAC public key to the **/home/&gt;user&gt;/.ssh/authorized_keys** file starting with **ssh-rsa &lt;public key&gt; &lt;key_name&gt;**.**  <IG--What does "starting with" mean? I see ssh-rsa below. Is that relate to the previous ssh-rsa command?>  

**Celeste stopped here 10/17**

    ```
	    mkdir /home/<user>/.ssh
	    chown <user> .ssh
	    chgrp <user> .ssh
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
	   AuthorizedKeysFile /etc/sshd/authorized_keys/%u  
	   PasswordAuthentication no
    ```
If you change the default settings, you have to create the corresponding directory for authorized_keys under /etc and setup the authorized keys in this folder instead of user's home folder.
