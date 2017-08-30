---
layout: default
title: Enable PIV/CAC for SSH to a UNIX-like Server
permalink: /userconfig/ssh
collection: userconfig
---

Enabling your PIV for Secure Shell (SSH) is the most secure way to remotely access UNIX-like servers on your network. The strong security features of your PIV hardware (e.g., certificates and key pairs, encryption, biometrics) make it extremely difficult to exploit. Software authentication methods (e.g., usernames and passwords) are much more likely to be targeted by attackers. 

{% include alert-info.html heading = "Your PIV contains an authentication key pair and public certificate. Using a PIV key pair and public certificate is exactly like using a key pair and self-signed certificate for SSH remote access." %}

{% include alert-info.html heading = "Other authentication options are available, such as Linux' Pluggable Authentication Modules (PAM)." %}

This guide will help you to enable your PIV for SSH to UNIX-like servers from a _Windows_, _Linux_, or _macOS_ computer.

- [**Enable PIV for SSH from Windows**](#enable-piv-for-ssh-from-windows) 
- [**Enable PIV for SSH from Linux**](#enable-piv-for-ssh-from-linux)
- [**Enable PIV for SSH from macOS**](#enable-piv-for-ssh-from-macOS)
- [**Configure a UNIX-like Server**](#configure-a-unix-like-server)

## Enable PIV for SSH from Windows

- [**Hardware and software requirements**](#hardware-and-software-requirements)
- [**Install PuTTY-CAC**](#install-putty-cac)
- [**Use PIV to insert Microsoft CAPI key into Pageant**](#use-piv-to-insert-microsoft-capi-key-into-pageant)
- [**Configure PuTTY**](#configure-putty)
- [**SSH to a UNIX-like server**](#ssh-to-a-unix-like-server)

### Hardware and software requirements

* A PIV
* Windows computer
* A card reader
* PuTTY-CAC application (an open-source SSH client that supports PIV authentication)
* Pageant application (an SSH authentication agent used with PuTTY-CAC)

### Install PuTTY-CAC

1. Download and install [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}_. (_PuTTY-CAC will normally be installed at **C:\Program Files\PuTTY**._)

### Use PIV to insert Microsoft CAPI key into Pageant 

1. Insert your **PIV** into your card reader and go to:  **C: &gt; Program Files &gt; PuTTY &gt; Pageant**.
2. Click the **Pageant** icon from the Windows taskbar, and select **View Keys &amp; Certs**.

> _The Pageant **Key/CAPI Cert List** window opens._

3. Click **Add Cert**.
4. At the **Windows Security** window, select your **Smart Card Logon** certificate.
5. To ensure that the certificate is the right one, click **Click here to view certificate properties &gt; Details**.
6. Click **Enhanced Key Usage**.

> You should now see the **Smart Card Logon** window. (This means the certificate is of the right type.)

7. Click on the **Smart Card certificate** (i.e., **CAPI key**). Then click **OK** and **Close**. 

> _This fills in the certificate information. (Clear any expired or revoked certificates.) Whenever you start Pageant, you will need to re-add the certificate._

### Configure PuTTY

#### Set up a PIV login profile

1. At the Windows taskbar, click the **Pageant** icon; then select **New Session** to launch **PuTTY**.
2. Enter the Jump server's IP address and a session name. Click **Load**.
3. From **Category**, select **Connection &gt; SSH &gt; CAPI**. 
4. Click the checkbox for **Attempt "CAPI Certificate" (Key-only) auth (SSH-2)**.
5. At the **PuTTY Configuration** window, select **Connection &gt; SSH &gt; Auth**. 
6. Click the checkboxes for **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**.

#### Obtain PIV SSH key

1. At the **PuTTY Configuration** window, select **Connection &gt; SSH&nbsp;&gt; CAPI**. 
2. Under **Authentication Parameters**, click the **Browse** button.  

> _This fills in the **Cert** and **SSH keystring**._

3. Save your **SSH keystring**&nbsp;**_value_** (i.e., "SSH key") in a **Notepad** file. Send it to the SSH server administrator to be added to your SSH server account. 

#### SSH to a UNIX-like server

1. Launch **PuTTY**. 
2. Select a **Saved Session**; then click **Load** and **Open**.
3. Enter your **remote UNIX/Linux account name**.  
4. At the prompt, enter your PIV **PIN** and click **OK**. 
5. Once logged into the remote server, enter the command: **ssh-add –l** to display the SSH key.  

> _For each server you "jump to," **ssh-add –l** will display the SSH key. Once you see it, you may **SSH** to any host in the environment._

## Enable PIV for SSH from Linux

- [**Hardware and software requirements**](#hardware-and-software-requirements)
- [**Configure for PIV login**](#configure-for-piv-login)
- [**Obtain and save public key from PIV**](#obtain-and-save-public-key-from-piv)
- [**SSH to a UNIX-like server**](#ssh-to-a-unix-like-server)

### Hardware and software requirements

* A PIV
* A card reader
* A Linux computer 
  
### Configure for PIV login

For an open-source method, go to: [**OpenSC**](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}_.)

### Obtain and save public key from PIV

1. Insert your **PIV** into your card reader.
2. To save your **public SSH key** to a file, enter:

        ```
			ssh-keygen -D /usr/lib64/opensc-pkcs11.so > mykey.pub
        ```  

3. Send the file to the SSH server administrator.

### SSH to a UNIX-like server

1. Insert your **PIV** into your card reader.
2. To log into the remote server, enter:

        ```
			ssh -I /usr/lib64/opensc-pkcs11.so <remote-host>
        ```    

3. At the PIV card password prompt, enter your **PIN**.

> _The **remote-host shell prompt** appears._

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %} 

## Enable PIV for SSH from macOS (10.12 Sierra)

- [**Hardware and software requirements**](#hardware-and-software-requirements)
- [**Configure for PIV login**](#configure-for-piv-login)
- [**Obtain and save public key from PIV**](#obtain-and-save-public-key-from-piv)
- [**SSH to a UNIX-like server**](#ssh-to-log-into-unix-like-server)

### Hardware and software requirements

* A PIV
* A card reader
* A Mac (macOS 10.12 Sierra) computer 
  
### Configure for PIV login

For an open-source method, go to: [**OpenSC**](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}_.)

### Obtain and save public key from PIV

1. Insert your **PIV** into your card reader.
2. To save your **public SSH key** to a file, enter:

        ```
			ssh-keygen -D /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so > mykey.pub
        ```

3. Send the file to the SSH server administrator.

### SSH to a UNIX-like server

1. Insert your **PIV** into your card reader.
2. To log into the remote server, enter:

        ```
		 	ssh -I /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so <remote-host>
        ```

3. At the PIV password prompt, enter your **PIN**.

> _The **remote-host shell prompt** appears._

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}

## Configure a UNIX-like Server

1. Change the configuration in the **/etc/ssh/sshd_config** file and restart the **sshd**:

      ```
		AuthorizedKeysFile /etc/sshd/authorized_keys/%u
		PasswordAuthentication No
      ```

2. Create the **/etc/sshd/authorized_keys** directory:

        ```
			mkdir /etc/sshd/authorized_keys
        ```

3. To allow one person to have access, place his/her PIV's SSH public key in this directory, according to username: **/etc/sshd/authorized_keys/[login ID]**. 
  
>_Only a **root user** may modify this directory and its files to ensure that access requirements are enforced._  
  
4. Disable any alternative means of access (i.e., passwords), as needed.
