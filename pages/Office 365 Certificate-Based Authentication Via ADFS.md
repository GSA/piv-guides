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

  
If user account has a non-routable domain suffix then add alternate suffix if necessary in AD Domains and Trusts for alternate UPN
*Recommendation to have an OU filter plan before synchronizing to the cloud. In this document we have created an OU named O365 above using PowerShell for easy OU filtering and sync to the cloud. Then we move users into O365 OU for clean synchronization to the cloud.
#####AD Certificate Name Mapping Description:
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

Group Policy setup
Edit the group policy named ADFS_GPO 
Disable third party roots
•   Navigate to the computer configuration>policies>windows setting>security setting>public key policies
•   Open the Path Validation setting object 
•   Check the “Define these settings” box
•   Click on the “only Enterprise root CAs” radio button
•   Confirm the policy is active
Set SendTrustedIssuerList in registry
•   Navigate to the computer configuration>Preferences>Windows Setting>Registry
•   Right click and select New>Registry Item
•   Action Update
•   Hive:  HKLM
•   Path:  SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL
•   Value Name:  SendTrustedIssuerList
•   Value type:  REG_DWORD
•    Value Data: (0) Hex

Directory preparations

If user account has a non-routable domain suffix then add alternate suffix if necessary in AD Domains and Trusts for alternate UPN
*Recommendation to have an OU filter plan before synchronizing to the cloud. In this document we have created an OU named O365 above using PowerShell for easy OU filtering and sync to the cloud. Then we move users into O365 OU for clean synchronization to the cloud.

Install ADFS server
The system where ADFS is installed must be domain joined
The internal name for the ADFS server must not match the external name on the certificate:
•   Adfs.foobar.local and adfs.foobar.com
•   Fs.foobar.com and adfs.foobar.com
Plan the number of ADFS servers according to https://msdn.microsoft.com/en-us/library/azure/dn151324.aspx
Additional downloads in order 
Download and install on system running ADFS:
1.  Microsoft Online Services Sign-In Assistant for IT Professionals RTW: Restart required
https://www.microsoft.com/en-us/download/details.aspx?id=41950
2.  Install Windows Azure Active Directory Module for Windows PowerShell for running script
http://go.microsoft.com/fwlink/p/?linkid=236297
Federation to Office365: Run  bulleted commands on ADFS system in “Windows Azure Active Directory Module for Windows PowerShell” 
Azure Active Directory PowerShell
•   $credential = Get-Credential
•   Import-Module MsOnline
•   Connect-MsolService -Credential $credential
•   New-MSOLFederatedDomain –DomainName .foobar.com  (Note**this will add the domain to Office365, if domain already exist in Office 365 then use PowerShell cmdlet Update-MSOLFederatedDomain instead of New-MSOLFederatedDomain )
•   Get-msoldomain  (should show the domain is Federated with Office 365)

Open ADFS Management and set authentication method to only certificate authentication under Authentication Policies 

Download and install on member server in the domain:  

For small organizations or small directories run Azure AD Connect on the domain controller to configure and start synchronization from on premise AD to the O365 cloud.
•   Azure AD Connect for synchronization 
http://go.microsoft.com/fwlink/?LinkId=615771

Firewall rules:
Allow Inbound to ADFS TCP 443 & 49443
Move all ADFS servers into ADFS OU in Active Directory Users and Computers

Run gpupdate /force on ADFS server(s)g from elevated command prompt.
