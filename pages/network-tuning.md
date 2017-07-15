
## Network Tuning / Issue 50


# Use a table?
Someone (not sure who now) had mentioned this should be in table, but formatting table cells is so limited with markdown I'm thinking this isn't the direction we should go. Even a numbered list will need to be done manually and cannot have a carriage return in it - I think it has to be entered all on one line and they'll be no support for code blocks or info boxes  e.g.,

	1<wbr>. Open XYZ<br>2. Click this<br>3. Close that<br>4. All done

| **Field** | **Value** |
| :-------- | :------------------------------- |
| Cached logon credential limit | 1<wbr>. Open XYZ<br>2. Click this<br>3. Close that<br>4. All done |
| Increase the network retrieval timeout setting on your domain | https://technet.microsoft.com/en-us/library/cc771429(v=ws.11).aspx |
| Increase the OCSP setting from the default of "50" to a higher number referenced here under Defining Default Behavior | https://technet.microsoft.com/en-us/library/ee619783(v=ws.10).aspx |
| patch link again....common question still | https://support.microsoft.com/en-us/kb/2831238 |
| may be worth including the link to the United States Government Configuration Baseline (USGCB) | https://usgcb.nist.gov/usgcb_content.html |


# Easier to use headings and numbered steps

### Cached logon credential limit

Description goes here. Idefeulo foc omoemowa wahteze liv juvde puguprof. Epehuji upuga zige odfe igo sit pilamhul oto ukurecef.

 1. Open XYZ
 2. Click this
 3. Close that
 4. All done

### Increase the network retrieval timeout setting on your domain
https://technet.microsoft.com/en-us/library/cc771429(v=ws.11).aspx

### Increase the OCSP setting from the default of “50” to a higher number referenced here under Defining Default Behavior
https://technet.microsoft.com/en-us/library/ee619783(v=ws.10).aspx

### patch link again….common question still
https://support.microsoft.com/en-us/kb/2831238

### may be worth including the link to the United States Government Configuration Baseline (USGCB)
https://usgcb.nist.gov/usgcb_content.html



## Troubleshooting - Put in separate document

---
https://github.com/GSA/piv-guides/issues/49

Error Message:
The system could not log you on. The requested key container does not exist on the smart card.

Operating System:

Windows 10
Windows 2008R2, Windows 2012R2
Remote Desktop
Only native drivers (Microsoft drivers)
Repeatable (absolutely happens every time)

Cause :
There is a problem with the smart card driver. The problem can be seen when trying to connect with terminal server.
Solution:
Check using certutil -scinfo that the driver is installed on the server and on the client computer

---

https://github.com/GSA/piv-guides/issues/21

