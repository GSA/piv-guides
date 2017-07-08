---
layout: default
title: Set a script to run on the target clients to distribute CA certificates to NSS
collection: userconfig
permalink: userconfig/nss/
---

### Pre-requisits

1. Install NSS certutil on client machines: https://github.com/christian-korneck/firefox_add-certs/releases
2. Client machines are configured for PIV login.

### Set a Script to Run on the Target clients to Distribute CA Certificates to NSS

1. In domain controller, Copy the CA certificate you wish to distribute in to the directory so that it is accessible via \\fileserver\scripts$\comp_resources\nss\publicca.cer
2. Open gpmc.msc and create and edit a GPO on the test OU you are targetting.
3. Navigate to User Configuration\Policies\Windows Settings\Scripts\

4. Double-click on Logon.

5. Click Show files.

6. Right-click and create a new BAT file named firefox_ca_add.bat that contains the following:

            if not exist "%appdata%\mozilla\firefox\profiles" goto:eof
            set profiledir=%appdata%\mozilla\firefox\profiles
            dir "%profiledir%" /a:d /b > "%temp%\temppath.txt"
            if not exist "c:\windows\syswow64\nss" goto WIN32
            for /f "tokens=*" %%i in (%temp%\temppath.txt) do (
            cd /d "%profiledir%\%%i"
            copy cert8.db cert8.db.orig /y
            "c:\windows\syswow64\nss\certutil.exe" -A -n "Our Organization's Root CA" -i "c:\windows\system32\nss\publicca.cer" -t "TCu,TCu,TCu" -d .
            )
            goto FINALLY
            :WIN32
            if not exist "c:\windows\system32\nss" goto FINALLY
            for /f "tokens=*" %%i in (%temp%\temppath.txt) do (
            cd /d "%profiledir%\%%i"
            copy cert8.db cert8.db.orig /y
            "c:\windows\system32\nss\certutil.exe" -A -n "Our Organization's Root CA" -i "c:\windows\system32\nss\publicca.cer" -t "TCu,TCu,TCu" -d .
            )
            goto FINALLY
            :FINALLY
            del /f /q "%temp%\temppath.txt"

7. Back in the Logon Properties window, click Add, then Browse to the firefox_ca_add.bat file, double-click.

8. Double-click on Logoff, and perform relatively the same, except navigating in the directory tree to the script you created within the ./Startup/ directory.

9. Perform a `gpupdate /force` on the test client, and restart the machine (okay fine, you can also just run the BAT file).

10. Open firefox and navigate to Tools> Options> Advanced> Encryption tab> Certificates pane> View Certificates button and scroll down until you find “Our Organization’s Root CA”

Removing an issued certificate:

```

cd /d "%profiledir%\%%i"
"c:\windows\syswow64\nss\certutil.exe" -D -n "Our Organization's Root CA" -d 
```
