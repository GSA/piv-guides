---
layout: default
title: Enabling Smart Card for Mac OS (Sierra)
permalink: /apple/piv-sierra
collection: apple
---

_This document applies to Sierra OS only. It is not meant for Mac OS versions earlier than 10.12.3._

System Requirements
* Mac iMac or MacBook that is from 2010 or newer
* 4 GB Ram, 8 GB Ram recommended
* Core 2 Quad processor minimum, i5/i7 processor recommended
* Smart Card Reader SCR3310 (Puck style) or SCR 3310A (Foldable)


ENABLING THE SMART CARD

Turn on Smart Card Services

1. Create a Managed Mobile profile for the user, and have them set an account password.
2. Open a Terminal window, and enter the following command with elevated privileges:
	sudo security authorizationdb smartcard enable
Smart Card services should now be enabled for the system. To check use the following command:
	sudo security authorizationdb smartcard status
3. Now you are ready to pair the user’s smart card with the account.


Pair the User’s Smart Card to their Account

1. Make sure the smart card reader is plugged into a USB port.
2. A dialog box should pop up when you insert the user’s smart card.
3. Select the certificate for PIV Authentication in the drop-down menu.
4. The system will prompt for an elevated user to authorize the pairing of the PIV Certificate to the user’s account.
5. The process should be complete as soon as you click "Pair". The next time they login, the user will be prompted for their PIN on next login, and they system will replace the current keychain password.



Resources

Listed below is the working manual for the Security Authorizationdb terminal command function:
A full manual for the Security command is at:https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/security.1.html

Implementation Plan for User Migration

Smart Card pairing should occur on first login for the user, therefore this process will most likely have to occur as part of the post-imaging process, during an initial setup session with the user.

The built-in mechanisms that are in place for smart card enforcement for Yosemite OS are not compatible with the new Secure Integrity Protection protocols implemented in Sierra OS, so a clean install followed by a manual transfer of user home folder data is recommended at this time.

Known Risks / Issues

Risk 1

Methods to temporarily un-enforce and re-enforce a PIV enabled user will not be addressed in this version of the playbook.
When you implement Smart Card enforcement for a user, the system changes the way passwords are handled in the Sierra OS keychain.
Sierra changes the storage location of keychain passwords in the Secure Integrity Protection (SIP) area of the operating system, which makes it impossible to assign a user a randomized temporary password that can be replaced by a user’s PIV card pin when you re-enable enforcement. Therefore, you must either allow a known password to be used during an un-enforced period, or you must find a way to conceal the user password during the period of temporary un-enforcement, such that the user is the sole person in possession of the credentials. JSS version 9.98 may resolve this, but this is not confirmed.

Risk 2

The Enterprise Connect PKI tool is still in its final beta stages, and is subject to change. 
Sierra currently cannot read digital signing and encryption certificates from the PIV card, and pass them to Outlook 365 to sign emails. Agencies are working with the Apple Development team to address this. If your Agency uses Outlook 365, we recommend that you descope mail signing from your initial Sierra PIV requirements.


Enterprise Connect PKI

Enterprise Connect enables Mac users to use Kerberos authentication and access mapped network drives. More information is available at [https://www.jamf.com/jamf-nation/discussions/17757/about-enterprise-connect](https://www.jamf.com/jamf-nation/discussions/17757/about-enterprise-connect). To use it, you can install the Beta 3 package located in the Sierra/Beta Software folder on the Apple$ Share.
Once it is installed, it will ask you for your smart card pin for sign in:
Network Share drives that have been added to Enterprise Connect will automatically mount after login.

You can [contribute]({{ site.baseurl }}/contribute/) to this effort or open an [Issue]({{site.repo_url}}/issues) to discuss a need you may have for a guide.
