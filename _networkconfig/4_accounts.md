---
layout: page_collection
title: Accounts
collection: networkconfig
permalink: networkconfig/accounts/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Difficulty: Moderate</em>
</div>
</div>

## Two methods

* User Principal Name (UPN)
* altSecurityIdentities

A portion of agencies may be using the User Principal Name (UPN) mapping to associate a PIV certificate to a user account.  In the UPN model:

* Each PIV credential can only be associated with ONE account
* The User Principal Name value from the Subject Alternate Name in the PIV authentication certificate is required to be populated 
* There is less flexibility for managing privileged accounts

You will find more flexibility in using the altSecurityIdentities mapping options which were made available in 2008 in specific network platforms.  In the altSecurityIdentities model:

* Each PIV credential can be associated with MORE THAN ONE account
* Six options from the certificate can be used to map to each account
* There is flexibility for managing privileged accounts
* Users are presented a User Name Hint to help choose which account to authenticate to

### Associating PIV Credentials to the Active Directory User Accounts using altSecurityIdentities

To help you configure and enable User Name Hints and altSecurityIdentities, there is documentation available freely online from sources.  The information provided here is to help you with PIV and US Federal government common challenges.

1. It is NOT required that you get updated PIV credentials and certificates without a UPN value populated
  * This is a common misconception
  * If your PIV credentials do have a UPN value in the Subject Alternative Name, this method will still work for your agency.  

1. Disable UPN Mapping
  * This is a registry setting and you must disable this setting on all domain controllers
  * [Link to the registry setting](https://technet.microsoft.com/en-us/library/ff520074(WS.10).aspx)
  
1. Map the user certificates to the altSecurityIdentities attribute for each account
  * You have six options from the certificates to use
  * A common challenge 

  
  
| Options       | Tag     | Example | Considerations |
| ------------- |:-------------:| -----:|-----:|
| Subject     | X509:\<S> | X509:\<S>C=US,O=U.S. Government,OU=General Services Administration,CN=LACHELLE LEVAN OID.0.9.2342.19200300.100.1.1=47001003151020 |   | 
| Issuer and Subject     | X509:\<I>\<S>  | X509:\<I>C=US,O=Entrust,OU=Certification Authorities,OU=Entrust Managed Services SSP CA\<S>C=US,O=U.S. Government,OU=General Services Administration,CN=LACHELLE LEVAN OID.0.9.2342.19200300.100.1.1=47001003151020 |   |
| Issuer and Serial Number | X509:\<I>\<SR> |    $1 |  
| SHA1 hash of public key| X509:\<SHA1-PUKEY> |    $1 |  
| RFC822 name | X509:\<RFC822>      |    $1 | 
| UPN     | X509:\<S> | $1600 | 

You can consider the pros and cons of each method for your agency.  The most common pros and cons are based on whether the attributes would need to be updated if a user receives an updated PIV credential.

| altSecurityIdentities       | Pro          | Con  |
| ------------- |:-------------:| -----:|
| Subject     |  | $1600 |
| Issuer and Subject     | X509:<I><S>      |   $12 |
| Issuer and Serial Number | X509:<I><SR>      |    $1 |  
| SHA1 hash of public key| X509:<SHA1-PUKEY>      |    $1 |  
| RFC822 name | X509:<SHA1-PUKEY>      |    $1 | 
| UPN     | X509:<S> | $1600 | 


There are helpful guides and links at the bottom of this page with public information on altSecurityIdentities and User Name Hints.  



To configure Active Directory one-to-one mapping using altSecurityIdentities attributes:

1.	Click Start, click Programs, click Administrative Tools, and click Active Directory Users and Computers.
2.	Expand the domain name node containing the user(s) to manage and click the Users folder. In the right pane, right-click the account to map and click Name Mappings.
3.	On the X.509 Certificates tab, click the Add button. Select the user certificate from the .cer file that should be mapped to the account.
4.	The Use Issuer for alternate security identity will be selected and appear gray by default because you need to use this for both one-to-one mapping and many-to-one mapping. 
Select the Use Subject for alternate security identity option to do one-to-one mapping. By unchecking this option, you will be doing many-to-one mapping. Click OK.
5.	Go to the section, testing the Mapping, to verify that this works.


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



#### References

Elements of this guide were derived from a [Microsoft Knowledgebase Article](https://support.microsoft.com/en-us/kb/281245)
