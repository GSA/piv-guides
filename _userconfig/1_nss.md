---
layout: default
title: Automate the Distribution of CA Certificates into NSS
collection: userconfig
permalink: userconfig/1_nss/
---

Organizations need to be able to automate the distribution of CA certificates into NSS for their enterprise configurations. <!--Tried to make the title simpler above. Does it make sense? Need an intro sentence. Don't see anything in this write-up that addresses LaChelle's comment about "Some of the intermediate CAs in the FPKI stop the CA name at OU rather than using a CN," which was one of the Listserv issues I sent you last night.  Also, LaChelle mentioned "enterprise configurations" in her initial comment on Issue 20. Can that be added in here somewhere?-->

## Prerequisites

1. Install NSS _certutil_ on your client machines: https://github.com/christian-korneck/firefox_add-certs/releases.
2. Configure client machines for PIV login. <!--No instruction needed?-->

## Create a Script To Distribute CA Certificates to NSS

1. Using a domain controller, copy a CA certificate you wish to distribute into the NSS <!--What directory name?-->directory so that it is accessible via _\\fileserver\scripts$\comp_resources\nss\publicca.cer_. <!--This is the directory path? Where does NSS come in?-->
2. Open _gpmc.msc_. 
3. Create and edit a GPO on a test _OU_ (i.e., your target). <!--Will this process be absolutely clear to the administrator? Is this to test whether OU issue is fixed and CN is allowed?-->
4. Navigate to _User Configuration\Policies\Windows Settings\Scripts\_. 
5. Double-click on _Logon_ and then click on _Show files_.
6. Right-click <!--On what?-->and create a new BAT file named _firefox_ca_add.bat_ that contains: <!--Is the BAT file the "script" the admin "added to the "/Startup/ directory" mentioned in Step 9? Explain "/Startup/ directory.-->

            if not exist "%appdata%\mozilla\firefox\profiles" goto:eof
            set profiledir=%appdata%\mozilla\firefox\profiles
            dir "%profiledir%" /a:d /b > "%temp%\temppath.txt"
            if not exist "c:\windows\syswow64\nss" goto WIN32
            for /f "tokens=*" %%i in (%temp%\temppath.txt) do (
            cd /d "%profiledir%\%%i"
            copy cert8.db cert8.db.orig /y
            "c:\windows\syswow64\nss\certutil.exe" -A -n "Our Organization's Root CA" -i "c:\windows\system32\nss\publicca.cer" -t "TCu,TCu,TCu" -d . <!--The space before period is correct? Is period necessary?-->
            )
            goto FINALLY
            :WIN32
            if not exist "c:\windows\system32\nss" goto FINALLY
            for /f "tokens=*" %%i in (%temp%\temppath.txt) do (
            cd /d "%profiledir%\%%i"
            copy cert8.db cert8.db.orig /y
            "c:\windows\system32\nss\certutil.exe" -A -n "Our Organization's Root CA" -i "c:\windows\system32\nss\publicca.cer" -t "TCu,TCu,TCu" -d . <!--The space before period is correct? Is period necessary?-->
            )
            goto FINALLY
            :FINALLY
            del /f /q "%temp%\temppath.txt"

7. Go to the Logon Properties window and click on Add.
8. Browse to and double-click on the _firefox_ca_add.bat file_.
9. Double-click on _Logoff_ and go through basically the same steps, but navigate in the directory tree to the script you created within the _./Startup/_ directory. <!--The /Startup/ directory was never mentioned before--explain this above where it should happen.-->
10. Perform a `gpupdate /force` on the test client and restart the machine. (You can also just run the BAT file.)
11. Open Firefox and navigate to _Tools-> Options-> Advanced-> Encryption tab-> Certificates pane-> View Certificates button_. Click on the button and scroll down until you find "Our Organization’s" Root CA. <!--Are you supposed to click on the View Certificates button? and then a list comes up that you scroll through? Explain.-->
12. Remove an issued CA certificate: <!--Can't follow the logic of this ending. How does this step relate to "automated distribution of CA certificates into NSS"? Need a more clear wrap-up and tie-in to the purpose of this Playbook.-->

```

cd /d "%profiledir%\%%i"
"c:\windows\syswow64\nss\certutil.exe" -D -n "Our Organization's Root CA" -d 
```
