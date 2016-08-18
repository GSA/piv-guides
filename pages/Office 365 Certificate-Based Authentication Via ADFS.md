---
layout: page
title: Office 365 Certificate-Based Authentication Via ADFS
permalink: /Office 365 Certificate-Based Authentication Via ADFS/
---
###A Solution for Office 365 Certificate-Based Authentication Via ADFS
<!--- The code below creates a difficulty identifier on the page, which can either 
be Beginner, Moderate, or Advanced depending on the technical knowledge required to 
complete the procedure. The example below includes text that mark the document as 
'Advanced', this string can be changed as needed.-->
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; 
height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Difficulty: Advanced</em>
</div>
</div>
Note: This document does not cover ADFS proxy server scenario or Office 365 account setup.
####Prerequisites
* Have a public-facing domain with the ability to manage entries.  
* Create publicly available (A/AAAA) records for the ADFS server. The FQDN of the DNS A/AAAA record must match the DNS name in the certificate.
* Acquire from a public Certificate Authority a certificate with a DNS name which matches the DNS name you have registered in DNS (adfs.foobar.com).  

####Install Active Directory server
#####Active Directory/Domain preparations

  
If the user account has a non-routable domain suffix then add an alternate suffix if necessary in AD _Domains and Trusts_ for the alternate UPN.  

We recommend you have an OU filter plan before synchronizing to the cloud. In this document we have created an OU named O365 above using PowerShell for easy OU filtering and sync to the cloud. Then we move users into O365 OU for clean synchronization to the cloud.
#####AD Certificate Name Mapping Operation:
A user presents a certificate to ADFS as part of authentication, and ADFS looks at the name mappings in AD to determine which user account should be logged on. If the certificate has a user principal name (UPN) the UPN is used to resolve the user account in AD. If there is no UPN, then the certificate's Distinguished Name is used.  
Perform the following operations on the Domain Controller. <-

* Open MMC and add the _Certificates_ snap-in for the _Local User_, and select _Personal->Certificates_  
* Find the user ID certificate, right click _All tasks->Export_. This opens the _Certificate Export_ Wizard  
* Select _Next_ three times  
* Browse to a folder, enter a file name, and select _Finish_  
* Using Windows Explorer, navigate to the folder location of the saved certificate.  
* Open the saved certificate, click on the _Certification Path_ tab, highlight the next certificate up from the user certificate, and click _View Certificate_.  
* On that certificate select the _Details_ tab and click _Copy to File_ which opens the _Certificate Export Wizard_.  
* Complete the wizard for that certificate and each certificate above it until all of the certificates in the path have been saved.  

| | |
|---|---|
|![Example of discovered trust path](../img/trustpathexample.png)|The first Sub CA above the leaf is the _leaf issuer_.|
|![valid certificate path](../img/valideecert.png)|![Invalid certificate path](../img/invalideecert.png)|
|Valid trust path|Invalid trust path|

Note: If the user certificate does not have a valid certificate path then stop and fix the trust path before continuing. 

####AD PKI Setup on the domain controller
1. Add the user's PIV auth cert (Leaf) into name mapping for the user in O365 OU in AD
1. As Enterprise Admin, run the following from an elevated command prompt: (where _certfile_ is name of certificate file).  
```bat
    certutil -f -dspublish _certfile_.cer rootca  
    certutil -f -dspublish _certfile_.cer subca..
    certutil -f -dspublish _certfile_.cer NTAuthca  
```
As administrator, run the following PowerShell commands on the domain controller:  
```powershell
    #Create OU O365 in Active Directory Users and Computers
    New-ADOrganizationalUnit -Name O365 -Path "DC=Foobar,DC=COM"
    #Create an OU in Active Directory Users and Computers
    New-ADOrganizationalUnit -Name ADFS -Path "DC= Foobar,DC=COM"
    #Create KDS root key
    Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))
    #Create group managed service account
    New-ADServiceAccount gMSAcct01 -DNSHostName yourhost.Foobar.com
    #Create a group policy for ADFS OU and link to ADFS OU
    New-gpo -name ADFS_GPO | new-gplink -target "ou=ADFS, DC= Foobar,DC=COM"  
```

#####Group Policy setup
* Edit the group policy you just added, _ADFS_GPO_.
* Disable third party roots:  
   1. Navigate to the computer configuration>policies>windows setting>security setting>public key policies.  
   1. Open the Path Validation setting object.  
   1. Check the _Define these settings_ checkbox.  
   1. Select the _only Enterprise root CAs_ radio button
* Confirm the policy is active.  
* Set _SendTrustedIssuerList_ in registry
   1. Navigate to the computer _Configuration->Preferences->Windows Setting->Registry_  
   1. Right-click and select _New->Registry Item_  
      * Action: Update  
      * Hive:  HKLM  
      * Path:  SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL  
      * Value Name:  SendTrustedIssuerList  
      * Value type:  REG_DWORD  
      * Value Data: (0) Hex  

####Install ADFS server
#####Prerequisites:
The system where ADFS is installed must be domain-joined.
The internal name for the ADFS server _must not_ match the external name on the certificate as in these examples:
* adfs.foobar.local and adfs.foobar.com
* fs.foobar.com and adfs.foobar.com

Plan the number of ADFS servers according to the Microsoft Azure article, [Plan your AD FS deployment](https://msdn.microsoft.com/en-us/library/azure/dn151324.aspx).  
 
Download and install on the system running ADFS in the order below. :  

1. [Microsoft Online Services Sign-In Assistant for IT Professionals](https://www.microsoft.com/en-us/download/details.aspx?id=41950) (restart required).  
1. [Windows Azure Active Directory Module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297) (for running a PowerShell script).

#####Federation to Office365
Run these commands on the ADFS system using _Windows Azure Active Directory Module for Windows PowerShell_.  
```dos
Azure Active Directory PowerShell
```
```powershell
$credential = Get-Credential  
Import-Module MsOnline  
Connect-MsolService -Credential $credential  
#This will add the domain to Office365; if domain already exists in Office 365 then use PowerShell ```cmdlet Update-MSOLFederatedDomain``` instead of ```New-MSOLFederatedDomain```)
New-MSOLFederatedDomain -DomainName .foobar.com  
Get-msoldomain  (should show the domain is Federated with Office 365)
```
Open ADFS Management and set authentication method to only certificate authentication under Authentication Policies 

Download and install on member server in the domain:  

For small organizations or small directories, run [Azure AD Connect for Synchronization](http://go.microsoft.com/fwlink/?LinkId=615771) on the domain controller to configure and start synchronization from on premise AD to the O365 cloud.  

#####Firewall rules
1. Allow Inbound to ADFS TCP 443 & 49443  
1. Move all ADFS servers into ADFS OU in _Active Directory Users and Computers_  

#####Group updates
1. From an Administrator command prompt, run `gpupdate /force` on the ADFS server.