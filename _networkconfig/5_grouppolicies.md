---
layout: page_collection
title: Group Policies
collection: networkconfig
permalink: networkconfig/grouppolicies/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Moderate</em>
</div>
</div>

The US Government publishes the [United States Government Configuration Baseline (USGCB)](http://usgcb.nist.gov/usgcb_content.html) for use by Executive Branch agencies to promote uniform configurations for [commonly used operating systems](https://cio.gov/cio-council-streamlines-configuration-baseline-process/).  The USGCB configuration guidelines for specific operating systems include references to some configurations related to smartcard (PIV) logon and should be referenced first.  

The information on this page is to answer common questions and identify the most commonly used configuration options.  For a full reference of options for each operating system, please refer to configurations guides published online.

### Machine Based Enforcement versus User Based Enforcement


Machine Based Enforcement (MBE)

User Based Enforcement (UBE)

**scforceoption** directs client Windows computers to enforce PIV logon for users. It is important to understand the ramifications of executing this step.

When you select the Smart Card is required for interactive logon check box in the Active Directory (AD) user account properties, Windows automatically resets the user password to a random complex password. In addition, Windows adds the SMARTCARD_REQUIRED flag to the UserAccountControl user account attribute and sets the DONT_EXPIRE_PASSWORD flag on the user account. The latter ensures that the user's password never expires after the Smart Card is required for interactive logon option is selected.

When a user logs on to Windows either locally or remotely using a Remote Desktop session, the Windows client automatically checks for the presence of the SMARTCARD_REQUIRED flag. If the Smart Card is required for interactive logon option is set for the user, Windows rejects the logon attempt if it's not made with smart card credentials.

Again, upon activation of scforceoption, users will **no longer know the password** to their account and will be **required** to use their PIV for authentication. Care should be used if enabling this option.



### Configure group policies for PIV Authentication
Group policy objects are used to manage configuration settings across Microsoft operating systems for workstations and servers joined to your network. Using group policy objects to manage all your configurations settings for PIV (smartcard logon) is not required; however, using group policy objects will provide a more streamlined process for efficiently applying configurations.




This task describes 2 common configurations related to domain Group Policy Objects (GPO).

|  scforceoption  |  This security policy setting requires users to log on to a computer by using a smart card.  |  Enabled / Disabled  |

**scforceoption** directs client Windows computers to enforce PIV logon for users. It is important to understand the ramifications of executing this step.

When you select the Smart Card is required for interactive logon check box in the Active Directory (AD) user account properties, Windows automatically resets the user password to a random complex password. In addition, Windows adds the SMARTCARD_REQUIRED flag to the UserAccountControl user account attribute and sets the DONT_EXPIRE_PASSWORD flag on the user account. The latter ensures that the user's password never expires after the Smart Card is required for interactive logon option is selected.

When a user logs on to Windows either locally or remotely using a Remote Desktop session, the Windows client automatically checks for the presence of the SMARTCARD_REQUIRED flag. If the Smart Card is required for interactive logon option is set for the user, Windows rejects the logon attempt if it's not made with smart card credentials.

Again, upon activation of scforceoption, users will **no longer know the password** to their account and will be **required** to use their PIV for authentication. Care should be used if enabling this option.

To enable or disable either of these policies:

1.  Open the Group Policy Management Console
1.  In the GPMC console tree, double-click Group Policy Objects in the forest and domain containing the GPO that you want to edit.
1.  Right-click the GPO, and then click Edit.
1.  In the console tree, edit the settings as appropriate.
