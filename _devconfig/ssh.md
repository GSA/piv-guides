---
layout: default
title: SSH
permalink: /devconfig/ssh
collection: devconfig
---

# Using PIV/CAC and Secure Shell (SSH) to Remotely Access UNIX-like Servers from a Windows, Linux, or Mac Computer

As a system administrator (SA), you need the ability to remotely access UNIX-like servers from your computer. Authenticating your PIV/CAC will allow you to use SSH for remote access.

This guide tells you how to:

  * Authenticate your PIV/CAC 
  * Use SSH from your Windows, Linux, or Mac computer
  * Configure a UNIX-like server

For the steps needed to authenticate your PIV/CAC and use SSH, click on the link for your OS: 

  * [Using PIV/CAC and SSH from a Windows Computer](#Using-PIV/CAC-and-SSH-for-Remote-Access-from-a-Windows-Computer)
  * [Using PIV/CAC and SSH from a Linux Computer](#Using-PIV/CAC-and-SSH-for-Remote-Access-from-a-Linux-Computer)
  * [Using PIV/CAC and SSH from a Mac OS X Computer](#Using-PIV/CAC-and-SSH-for-Remote-Access-from-a-Mac-OS-X-Computer)

For the steps needed to configure a UNIX-like server, click on the following link:

  * [Configure a UNIX-like server](#configure-a-unix-like-server)

## Before You Get Started &mdash; More about PIV/CAC Authentication

  * Your PIV/CAC contains an authentication key pair and public certificate.
  * Using the PIV/CAC key pair and public certificate is exactly like using a key pair and self-signed certificate for SSH remote access.

## Using PIV/CAC and SSH for Remote Access from a Windows Computer

### Hardware and software requirements

  * A PIV/CAC card
  * Windows-based computer or workstation
  * A smartcard reader
  * PuTTY-CAC application
  * Pageant application

> _**Note:**  You will download **PuTTY-CAC** and **Pageant** during the steps below._

### Procedures

These steps will ensure that your computer and Jump server recognize your PIV/CAC credential. Your authenticated credential will allow the correct drivers to be enabled on the target Client.

#### Install PuTTY-CAC

**_PuTTY-CAC_** is an SSH client that supports PIV/CAC authentication for Windows.

  1. Download and install [**_PuTTY-CAC_**](https://github.com/NoMoreFood/putty-cac/releases). (PuTTY-CAC is referred to as &quot;**_PuTTY_**&quot; within the application.)
  2. Open PuTTY and click on **_About_** (lower left-hand corner of the **_PuTTY Configuration_** window) to verify that the correct version was installed.

  > _**Note:**  PuTTY will typically be installed at **_C:\Program Files\PuTTY_**.)_

#### Use PIV/CAC to insert Microsoft CAPI key into Pageant

  > **_CAPI_** is Microsoft's Crytographic Application Programming Interface. **_Pageant_** is an SSH authentication agent.

  1. Insert your **_PIV/CAC_** into the smartcard reader.
  2. Open **_Windows Explorer_**.
  3. Open **_Pageant_** and go to **_C:_** &gt; **_Program Files_** &gt; **_PuTTY_** &gt; **_Pageant_**.

  > _A window will not open, but the **Pageant** icon will appear in the Windows taskbar at the bottom of the screen._

  4. Right-click on the **_Pageant_** icon and select **_View Keys &amp; Certs_**.

  > _The Pageant **Key/CAPI Cert List** window will open._

  5. Click on **Add Cert**.
  6. Select your **Smart Card Logon** certificate from the **Windows Security** window.
  7. To verify that this is the correct certificate, click on the link, **_Click here to view certificate properties_**, and then click on **Details**.
  8. Locate and click on **Enhanced Key Usage**. You should see the **Smart Card Logon**. (This will mean that the certificate is the right type.) Then, click on **OK** to close the window.

  > _**Note:**  If multiple certificates exist, you may want to clear the expired or revoked certificates._
 
  9. Click on the **Smart Card certificate** to highlight it, and then click on **OK**.  Then, click on **Close**.

  > _The Pageant window will populate with the certificate information._

  > _**Note:**  You will need to re-add the certificate every time that you start Pageant._

#### Configure PuTTY

##### Set up a PIV login profile

  1. Right-click on the **Pageant** icon from the Windows taskbar and select **New Session**.

  > _This will launch **PuTTY** so you can set up a new profile. (**Note:**  To create new profiles for multiple Jump servers, repeat Steps 2-6 for each profile._
  
  2. Enter the **IP address** of your _Jump server_ in the **Host Name (or IP address)** textbox and follow the remaining steps below.  (If you already have a profile set up, select it, and click on the **Load** button.)

  3. Enter a descriptive name into the **Saved Sessions** textbox.
  4. From the left **Category**: panel, select **Connection** &gt; **SSH** &gt; **CAPI**. Then, click on the checkbox beside the words, **Attempt &quot;CAPI Certificate&quot; (Key-only) auth (SSH-2)**.
  5. From within the **PuTTY Configuration** window, select **Connection** &gt; **SSH** &gt; **Auth**. Then, click on the checkboxes for both **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**.
  6. Click on **Session** from the left panel; enter a name in the **Saved Session** text box; and then click on the **Save** button. 

  > _This completes the profile set-up for the PIV login._

##### Obtain PIV/CAC card's SSH key

  1. To get your PIV card&#39;s **SSH key**, in the **PuTTY Configuration** window, go to the left panel and click on **Connection** &gt; **SSH** &gt; **CAPI**.  Then, under **Authentication Parameters**, click on  the **Browse** button.  

  > _This will automatically fill in the **Cert** and **SSH keystring** textboxes._

  2. Next, copy the **SSH keystring** _value_, paste it into **Microsoft Notepad**, and save it.  

  3. Contact the Jump server support group to provide your **SSH key** and request that they add it to your Jump server account.

  > _**Note**:  For other Jump servers, submit a service ticket to the support group and include the IP address of the Jump server you are using, your account name, and your PIV/CAC's SSH key._

#### Verify your PuTTY login

 > _**Note:**  Once the support group has set up an account with your **SSH key** on the Jumpbox, you'll then be able to use your **PIV card** to log into the Jumpbox._

  1. Run **PuTTY** and select the **Saved Session**. Click on **Load,** and then click on **Open**.
  2. Enter your **remote Unix/Linux account name**.  

  > _A window will open and prompt you for your **PIV card PIN**._

  3. Enter your **PIV card PIN** and click on **OK** to log in.
  4. Once logged in, run the command: **ssh-add –l** to display the key.  

  > _After each server you &quot;jump&quot; to, the output of **ssh-add –l** should always show the key.  After you see the key, you may **ssh** to any other hosts in the environment._

## Using PIV/CAC and SSH for Remote Access from a Linux Workstation

### Hardware and software requirements

  * A PIV card
  * A smartcard reader
  * A Linux-based computer or workstation that is configured to use a PIV/CAC card for login. (For additional information, go to [**conifigure opensc**](https://github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release).)

### Procedures

#### Obtain and save public key from PIV/CAC

  1. Insert your **PIV/CAC** into your computer's smartcard reader.
  2. Use the following command to save the **user&#39;s public SSH key** to a file and submit the file to Jump server administrator.
		
        ```
			ssh-keygen -D /usr/lib64/opensc-pkcs11.so > mykey.pub
        ```  
	
#### Log in via SSH

  1. Insert your **PIV/CAC** into your computer's smartcard reader.

  2. Use the following command to log into the remote machine.
	
        ```
			ssh -I /usr/lib64/opensc-pkcs11.so <remote-host>
        ```    

  3. At the PIV card password prompt, enter your **PIN**. You should see the **_remote-host shell prompt_**.
  
  > **Note:**  The card reader may flash. **Do not** remove the PIV card until the login process has been completed.

## Using PIV/CAC and SSH for Remote Access from a Mac OS X Workstation

### Hardware and software requirements

  * A PIV card
  * A smartcard reader
  * A Mac OS X computer correctly configured to use a PIV card for login. For additional information, go to [**configure opensc**](https://github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release).)

### Procedures

#### Obtain and save public key from PIV card

  1. Insert your **PIV card** into your computer's smartcard reader.
  2. Use the following command to save the **user&#39;s public SSH key** to a file and submit the file to Jump server administrator.

        ```
			ssh-keygen -D /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so > mykey.pub
        ```
	
#### Log in via SSH

  1. Insert your **PIV card** into your computer's card reader.

  2. Use the following command to log into the remote machine. 
        
        ```
		 	ssh -I /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so <remote-host>
        ```

  3. At the PIV card password prompt, enter your **PIN**. You should see remote-host shell prompt.
  
  > **Note:**  The card reader may flash. **Do not** remove the PIV card until the login process has been completed.

## How to Configure a UNIX-like Server

 1. Change the configuration in the **/etc/ssh/sshd_config** file. Then restart the **sshd**.
 
 	```
		AuthorizedKeysFile /etc/sshd/authorized_keys/%u
		PasswordAuthentication No
	```

  2. Create the directory: **/etc/sshd/authorized_keys**.

        ```
			mkdir /etc/sshd/authorized_keys
        ```

  3. To allow one user to have such access, place the user&#39;s PIV card's SSH public key in the following directory, according to the user's name: **/etc/sshd/authorized_keys/[login ID]**. (**Note:** To ensure that access requirements are enforced, only a **root user** may modify this directory and its files.)  

  4. Disable any alternative means of access (i.e., via passwords), as needed.
