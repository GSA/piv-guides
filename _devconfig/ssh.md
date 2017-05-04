---
layout: default
title: SSH
permalink: /devconfig/ssh
collection: devconfig
---
# How do I enable PIV/CAC for Secure Shell (SSH) to a Unix-like system from Windows?

These procedures are intended for network and system administrators, or other IT professionals, who are responsible for the day-to-day network operations of Federal Government agencies.  As part of their roles, these professionals will be authorized by their agencies to use secure methods to remotely access other computer hosts.

For those professionals who use Windows-based systems, **PuTTY** allows for remote access. PuTTY is an open-source terminal emulator, serial console, and network file transfer application. It supports network protocols such as Secure Copy (SCP), Secure Shell (SSH), Telnet, rlogin, and &quot;raw socket&quot; connections. It can also be used to connect to a serial port.

## Hardware and software requirements

- Windows-based Workstation or Computer
- PuTTY Application
- Pageant Application

> _**Note:**  You will download the required applications during the steps below._

## Procedures

### Install PuTTY-CAC

1. To download and install **PuTTY-CAC**, go to: [https://github.com/NoMoreFood/putty-cac/releases](https://github.com/NoMoreFood/putty-cac/releases).  (PuTTY-CAC is referred to as &quot;PuTTY&quot; within the application.)
2. Open PuTTY and click on **About** (lower left-hand corner of the **PuTTY Configuration** window) to verify that the correct version was installed.

> _**Note:** PuTTY will typically be installed at C:\Program Files\PuTTY.)_

### Insert CAPI Key into Pageant

> _**CAPI** is Microsoft's Crytographic Application Programming Interface._

1. Insert your **PIV card** into the card reader.
2. Open **Windows Explorer**.
3. Open **Pageant** by clicking **C:** &gt; **Program Files** &gt; **PuTTY** &gt; **Pageant**.

> _A window will not open, but the **Pageant** icon will appear in the Windows taskbar at the bottom of your screen._

4. Right-click on the **Pageant** icon and select **View Keys &amp; Certs.**

> _The Pageant **Key/CAPI Cert List** window will open._

5. Click on **Add Cert**.
6. Select your **Smart Card Logon** certificate from the **Windows Security** window.
7. To verify that this is the correct certificate, click on the link, **Click here to view certificate properties**, and then click on **Details**.
8. Locate and click on **Enhanced Key Usage**. You should see the **Smart Card Logon**. (This will mean that the certificate is the right type.)

> _**Note:** If multiple certificates exist, you may want to clear out the expired or revoked certificates._

9. Click on **OK** to close the **Details** window.
10. Click on the **Smart Card certificate** to highlight it, and then click on **OK**.

> _The **Pageant** window will populate with the certificate information._

11. Click on **Close**.

> _**Note:** You will need to re-add the certificate every time that you start **Pageant**._

### Configure PuTTY

1. Right-click on the **Pageant** icon again from the Windows taskbar and select **New Session**.  (This will launch **PuTTY**.)

> _From within **PuTTY**, you'll need to set up a new profile._  

2. Enter the **IP address** of your _Jumpbox_ in the **Host Name (or IP address)** textbox and follow the remaining steps below.  (If you already have a profile set up, select it, and click on the **Load** button.)

> _**Note:** If you want to create new profiles for multiple Jumpboxes, you'll need to repeat the following steps for each profile._

3. Enter a descriptive name into the **Saved Sessions** textbox.
4. From the left **Category** : panel, select **Connection** &gt; **SSH** &gt; **CAPI**. Then, check the box beside the words **Attempt &quot;CAPI Certificate&quot; (Key-only) auth (SSH-2)**.
5. From within the **PuTTY Configuration** window, select **Connection** &gt; **SSH** &gt; **Auth**.Then, click the checkboxes forboth **Allow agent forwarding** and **Allow attempted changes of username in SSH-2**.
6. Click on **Session** from the left panel; enter a name in the **Saved Session** text box; andthenclick on the **Save** button. ** (**This sets up a profile for PIV logon.)
7. To get your PIV card&#39;s **SSH key** , in the **PuTTY Configuration** window, go to the left panel and click on **Connection** &gt; **SSH** &gt; **CAPI**.  Then, under **Authentication Parameters** , click on  the **Browse** button.  (This will automatically fill in the **Cert** and **SSH keystring** textboxes.)
8. Next, copy the **SSH keystring** value and paste it into **Microsoft Notepad** and save it.  (You will need the SSH key when you contact the Jumpbox support team in Step 9 or if you need to create a service ticket.)
9. Contact the Jumpbox support group to request that they add your **PIV card&#39;s SSH key** to **your account on the Jumpbox**.

> _**Note** : For other Jumpboxes, submit a service ticket to that support group and include the IP address of the Jumpbox you are using, your account name, and the SSH key from your PIV card._

### Verify PuTTY logon

> _**Note:** Once the support group has set up an account with your SSH key on the Jumpbox, then you can use your PIV card to login to the Jumpbox._

1. Run **PuTTY** and select the Saved Session. Click on **Load,** and then click on **Open**.
2. Enter your remote Unix/Linux account name.  A window will open and prompt you for your PIV PIN.
3. Enter your PIN and click on **OK** to log in.
4. Once logged in, run the command:   **ssh-add –l** to display the key.  (After each server you &quot;jump&quot; to, the output of **ssh-add –l** should always show the key.  After you see the key, you can ssh to any other hosts in the environment.)
