---
layout: default
title: Use PIV/CAC for Secure Shell (SSH) to a UNIX-like Server
permalink: /devconfig/ssh-all
collection: devconfig
---

To use SSH for remote access to a UNIX-like server, you need to authenticate your PIV/CAC. You can authenticate your PIV/CAC and use SSH from a Windows, Linux, or Mac workstation/computer. For remote access, you also need to configure the targeted UNIX-like server. 

Select the link for your operating system (OS). (Also, please review _Configure a UNIX-like Server_.)

  * [Use PIV/CAC for SSH from a Windows Computer](#use-piv/cac-for-ssh-from-a-windows-computer)
  * [Using PIV/CAC and SSH from a Linux Computer](#using-piv/cac-and-ssh-for-remote-access-from-a-linux-computer)
  * [Using PIV/CAC and SSH from a Mac OS X Computer](#Using-piv/cac-and-ssh-for-remote-access-from-a-mac-os-x-computer)
  * [Configure a UNIX-like Server](#configure-a-unix-like-server)

## About PIV/CAC Key Pairs and Public Certificates

  * Your PIV/CAC contains an authentication key pair and public certificate.
  * Using the PIV/CAC key pair and public certificate is exactly like using a key pair and self-signed certificate for SSH remote access.

## Use PIV/CAC for SSH from a Windows-Based Computer

### Hardware and software requirements

  * A PIV/CAC
  * Windows-based computer
  * A smartcard reader
  * PuTTY-CAC application
  * Pageant application

> _**Note:**  You will download **PuTTY-CAC** and **Pageant** in the steps below._

### Procedures

These steps will help you to:

  * Authenticate your PIV/CAC
  * Ensure that your Windows-based computer and Jump server recognize your PIV/CAC 
  * Enable the correct drivers on your computer so you can use SSH for remote access

#### Install PuTTY-CAC

**_PuTTY-CAC_** is an open-source SSH client that supports PIV/CAC authentication.

  1. Download and install [**_PuTTY-CAC_**](https://github.com/NoMoreFood/putty-cac/releases). (Within the application, PuTTY-CAC is referred to simply as "**_PuTTY_**.") (PuTTY will typically be installed at **_C:\Program Files\PuTTY_**.)
  2. Open PuTTY and click on **_About_** (lower left-hand corner of the **_PuTTY Configuration_** window) to verify that the correct version was installed.

#### Use PIV/CAC to insert Microsoft CAPI key into Pageant

**_CAPI_** is Microsoft's Crytographic Application Programming Interface. **_Pageant_** is an SSH authentication agent that you use with PuTTY-CAC.

  1. Insert your **_PIV/CAC_** into the smartcard reader.
  2. Open **_Windows Explorer_**.
  3. Open **_Pageant_** and go to **_C:_** &gt; **_Program Files_** &gt; **_PuTTY_** &gt; **_Pageant_**.

  > _A window will not open, but the **Pageant** icon will appear at the bottom of the screen in the Windows taskbar._

  4. Right-click on the **_Pageant_** icon and select **_View Keys &amp; Certs_**.

  > _The Pageant **Key/CAPI Cert List** window will open._

  5. Click on **Add Cert**.
  6. Select your **Smart Card Logon** certificate from the **Windows Security** window.
  7. To verify that this is the correct certificate, click on **_Click here to view certificate properties_** &gt; &#8594; **Details**.
  8. Locate and click on **Enhanced Key Usage**. You should see the **Smart Card Logon**. (This will mean that the certificate is the right type.) Then, click on **OK** to close the window.

  > _**Note:**  If multiple certificates exist, you may want to clear the expired or revoked certificates._
 
  9. Click on the **Smart Card certificate** to highlight it, and then click on **OK**.  Then, click on **Close**.

  > _The Pageant window will populate with the certificate information._

  > _**Note:**  You will need to re-add the certificate every time that you start Pageant._

#### Configure PuTTY

##### Set up a PIV/CAC login profile

  1. Right-click on the **Pageant** icon from the Windows taskbar and select **New Session**.

  > _This will launch **PuTTY** so you can set up a new profile. (**Note:**  To create new profiles for multiple Jump servers, repeat Steps 2-6 for each profile._)
  
  2. Enter the **IP address** of your _Jump server_ in the **Host Name (or IP address)** textbox and follow the remaining steps below.  (If you already have a profile set up, select it, and click on the **Load** button.)

  3. Enter a descriptive name into the **Saved Sessions** textbox.
  4. From the left **Category**: panel, select **Connection** &gt; **SSH** &gt; **CAPI**. Then, click on the checkbox beside the words, **Attempt &quot;CAPI Certificate&quot; (Key-only) auth (SSH-2)**.
  5. From within the **PuTTY Configuration** window, select **Connection** &gt; **SSH** &gt; **Auth**. Then, click on the checkboxes for both **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**.
  6. Click on **Session** from the left panel; enter a name in the **Saved Session** text box; and then click on the **Save** button. 

  > _This completes the profile set-up for the PIV/CAC login._

##### Obtain PIV/CAC's SSH key

  1. To get your PIV card&#39;s **SSH key**, in the **PuTTY Configuration** window, go to the left panel and click on **Connection** &gt; **SSH** &gt; **CAPI**.  Then, under **Authentication Parameters**, click on  the **Browse** button.  

  > _This automatically fills in the **Cert** and **SSH keystring** textboxes._

  2. Next, copy the **SSH keystring** _value_, paste it into **Microsoft Notepad**, and save it.  

  3. Contact the Jump server administrator to provide your **SSH key** and request that it be added to your Jump server account.
  
  > _**Note:**  Once the administrator has set up an account with your **SSH key** on the Jump server, you will be able to use your PIV/CAC to log into the Jump server. For other Jump servers, submit a service ticket to the administrator and include the IP address of the Jump server you are using, your account name, and your PIV/CAC's SSH key._

#### Verify your PuTTY login and proceed with SSH

  1. Run **PuTTY** and select the **Saved Session**. 
  2. Click on **Load,** and then click on **Open**.
  3. Enter your **remote UNIX/Linux account name**.  

  > _A window will open and prompt you for your **PIV card PIN**._

  4. Enter your **PIV card PIN** and click on **OK** to log into the remote server.
  5. Once logged in, run the command: **ssh-add –l** to display the key.  

  > _After each server you &quot;jump&quot; to, the output of **ssh-add –l** should always show the key._ 
  
  > _After you see the key, you may **ssh** to any other hosts in the environment._

## Using PIV/CAC and SSH for Remote Access from a Linux Computer

### Hardware and software requirements

  * A PIV/CAC card
  * A smartcard reader
  * A Linux-based computer or workstation that is configured to use a PIV/CAC card for login. (For additional information, go to [**configure opensc**](https://github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release).)

### Procedures

#### Obtain and save public key from PIV/CAC

  1. Insert your PIV/CAC into your computer's smartcard reader.
  2. To save your **public SSH key** to a file, enter the command: 
		
        ```
			ssh-keygen -D /usr/lib64/opensc-pkcs11.so > mykey.pub
        ```  
  3. Submit the file with your public SSH key to the Jump server administrator.	

#### Log in via SSH

  1. Insert your **PIV/CAC** into your computer's smartcard reader.

  2. Use the following command to log into the remote server:
	
        ```
			ssh -I /usr/lib64/opensc-pkcs11.so <remote-host>
        ```    

  3. At the PIV card password prompt, enter your **PIN**. 
  
  > The **_remote-host shell prompt_** appears.

The card reader may flash. **Do not** remove the PIV/CAC until the login process has been completed.{:class="alert"}  

## Using PIV/CAC and SSH for Remote Access from a Mac OS X Computer

### Hardware and software requirements

  * A PIV/CAC card
  * A smartcard reader
  * A Mac OS X computer correctly configured to use a PIV/CAC for login. For additional information, go to [**configure opensc**](https://github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release).

### Procedures

#### Obtain and save public key from PIV card

  1. Insert your **PIV card** into your computer's smartcard reader.
  2. Use the following command to save the **user&#39;s public SSH key** to a file and submit the file to Jump server administrator.

        ```
			ssh-keygen -D /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so > mykey.pub
        ```
	
#### Log in via SSH

  1. Insert your **PIV/CAC** into your computer's smartcard reader.

  2. Use the following command to log into the remote server: 
        
        ```
		 	ssh -I /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so <remote-host>
        ```

  3. At the PIV/CAC password prompt, enter your **PIN**. 
  
  > The **remote-host shell prompt** appears.
  
The card reader may flash. **Do not** remove the PIV/CAC until the login process has been completed.{:class="alert"}  

## Configure a UNIX-like Server

 1. Change the configuration in the **/etc/ssh/sshd_config** file. Then restart the **sshd**:
 
 	```
		AuthorizedKeysFile /etc/sshd/authorized_keys/%u
		PasswordAuthentication No
	```

  2. Create the directory: **/etc/sshd/authorized_keys**:

        ```
			mkdir /etc/sshd/authorized_keys
        ```

  3. To allow one user to have such access, place the user&#39;s PIV card's SSH public key in the following directory, according to the user's name: **/etc/sshd/authorized_keys/[login ID]**. (**Note:** To ensure that access requirements are enforced, only a **root user** may modify this directory and its files.)  

  4. Disable any alternative means of access (i.e., via passwords), as needed.
