---
layout: default
title: SSH
permalink: /devconfig/ssh
collection: devconfig
---
# How do I enable PIV/CAC for Secure Shell (SSH) to a Unix-like system from Windows?

These procedures are intended for network and system administrators, or other IT professionals, who are responsible for the day-to-day network operations of Federal Government agencies.  As part of their roles, these professionals will be authorized by their agencies to use secure methods to remotely access other computer hosts.

For those professionals who use Windows-based systems, **PuTTY** is one method of remote access. PuTTY is an open-source terminal emulator, serial console, and network file transfer application. It supports network protocols such as Secure Copy (SCP), Secure Shell (SSH), Telnet, rlogin, and &quot;raw socket&quot; connections. It can also be used to connect to a serial port.

## Hardware and software requirements

- Windows-based Workstation or Computer
- PuTTY Application
- Pageant Application

> **Note:**  You will download the required applications during the steps below.
## Procedures

## Install PuTTY-CAC

1. To download and install **PuTTY-CAC**, go to: [https://github.com/NoMoreFood/putty-cac/releases](https://github.com/NoMoreFood/putty-cac/releases).  (PuTTY-CAC is referred to as &quot;PuTTY&quot; within the application.)
2. Open PuTTY and click on **About** (lower left-hand corner of the **PuTTY Configuration** window) to verify that the correct version was installed.

> **Note:** PuTTY will typically be installed at C:\Program Files\PuTTY.)

## Insert CAPI Key into Pageant

1. Insert your PIV card into the card reader.
2. Open **Windows**** Explorer**.
3. Open **Pageant** by clicking **C:** &gt; **Program Files** &gt; **PuTTY** &gt; **Pageant**.

> A window will not open but the Pageant icon will appear in the Windows taskbar.

1. Right-click the icon and select **View Keys &amp; Certs.**

The Pageant **Key/CAPI Cert List** window will appear.

1. Click **Add Cert**.
2. Select your **Smart Card Logon** certificate from the **Windows Security** window.
3. To ensure that this is the correct certificate, click on the link **Click here to view certificate properties** and then click on **Details**.
4. Locate and click on **Enhanced Key Usage**.  You should see the **Smart Card Logon**.  (This indicates that the certificate is the right type.)

**Note:** If multiple certificates exist, you may want to clear out the expired or revoked certificates.

1. Click **OK** to close the Details window.
2. Click on the Smart Card certificate to highlight it and then click on **OK**.
3. The Pageant window will populate with the certificate information.
4. Click on **Close**.

**Note:** The certificate needs to be re-added every time Pageant is started.

## Configure PuTTY

1. Right-click on the **Pageant** icon again from the Windows taskbar and select **New Session**.  (This will launch PuTTY.)
2. From within PuTTY, enter the IP address of your _Jumpbox_ in the **Host Name (or IP address)** textbox to set up a new profile. Follow the remaining steps below.  (If you already have a profile set up, select it, and click on the **Load** button.)

**Note:** If you are creating new profiles for multiple Jumpboxes, you will have to repeat the following steps for each profile.

1. Enter a descriptive name into the **Saved Sessions** textbox.
2. From the left **Category** : panel, select **Connection** &gt; **SSH** &gt; **CAPI**. Then, check the box beside the words **Attempt &quot;CAPI Certificate&quot; (Key-only) auth (SSH-2)**.
3. From within the **PuTTY Configuration** window, select **Connection** &gt; **SSH** &gt; **Auth**.Then, click the checkboxes forboth **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**.
4. Click on **Session** from the left panel; enter a name in the **Saved Session** text box; andthenclick on the **Save** button. ** (**This sets up a profile for PIV logon.)
5. To get your PIV card&#39;s **SSH key** , in the **PuTTY Configuration** window, go to the left panel and click on **Connection** &gt; **SSH** &gt; **CAPI**.  Then, under **Authentication Parameters** , click on  the **Browse** button.  (This will automatically fill in the **Cert** and **SSH keystring** textboxes.)
6. Next, copy the **SSH keystring** value and paste it into **Microsoft Notepad** and save it.  (You will need the SSH key when you contact the Jumpbox support team in Step 9 or if you need to create a service ticket.)
7. Contact the Jumpbox support group to request that they add your **PIV card&#39;s SSH key** to **your account on the Jumpbox**.

**Note** : For other Jumpboxes, submit a service ticket to that support group and include the IP address of the Jumpbox you are using, your account name, and the SSH key from your PIV card.

**Verify PuTTY logon**

Note: Once the support group has set up an account with your SSH key on the Jumpbox, then you can use your PIV card to login to the Jumpbox.

1. Run **PuTTY** and select the Saved Session. Click on **Load,** and then click on **Open**.
2. Enter your remote Unix/Linux account name.  A window will open and prompt you for your PIV PIN.
3. Enter your PIN and click on **OK** to log in.
4. Once logged in, run the command:   **ssh-add –l** to display the key.  (After each server you &quot;jump&quot; to, the output of **ssh-add –l** should always show the key.  After you see the key, you can ssh to any other hosts in the environment.)
