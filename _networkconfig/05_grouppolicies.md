---
layout: default
title: Group Policies and Enforcement
collection: networkconfig
permalink: networkconfig/grouppolicies/
---

The US Government publishes the [United States Government Configuration Baseline (USGCB)](http://usgcb.nist.gov/usgcb_content.html){:target="_blank"}{:rel="noopener noreferrer"} for use by Executive Branch agencies to promote uniform configurations for [commonly used operating systems](https://cio.gov/cio-council-streamlines-configuration-baseline-process/){:target="_blank"}{:rel="noopener noreferrer"}.  The USGCB configuration guidelines for specific operating systems include references to some configurations related to smartcard (PIV) logon and should be referenced first.

The information on this page is to answer questions and identify the most commonly used configuration options.  For a full reference of options for each operating system, please refer to configurations guides published by other sources online.

* [Machine Based Enforcement versus User Based Enforcement](#machine-based-enforcement-versus-user-based-enforcement)
* [Defining the policies for Machine Based Enforcement or User Based Enforcement](#defining-the-policies-for-machine-based-enforcement-or-user-based-enforcement)

## Machine Based Enforcement versus User Based Enforcement

There are two options for requiring users to use PIV credentials to authenticate to the network domain:

* Machine Based Enforcement (MBE)
* User Based Enforcement (UBE)

These options are controlled by group policy applied to either Machine or User objects in your network domain. There is planning required to move to full User Based Enforcement and agencies are often using a combination of both Machine and User enforcement in their deployments.

{% include alert-warning.html heading = "User Based Enforcement" content="The user's password will no longer be known by the user.  Look for agency internal applications that are still using Username and Password and performing Form Based Authentication against the network directories. Fix these using Kerberos, SAML or direct x509 authentication." %}

Impacts and considerations are identified to help you plan and execute according to your agency network and user needs.

| Type | Impacts | Considerations |
| ----- | -------| -------|
| Machine Based Enforcement | The user is required to use their PIV credential to authenticate to each device where the policy is applied. | The user password is maintained. |
| User Based Enforcement | The password stored for the user is removed, and changed to a long hash value unknown to the user.  Your users no longer have passwords for the network. | Any applications which were implemented to prompt your users for a username and password and which are using your network domain directories will no longer be accessible. |

Your applications impacted by User Based Enforcement are designed or deployed using: a) Form Based or Basic Authentication, or 2) LDAP simple binds.  The user will be presented with the application form to enter a username and password and the user will no longer have the password.

You want to analyze your applications and identify which are configured to use your users' network domain passwords.  There are methods to fix the applications by enabling Kerberos, SPNEGO (web applications), direct x509 authentication (client certificate authentication), or the SAML and Open ID Connect (OIDC) protocols.  These topics will be covered in the Applications section of the guides which are in-development and we invite *all* to contribute to!

## Defining the policies for Machine Based Enforcement or User Based Enforcement
The setting to enforce PIV logon is controlled by **scforceoption** in your network domain user and workstation policies.

- Machine Based Enforcement is when you apply the **scforceoption** to a workstation or server object in your network domain.
- User Based Enforcement is when you apply the **scforceoption** to a user in your network domain.

This is the only difference when implementing the policy: which objects in your domain you apply the policy to.

You can set the policy option on a single user by checking the _Smart Card is required for interactive logon_ check box in the user account properties.  You can also apply this setting using group policy objects. When the **scforceoption** setting is applied, the SMARTCARD_REQUIRED flag is added to the UserAccountControl (UAC) and the DONT_EXPIRE_PASSWORD attribute is set to true.
