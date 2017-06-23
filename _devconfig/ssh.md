---
layout: default
title: Use PIV for Secure Shell (SSH)
permalink: /devconfig/ssh
collection: devconfig
---

To use SSH for remote access to a UNIX-like server, you need to first authenticate your PIV. PIV authentication and SSH can be done from a Windows, Linux, or Mac-based computer. For remote access, you also need to configure the UNIX-like server.

Select the link for your operating system (OS). (Also, please review _Configure a UNIX-like Server_.)

  * [Use PIV for SSH from a Windows Computer](#use-piv-for-ssh-from-a-windows-computer)
  * [Use PIV for SSH from a Linux Computer](#use-piv-for-ssh-from-a-linux-computer)
  * [Use PIV for SSH from a Mac Computer](#use-piv-for-ssh-from-a-mac-computer)
  * [Configure a UNIX-like Server](#configure-a-unix-like-server)
  
{% include alert-info.html heading = "Your PIV contains an authentication key pair and public certificate. Using a PIV key pair and public certificate is exactly like using a key pair and self-signed certificate for SSH remote access." %}&nbsp;

## Use PIV for SSH from a Windows Computer

### Hardware and software requirements

  * A PIV
  * Windows computer
  * A smartcard reader
  * PuTTY-CAC application (an open-source SSH client that supports PIV authentication)
  * Pageant application (an SSH authentication agent used with PuTTY-CAC)

  > _**Note:**  You will download **PuTTY-CAC** and **Pageant** in the steps below._

### Procedures

These steps will help you to:

  * Authenticate your PIV
  * Ensure that your Windows computer and Jump server recognize your PIV
  * Enable the correct drivers on your computer for SSH

#### Install PuTTY-CAC

  1. Download and install [**PuTTY-CAC**](https://www.github.com/NoMoreFood/putty-cac/releases){:target="_blank"}. (Within the application, PuTTY-CAC is referred to simply as "**PuTTY**." PuTTY will usually be installed at **C:\Program Files\PuTTY**.)
  2. Open PuTTY and click on **About** (lower left-hand corner of the **PuTTY Configuration** window) to ensure that the correct version was installed.

#### Use PIV to insert Microsoft CAPI key into Pageant
 
  > **Note:**  The **CAPI key** is the "Smart Card certificate" discussed in Step 9. 

  1. Insert your **PIV** into the smartcard reader.
  2. Open **Windows Explorer**.
  3. Open **Pageant** and go to **C: &gt; Program Files &gt; PuTTY &gt; Pageant**.

  > A window will not open, but the **Pageant** icon will appear at the bottom of the screen in the Windows taskbar.

  4. Right-click on the **Pageant** icon and select **View Keys &amp; Certs**.

  > _The Pageant **Key/CAPI Cert List** window will open._

  5. Click on **Add Cert**.
  6. Select your **Smart Card Logon** certificate from the **Windows Security** window.
  7. To ensure that this is the correct certificate, click on **Click here to view certificate properties &gt; Details**.
  8. Locate and click on **Enhanced Key Usage**. You should see the **Smart Card Logon**. (This means that the certificate is the right type.) Click on **OK** to close the window.

  > _**Note:**  If multiple certificates exist, you may want to clear the expired or revoked certificates._

  9. Click on the **Smart Card certificate** to highlight it. Then click on **OK** and **Close**.

  > _The Pageant window will populate with the certificate information. (**Note:**  Every time you start Pageant, you must re-add the certificate._)

#### Configure PuTTY

##### Set up a PIV login profile

  1. Right-click on the **Pageant** icon from the Windows taskbar. Select **New Session** to launch **PuTTY**.

  > _Use PuTTY to set up a new PIV login profile for a Jump server. To create new profiles for multiple Jump servers, repeat Steps 2-6 for each Jump server._

  2. Enter the **IP address** of the Jump server in the **Host Name (or IP address)** textbox. (If you already have a profile for the Jump server, select it, and click on the **Load** button. Otherwise, follow Steps 3-6 to set up the profile.)
  3. Enter a session name into the **Saved Sessions** textbox.
  4. From the left **Category**: panel, select **Connection &gt; SSH &gt; CAPI**. Then, click on the checkbox for **Attempt "CAPI Certificate" (Key-only) auth (SSH-2)**.
  5. From within the **PuTTY Configuration** window, select **Connection &gt; SSH &gt; Auth**. Next, click on the checkboxes for **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**.
  6. Finally, click on **Session** from the left panel and enter a name in the **Saved Session** textbox. Click on the **Save** button.

##### Obtain PIV's SSH key

  1. To get your PIV's **SSH key**, go to the **PuTTY Configuration** window. In the left panel, click on **Connection &gt; SSH &gt; CAPI**.  Under **Authentication Parameters**, click on  the **Browse** button.  

  > _This automatically fills in the **Cert** and **SSH keystring** textboxes._

  2. Copy and paste the **SSH keystring** **_value_** (i.e., SSH key) into **Microsoft Notepad** and save it.  
  3. Provide your SSH key to the Jump server administrator and ask that it be added to your Jump server account.

  > _**Note:**  Once the Jump server account has been set up with your SSH key, you can use your PIV to log in. For other Jump servers, submit a service ticket to the administrator and include the IP address of the Jump server you are using, your account name, and your PIV's SSH key._

#### Verify your PuTTY login and proceed with SSH

  1. Run **PuTTY** and select the **Saved Session**.
  2. Click on **Load** and then on **Open**.
  3. Enter your **remote UNIX/Linux account name**.  
  4. At the prompt, enter your **PIV card PIN** and click on **OK** to log into the remote server.
  5. Once logged in, run the command: **ssh-add –l** to display the SSH key.  

  > _For each server you "jump" to, use **ssh-add –l** to display the SSH key. Once you see the key, you may **ssh** to any other hosts in the environment._

## Use PIV for SSH from a Linux Computer

### Hardware and software requirements

  * A PIV
  * A smartcard reader
  * A Linux computer that is configured to use a PIV for login. (For additional information, go to [**configure opensc**](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}.)

### Procedures

These steps will help you to:

  * Authenticate your PIV
  * Enable you to use SSH for remote access

#### Obtain and save public key from PIV

  1. Insert your **PIV** into your computer's smartcard reader.
  2. To save your **public SSH key** to a file, enter:

        ```
			ssh-keygen -D /usr/lib64/opensc-pkcs11.so > mykey.pub
        ```  
  3. Submit the file with your public SSH key to the Jump server administrator.

#### Log in via SSH

  1. Insert your **PIV** into your computer's smartcard reader.
  2. To log into the remote server, enter:

        ```
			ssh -I /usr/lib64/opensc-pkcs11.so <remote-host>
        ```    

  3. At the PIV card password prompt, enter your **PIN**.

  > _The **remote-host shell prompt** appears._

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}&nbsp; 

## Use PIV for SSH from a Mac (macOS 10.12 Sierra) Computer

### Hardware and software requirements

  * A PIV
  * A smartcard reader
  * A Mac (macOS 10.12 Sierra) computer configured for PIV login. For additional information, go to [**configure opensc**](https://www.github.com/OpenSC/OpenSC/wiki/Download-latest-OpenSC-stable-release){:target="_blank"}.

### Procedures

These steps will help you to:

  * Authenticate your PIV
  * Enable you to use SSH for remote access

#### Obtain and save public key from PIV card

  1. Insert your **PIV** into your computer's smartcard reader.
  2. Use the following command to save the **user's public SSH key** to a file and submit it to Jump server administrator.

        ```
			ssh-keygen -D /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so > mykey.pub
        ```

#### Log in via SSH

  1. Insert your **PIV** into your computer's smartcard reader.
  2. Use the following command to log into the remote server:

        ```
		 	ssh -I /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so <remote-host>
        ```

  3. At the PIV password prompt, enter your **PIN**.

  > The **remote-host shell prompt** appears.

{% include alert-warning.html heading = "The card reader may flash. **Do not** remove the PIV until the login process has been completed." %}&nbsp;

## Configure a UNIX-like Server

### Procedures

These steps will help you to configure a UNIX-like server for remote access.

  1. Change the configuration in the **/etc/ssh/sshd_config** file and restart the **sshd**:

      ```
		AuthorizedKeysFile /etc/sshd/authorized_keys/%u
		PasswordAuthentication No
      ```

  2. Create the directory, **/etc/sshd/authorized_keys**:

        ```
			mkdir /etc/sshd/authorized_keys
        ```

  3. To allow one user to have access, place the user's PIV's SSH public key in this directory, according to the user's name: **/etc/sshd/authorized_keys/[login ID]**. (**Note:** Only a **root user** may modify this directory and its files. This ensures that access requirements are enforced.)  
  4. Disable any alternative means of access (i.e., via passwords), as needed.
