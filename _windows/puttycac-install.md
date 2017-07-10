---
layout: default
title: PuTTY-CAC Installation - Windows
permalink: /windows/puttycac-install
collection: windows
---

### Background
Most Unix-like systems are configured to use the SSH protocol for remote access, but most SSH client applications do not support PIV as required by Federal policy.  Putty-CAC, a fork of the Open Source Putty SSH client, resolves this issue.

> *Note that [Van Dyke Secure CRT](https://www.vandyke.com/products/securecrt/index.html), a commercial product, also supports PIV SSH login for multiple platforms, including Windows and Mac.*

### Installing PuTTY-CAC
1. If you have a forge.mil account, download the latest Putty-CAC package from forge.mil. If you do not have access to forge.mil, you can also download it at [https://risacher.org/putty-cac](https://risacher.org/putty-cac). Source code is available at [https://github.com/risacher/putty-cac](https://github.com/risacher/putty-cac)
2. There is no installer available for the binaries, so you must either:<br>
● Place the executable files in a directory that you have execute rights over.<br>
● Build an installation package to install the executables in the location you choose.  This will enable the Putty-CAC applications to be available from the Start Menu.<br>
> *At a minimum, you must install the following packages:*<br>
> ● putty.exe<br>
> ● pageant.exe<br>
3. Verify the version of PuTTY that was installed by opening the application and clicking About in the lower left corner.
4. Launch pageant from the PuTTY install directory, (eg, C:\Program Files\Putty-CAC). Pageant will appear in the taskbar on the bottom right of your desktop;it will not open a window. 
5. You must now insert the CAPI Key and configure PuTTY-CAC. Follow the steps below.

## Add CAPI Key into Pageant

1. Open Windows Explorer or click Start > Computer.
2. Open Pageant by clicking the executable. 
3. A window will not open, but  the Pageant icon will appear on the menu bar. Right-click the icon and select View Keys.
4. The Pageant Key List window will appear. Click Add CAPI Cert.
5. Select your Smart Card Logon certificate from the Windows Security window.
> ● Make sure you choose the correct certificate! Select “Click here to view certificate properties,” click “Details,” scroll half-way, and locate Enhanced Key Usage. It should begin with “Smart Card Logon;” this indicates it is the correct certificate. If you do not see this field, select a different certificate.<br>
> *Note: If multiple certificates exist, you may want to clear out the expired or revoked certificates by following How To – **FIXME: PIV Card – Clear certificate store***. <br>
 ● Click OK to close the details window.
6. Highlight the correct Smart Card certificate and click OK.
7. The Pageant Window will now display the certificate information.
8. Click Close. 
> *Warning: You must  re-add your certificate every time pageant is started.*

### Configure PuTTY-CAC

1. Right-click the Pageant icon again from the menu bar and select New Session. This will launch PuTTY.
2. From within PuTTY, enter the destination IP address or hostname in the Host Name (or IP address) textbox to setup a new profile, or if you already have profiles set up in PuTTY, load that profile. 
> Note: If you have multiple destination profiles, you will have to do the following steps for each profile
3. Enter a descriptive name under Saved Sessions textbox (if setting up a new profile).
4. On left panel, select Connection > SSH > CAPI thencheck the box beside the words Attempt “CAPI Certificate” (Key-only) auth (SSH-2).
5. From within PuTTY, select Connection > SSH > Auth then select both “Allow agent forwarding” and “Allow attempted changes of username in SSH-2.”
6. Click Session, then Save. This profile is now configured for PIV logon.
7. To get your PIV card’s SSH key, in PuTTY, go to Connection > SSH > CAPI  and select the browse button on the right side. This will automatically fill in the “Cert” and “SSH keystring” fields. 
8. Copy and paste the SSH keystring value from PuTTY into Notepad as you will need to include the SSH key when you contact the jumpbox support team or create a service ticket.
> The configuration file should contain “Host *” and “ForwardAgent yes” and exist in the same folder where they place the SSH key.
9. In Saved Sessions, click Save to save your configuration.


### Verify PIV Login

1. Open Pageant (if not already running) and make sure your CAPI key is populated, close the Pageant window. Right click the Pageant icon and choose “New Session”. This will open PuTTY-CAC.
2. Load one of your saved sessions that you previously configured for PIV logon.
3. When prompted, enter your remote Unix/Linux account name, and you should be prompted for your PIV PIN.
4. Enter your PIN, click OK and you should be logged in.
5. Once logged in, run ‘ssh-add –l’ to ensure that the forwarding agent is working. If you do not see the key printed when you run this command, something is wrong and you will not be prompted for your PIN if you ssh further into the environment.
6. Both the cert key that was pasted into the .ssh/authorized_keys and the config file need to be copied or scp’d to all the servers you will connect to in the data center. If the forwarding agent is working when you ssh to a server beyond the jumphost, you should be prompted for the PIN again.
7. After each server you ‘jump’ to, the output of ssh-add –l should always show the key. If not, either permissions are wrong or a file is mislabeled, or missing.

