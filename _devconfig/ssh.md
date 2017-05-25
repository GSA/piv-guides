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

Select from these sections for your OS: 

  * [SSH using Windows](#ssh-using-windows)
  * [SSH using Linux](#ssh-using-linux)
  * [SSH using Mac OS X](#ssh-using-mac-os-x)
  * [Configure a UNIX-like server](#configure-a-unix-like-server)

## Before You Get Started&mdash;Additional Information about PIV/CAC Authentication

    * Your PIV/CAC contains an authentication key pair and public certificate.
    * Using the PIV/CAC key pair and public certificate is exactly like using a key pair and self-signed certificate for SSH remote access.

## Using PIV/CAC and SSH for Remote Access from a Windows Workstation

### Hardware and software requirements

- A PIV/CAC card
- Windows-based computer or workstation
- A smartcard reader
- PuTTY-CAC application
- Pageant application

> _**Note:**  You will download PuTTY-CAC and Pageant during the steps below._

### Procedures

Use these steps to ensure that your workstation and Jump server recognize your PIV/CAC credential. Your authenticated credential allows the correct drivers to be enabled on the target Client.

#### Install PuTTY-CAC

**_PuTTY-CAC_** is an SSH client that supports PIV/CAC authentication.

1. Download and install [**_PuTTY-CAC_**](https://github.com/NoMoreFood/putty-cac/releases). (PuTTY-CAC is referred to as &quot;**_PuTTY_**&quot; within the application.)
2. Open PuTTY and click on **_About_** (lower left-hand corner of the **_PuTTY Configuration_** window) to verify that the correct version was installed.

> _**Note:**  **PuTTY** will typically be installed at **_C:\Program Files\PuTTY_**.)_

#### Use PIV/CAC to insert Microsoft CAPI Key into Pageant

> **_CAPI_** is Microsoft's Crytographic Application Programming Interface. **_Pageant_** is an SSH authentication agent.

1. Insert your **_PIV/CAC_** into the card reader.
2. Open **_Windows Explorer_**.
3. Open **_Pageant_** and go to **_C:_** &gt; **_Program Files_** &gt; **_PuTTY_** &gt; **_Pageant_**.

> _A window will not open, but the **Pageant** icon will appear in the Windows taskbar at the bottom of the screen._

4. Right-click on the **_Pageant_** icon and select **_View Keys &amp; Certs_**.

> _The Pageant **Key/CAPI Cert List** window will open._

5. Click on **Add Cert**.
6. Select your **Smart Card Logon** certificate from the **Windows Security** window.
7. To verify that this is the correct certificate, click on the link, **Click here to view certificate properties**, and then click on **Details**.
8. Locate and click on **Enhanced Key Usage**. You should see the **Smart Card Logon**. (This will mean that the certificate is the right type.)

> _**Note:**  If multiple certificates exist, you may want to clear out the expired or revoked certificates._

9. Click on **OK** to close the **Details** window.
10. Click on the **Smart Card certificate** to highlight it, and then click on **OK**.

> _The Pageant window will populate with the certificate information._

11. Click on **Close**.

> _**Note:**  You'll need to re-add the certificate every time that you start **Pageant**._

#### Configure PuTTY

1. Right-click on the **Pageant** icon again from the Windows taskbar and select **New Session**.  (This will launch **PuTTY**.)

> _From within **PuTTY**, you'll need to set up a new profile._  

2. Enter the **IP address** of your _Jump server_ in the **Host Name (or IP address)** textbox and follow the remaining steps below.  (If you already have a profile set up, select it, and click on the **Load** button.)

> _**Note:**  If you want to create new profiles for multiple Jump servers, you'll need to repeat the following steps for each profile._

3. Enter a descriptive name into the **Saved Sessions** textbox.
4. From the left **Category**: panel, select **Connection** &gt; **SSH** &gt; **CAPI**. Then, click on the checkbox beside the words, **Attempt &quot;CAPI Certificate&quot; (Key-only) auth (SSH-2)**.
5. From within the **PuTTY Configuration** window, select **Connection** &gt; **SSH** &gt; **Auth**. Then, click on the checkboxes for both **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**.
6. Click on **Session** from the left panel; enter a name in the **Saved Session** text box; and then click on the **Save** button. 

> _This sets up a profile for PIV logon._

7. To get your PIV card&#39;s **SSH key**, in the **PuTTY Configuration** window, go to the left panel and click on **Connection** &gt; **SSH** &gt; **CAPI**.  Then, under **Authentication Parameters**, click on  the **Browse** button.  

> _This will automatically fill in the **Cert** and **SSH keystring** textboxes._

8. Next, copy the **SSH keystring** _value_, paste it into **Microsoft Notepad**, and save it.  

> _You'll need the **SSH keystring value** (i.e., _SSH key_) when you contact the Jump server support team (as in Step 9) or if you need to create a service ticket._

9. Contact the Jump server support group to request that they add your **PIV card&#39;s SSH key** to **your account on the Jump server**.

> _**Note**:  For other Jump servers, submit a service ticket to that support group and include the **IP address** of the Jump server you are using, **your account name**, and the **SSH key** from your **PIV card**._

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
  * A Linux workstation or computer that is correctly configured to use a PIV/CAC card for login. (For additional information, go to [**conifigure opensc**](https://github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release).)

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

  3. At the PIV card password prompt, enter your **PIN**. You should see remote-host shell prompt.
  
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
