---
layout: page_collection
title: Group Policies
collection: networkconfig
permalink: networkconfig/grouppolicies/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Difficulty: Moderate</em>
</div>
</div>


### Configure group policies for PIV Authentication

This task describes 2 common configurations related to domain Group Policy Objects (GPO).

|  scforceoption  |  This security policy setting requires users to log on to a computer by using a smart card.  |  Enabled / Disabled  |
|  scremoveoption  |  This setting determines what happens when the smart card for a logged-on user is removed from the smart card reader.  |  No Action / Lock Workstation / Force Logoff / Disconnect if a Remote Desktop Services session  |

**scforceoption** directs client Windows computers to enforce PIV logon for users. It is important to understand the ramifications of executing this step.

When you select the Smart Card is required for interactive logon check box in the Active Directory (AD) user account properties, Windows automatically resets the user password to a random complex password. In addition, Windows adds the SMARTCARD_REQUIRED flag to the UserAccountControl user account attribute and sets the DONT_EXPIRE_PASSWORD flag on the user account. The latter ensures that the user's password never expires after the Smart Card is required for interactive logon option is selected.

When a user logs on to Windows either locally or remotely using a Remote Desktop session, the Windows client automatically checks for the presence of the SMARTCARD_REQUIRED flag. If the Smart Card is required for interactive logon option is set for the user, Windows rejects the logon attempt if it's not made with smart card credentials.

Again, upon activation of scforceoption, users will **no longer know the password** to their account and will be **required** to use their PIV for authentication. Care should be used if enabling this option.

To enable or disable either of these policies:

1.  Open the Group Policy Management Console
1.  In the GPMC console tree, double-click Group Policy Objects in the forest and domain containing the GPO that you want to edit.
1.  Right-click the GPO, and then click Edit.
1.  In the console tree, edit the settings as appropriate.


