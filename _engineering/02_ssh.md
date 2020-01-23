---
layout: default
title: Enable SSH
collection: engineering
permalink: engineering/ssh/
---

For network engineers, this guide will help you authenticate with your PIV/CAC credential and use SSH to access a remote Linux server from a Windows or macOS computer. For server administrators, this guide will help you configure a Linux server for remote access.

This guide uses open-source options: 
* **Windows:** PuTTY-CAC (without Pageant) and WinSCP with Pageant
* **macOS:**  OpenSC 

Commercial solutions are also available.

{% include alert-info.html content = "Your PIV/CAC credential contains an authentication certificate key pair (public and private) for smart-card logon. Using a PIV/CAC key pair is very similar to using a self-signed key pair for SSH. " %}

{% include alert-info.html content = "Your Chief Information Security Officer must determine that security controls are in place and approve SSH scenarios. You should also review your agency's policies and use your physical or virtual jump servers to restrict users from using SSH directly from workstations." %} 

- [SSH from Windows - Using PuTTY-CAC](#ssh-using-putty-cac)
- [SSH from Windows - Using WinSCP and Pageant](#ssh-using-winscp-and-pageant) 
- [SSH from macOS](#ssh-from-macos)
- [Configure a Linux Server](#configure-a-linux-server)

## SSH from Windows

{% include alert-warning.html content = "Network administrator privileges are needed to use SSH for remote access." %}

### SSH Using PuTTY-CAC

PuTTY-CAC is an open-source SSH client that uses Microsoft's CryptoAPI (CAPI). (Pageant isn't needed with PuTTY-CAC for this solution.)
1. You'll need to download [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"} to _C:\ssh\putty.exe_ or a similar folder. Select either _32-bit_ or _64-bit_, based on your Windows OS. (Pageant and MSI Installers aren't needed.)
2. Double-click on _putty.exe_ and insert your PIV/CAC card into your card reader.
3. At the **PuTTY Configuration** window, go to _Category:_ &gt; _Connection_ &gt; _SSH_ &gt; _Certificate_. Click the _Set CAPI Cert..._ button and _OK_.
<br><br>
![PuTTY Configuration Window]({{site.baseurl}}/img/ssh-putty-cac-1.png){:style="float:left"}
<br><br>
4. From the **Windows Security** list, select your PIV/CAC authentication certificate by clicking _OK_. If you don't see your certificate, click _More choices_. (For help with certificates, see [Understanding PIV Certificates](https://piv.idmanagement.gov/details/#understanding-piv-certificates){:target="_blank"}.)
<br><br>
![Add CAPI Cert - #2]({{site.baseurl}}/img/winSCP-5.PNG)
<br>
5. Back at the **PuTTY Configuration** window, click the _Copy to Clipboard_ button and paste the SSH key into a text file. (**Note:** PuTTY-CAC derives the SSH key from the public key of your authentication certificate.) The SSH key will look like this:

   ```
      ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOF...
      CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4
   ```    
6. Send the text file to the server administrator and request an account. (Notice that the _Attempt Certificate Authentication_ box is now checked.)<br>
7. While waiting for an account, you can create SSH session profiles for target remote servers:<br><br> 
     o Click _Session_ and enter a remote server's _hostname_ or _IP address_.<br> 
     o For _Connection type_, click _SSH_. (Notice that under _Port_, _22_ appears.)<br>
     o Enter a session name in _Saved Sessions_ and click _Save_.<br>
8. Once you have an account, open PuTTY-CAC and insert your PIV/CAC card into your card reader. 
9. Click a _Saved Session_ and _Load_. 
10. Click _Open_ to connect to the remote server. (A dialog box displays the server's key thumbprint.) 
11. Verify the server key and accept it by clicking _Yes_.
12. Enter your account username. (A dialog box displays your PIV/CAC authentication certificate.) 
13. Click _Yes_ to permit the _signing operation_ and enter your PIV/CAC PIN. (You'll then be logged into the remote server.) 

{% include alert-warning.html content = "The card reader may flash. Do not remove your card until you're logged in." %}

### SSH Using WinSCP and Pageant

WinSCP is an open-source, secure copy protocol (SCP) and secure file transfer protocol (SFTP) client. Pageant is an SSH authentication agent that uses Microsoft's CAPI.  

1. Download **Pageant** to _C:\ssh\pageant.exe_ or a similar folder. Select [_32-bit_](https://github.com/NoMoreFood/putty-cac/blob/master/binaries/x86/pageant.exe){:target="_blank"} or [_64-bit_](https://github.com/NoMoreFood/putty-cac/blob/master/binaries/x64/pageant.exe){:target="_blank"}, based on your Windows OS. 
2. Download the [**WinSCP installer**](https://winscp.net/eng/download.php){:target="_blank"} to _C:\ssh\WinSCP-Setup.exe_ or a similar folder.
3. Double-click _WinSCP-Setup.exe_ to launch the _WinSCP installer_ and use the recommended installation settings.
4. Double-click _pageant.exe_ to launch **Pageant**. 
5. Next, at the **Windows** taskbar, click the _up-arrow_ and right-click the **Pageant** icon (_computer wearing a Fedora_). 
<br>
![Accessing Pageant - #2]({{site.baseurl}}/img/winSCP-2.PNG)
<br>
6. A **Pageant** dialog box appears. Click _Cert Auth Prompting_.
<br>
![Enable Cert Auth Prompting]({{site.baseurl}}/img/winSCP-3.PNG)
<br>
7. Click _Add CAPI Cert_ to view eligible authentication certificates.
<br>
![Add CAPI Cert - #1]({{site.baseurl}}/img/winSCP-4.PNG)
<br>
8. From the **Windows Security** screen, select your PIV/CAC authentication certificate, and click _OK_. If you don't see your certificate, click _More choices_. (For help with certificates, see [Understanding PIV Certificates](https://piv.idmanagement.gov/details/#understanding-piv-certificates){:target="_blank"}.)
<br>
![Add CAPI Cert - #2]({{site.baseurl}}/img/winSCP-5.PNG){:style="width:48%;"}
<br>
9. Double-click the **Pageant** icon to confirm that your certificate appears on the _Pageant Key List_.   
10. The _Pageant Key List_ shows the certificate's SSH key attributes, such as type, size, thumbprint, etc. Click your certificate and the _Copy to Clipboard_ button. (**Note:** Pageant derives the SSH key from the public key of your authentication certificate.) Close the _Pageant Key List_.
<br>
![Add CAPI Cert - #3]({{site.baseurl}}/img/winSCP-6.PNG){:style="width:48%;"}
<br>
11. Paste the SSH key into a text file. It will look like this:
     ```
       ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCOpGPxNh... CAPI:268f09f34ca7544bd44e1e310d2144...
       OID.0.9.2342.19200300.100.1.1=47999999999999 + CN=SAM JACKSON, OU=General Services Administration,
       O=U.S. Government, C=US
     ```
12. Send the text file to the server administrator and request a new account.
13. Once you have an account, go to the **WinSCP Login** window. Click _New Site_ and then the _Advanced_ button.
<br><br>
![WinSCP Configuration - #2]({{site.baseurl}}/img/winSCP-7.PNG){:style="width:63%;"}
<br><br>
15. At the **Advanced Site Settings** window, select _SSH_ &gt; _Authentication_. Click the checkbox for _Attempt Authentication using Pageant_ and then click _OK_. (WinSCP selects additional checkboxes by default.) 
<br><br>
![WinSCP Configuration - #2]({{site.baseurl}}/img/winSCP-8.PNG){:style="width:63%;"}
<br><br>
16. Insert your PIV/CAC card into your card reader. 
17. Enter the remote server's host name and your username. Click _Login_. 
18. The **Warning** dialog box displays the server’s key thumbprint. Verify it and click _Yes_ to accept.
19. At the **Certificate Usage Confirmation - Pageant** dialog box, click _Yes_ to confirm your authentication certificate.
<br><br>
![WinSCP Configuration - #2]({{site.baseurl}}/img/winSCP-10.PNG){:style="width:63%;"}
<br><br>
20. When prompted, enter your PIV/CAC PIN. You'll then be logged into the server.

{% include alert-warning.html content = "The card reader may flash. Do not remove your card until you're logged in." %}

## SSH from macOS

{% include alert-warning.html content = "Network administrator privileges are needed to use SSH for remote access." %}

There are two options for configuring SSH clients to use a PIV/CAC device as the SSH key store:

### Built-in PIV/CAC support (macOS High Sierra and later)

1. Insert your PIV/CAC into your card reader.
2. Use ` ssh-keygen -D /usr/lib/ssh-keychain.dylib` to get the OpenSSH-format public key fingerprint which can be added to your `authorized_keys` file, account profiles, etc.
3. Add `PKCS11Provider=/usr/lib/ssh-keychain.dylib` to your `~/.ssh/ssh_config` file to tell `ssh` to scan the PIV profiles for keys when determining which keys to attempt on remote hosts.

See https://support.apple.com/en-us/HT208372 for additional information

### OpenSC

You can use OpenSC on your macOS computer to authenticate to a remote server with your PIV/CAC card.  

1. Install [OpenSC](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}. 
2. Insert your PIV/CAC into your card reader.
3. To view the certificates on your Mac, enter:  
     ```
	pkcs15-tool --list-public-keys  
     ```
4. Make note of the _PIV AUTH pubkey_&nbsp;&nbsp;**ID** number. 
     ```
	Using reader with a card: SCR35xx Smart Card Reader
	Public RSA Key [PIV AUTH pubkey]
		Object Flags   : [0x0]
		Usage          : [0xD1], encrypt, wrap, verify, verifyRecover
		Access Flags   : [0x2], extract
		ModLength      : 2048
		Key ref        : 154 (0x9A)
		Native         : yes
		ID             : 01 (EXAMPLE ONLY)
		DirectValue    : <absent>
     ```
5. Use your _PIV AUTH pubkey_&nbsp;&nbsp;**ID** number to view your SSH key. Enter: 
     ```
    pkcs15-tool --read-ssh-key 01
     ```
6. When prompted, enter your PIV/CAC PIN. The SSH key will look like this:  
     ```
    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCyPn2dShOFLBnMraiP2MnLU ....  
     ```
7. Copy the SSH key and paste it into a text file.
8. Send the text file to the server administrator and request a new account.
9. Once you have an account, you can log into the remote server. Enter: 
     ```
	ssh -I /usr/lib64/opensc-pkcs11.so <username>@<remote-host>
     ```
10. Optionally, you can update the setting in the _/etc/ssh_config_ file to:  
     ```
	PKCS11Provider /usr/lib64/opensc-pkcs11.so
     ```
11. Enter your PIV/CAC PIN when prompted. Once it's validated, you'll be logged into the remote server.

{% include alert-warning.html content = "The card reader may flash. Do not remove your card until you're logged in." %}

## Configure a Linux Server

{% include alert-warning.html content = "Server administrators must have root privileges for these steps." %}
 
{% include alert-info.html content = "The following SSH configurations are examples only. Other options are available, including Pluggable Authentication Modules (PAM) that look up user accounts and authorizations through directories. You can automate account set-ups by using centralized configuration management tools that can push or remove authorized_keys." %}

By default, SSH keys are read from the _.ssh/authorized_keys_ file in your home directory. 

1. You'll need to create a _/home/&lt;username&gt;/.ssh_ directory and change it to the requester's ownership. Then, create an _authorized_keys_ file in the _.ssh_ directory and copy the requester's SSH key to the _/home/&lt;user&gt;/.ssh/authorized_keys_ file starting with _ssh-rsa&lt;public key&gt;&lt;key_name&gt;_:
   ```
	    mkdir /home/<user>/.ssh
	    chown <user> .ssh
	    chgrp <user> .ssh
	    chmod 700 .ssh
	    cat > authorized_keys 
	    ssh-rsa AAAAB3NzaC1yc2EAAAADAQA... CAPI:05bf4653b3098a87b67816d81049f489d5b5ffb4    
   ```
2. Set the permissions for ..._authorized_keys_ to _600_ and change the _authorized_keys_ ownership to the user:
   ```
	     chmod 600 authorized_keys
	     chown <user> authorized_keys
	     chgrp <user> authorized_keys
   ```
3. You can change the location for the _authorized_keys_ file in the _/etc/ssh/sshd_config_ file and restart the _sshd_ service. You can also enforce authentication with a PIV/CAC card by disabling password use:
   ```
	     AuthorizedKeysFile /etc/ssh/authorized_keys/%u  
	     PasswordAuthentication no
   ```
**Note:**&nbsp;&nbsp;If you change the default settings, you'll need to create a corresponding directory for _authorized_keys_ under _/etc/ssh_ and place the _authorized_keys_ there vs. in the user's home folder.

## Special Thanks

Special thanks to the Department of Homeland Security, Office of the Chief Information Officer, Identity Services Branch, Information Sharing and Services Office (IS2O), for sharing its WinSCP and Pageant procedures.
