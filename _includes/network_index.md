<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Moderate</em>
</div>
</div>

## Introduction to Network Authentication Guide

The Network Authentication guides are for configuring your Windows _network domain_ for smartcard logon using PIV credentials.  

There are many useful pages and technical articles available online which include details on configurations and using generic smartcards.  The information presented here is for common questions and configurations **specific** to the US Federal Government, **PIV** smartcards, and US Federal civilian agency certificate authorities.

There are five configuration categories to step through with your colleagues.  We recommend working with your Network Engineers, Domain Admins, Account Management, and Information Security colleagues to review the information, perform the configurations, and troubleshoot any issues together.  

1. [Checking Ports and Protocols](../networkconfig/ports/)
2. [Domain Controller certificates](../networkconfig/domaincontrollers/)
3. [Addition of US Federal Certificate chains to the Trusted Root Certificate Authorities](../networkconfig/trustedroots/)
4. [Associating PIV credentials to the network domain user accounts](../networkconfig/accounts/)
5. [Configuring group policies for PIV (smartcard) logon](../networkconfig/grouppolicies/)

#### Assumptions
*  Users have PIV cards and PIV card readers
*  You're using Microsoft Active Directory to manage your Windows network
*  Domain Controllers are Microsoft 2008 R2 or 2012
*  User workstations joined to the network are Windows 7, Windows 8 or Windows 10
   * There are options for workstations that are Mac OS based and joined to a Windows network - to be covered in addendums to this guide
