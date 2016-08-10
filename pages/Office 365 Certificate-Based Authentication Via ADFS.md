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

Note: This playbook does not cover setting up an ADFS proxy server.

1. Have a public facing domain with ability to manage entries.
1. Have an (A) record for the ADFS server.  Note that the name must match the certificate.
1. Acquire a certificate from a public Certificate authority for public facing ADFS.
1. Install Active Directory.
1. Install ADFS (not recommended to be loaded on the AD).
1. Create a group managed service account.
1. Set the KDS root key.
1. Download and install on system running ADFS:
  * [Windows Azure Active Directory Module](http://go.microsoft.com/fwlink/p/?linkid=236297) for Windows PowerShell for running scripts.
  * [Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) for synchronization.
  * [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=28177).

1. Run as administrator, the script _Windows Azure Active Directory Module for Windows PowerShell_
on the ADFS system.
1. Start _Windows Powershell_ and enter the following commands:

 ```powershell
$credential = Get-Credential 
Import-Module MsOnline
Connect-MsolService -Credential $credential
$exchangeSession = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "https://outlook.office365.com/powershell-liveid/" -Credential $credential -Authentication "Basic" -AllowRedirection
Import-PSSession $exchangeSession -DisableNameChecking
Set-ExecutionPolicy RemoteSigned
New-MSOLFederatedDomain -DomainName machine.yourdomain.gov
Get-msoldomain
<# Note: replace machine.yourdomain.gov with your ADFS server name. #>
```  

Add the following firewall rules:  

```
    Inbound to ADFS 443  
    Inbound to ADFS 49443  
```

Run _Azure AD Connect_ to configure and start synchronization from on premise AD to the O365 cloud.

Note: It is recommended that you create a dedicated OU for synchronization, and not the entire Directory: (ex. O365 OU)

####How this Approach was Derived
Dr. Trevor Freeman, CertiPath, Inc. provided this report:

#####Scenario
Organizations who have issued X.509 authentication certificates want to use them for authentication to authenticate to Office 365. The scenario is supported according to the Office 365 documentation by using Office 365 Federated Identity and an on premise identity provider such as ADFS.
https://blogs.office.com/2014/05/13/choosing-a-sign-in-model-for-office-365/
See Scenario 5.

#####Test Environment
1. We configured a single domain test forest in our lab using Windows 2012 R2 as the base platform and with an ADFS role on a member server.  
1. We configured accounts in the test forest with subject DN name mapping matching our PIV-Auth certificates. There was no UPN name in the SAN of the PIV-Auth certificate.  
1. We set up a test IIS web page using client certificate authentication with AD certificate mapping in the on premise domain to verify the account name mapping configuration.  
1. We connected to the IIS test page and verified the user was authenticated appropriately.  
1. The ADFS server was configured to be publicly accessible on the internet.  
1. We configured the ADFS server to use a public namespace under our control (certipath.com).  
1. We installed a certificate from a public CA on the ADFS server (fs.certipath.com)  
1. We federated with Office 365.  
1. We set up Azure AD Connect to sync the accounts from our on premise forest to O365.  
1. We chose the _Federation with ADFS_ under user sign in option page.  

#####Expected Behavior
1. User would connect to the Office 365 login portal (portal.office.com).  
1. User enters their UPN (user@certapath.com) on the office portal.  
1. User is redirected from the office portal to on premise ADFS server.  
1. User is prompted to select a certificate by their browser and their PIV-Auth certificate is one of the options.  
1. User selects the PIV-Auth certificate, enter the PIN.  
1. User is redirected back to O365 and they see their options as an authenticated user, i.e. Outlook, SharePoint, etc.  

#####Actual Behavior
1. User visited the Office Portal (portal.office.com).  
1. User entered their UPN (user@certipath.com).  
1. User was redirected to the certapath.com ADFS server but there was no certificate selection popup from the IE, Firefox or Chrome.   
1. User received an authentication error from the ADFS web page.  

#####Analysis
1. We used Wireshark on the ADFS server to capture the connection of the user to the ADFS server.  
1. We confirmed the user was connecting to the correct end point.  
1. The client was sending the TLS client hello.  
1. The server responded appropriately and was sending a client certificate request option for authentication.  

```text
Frame 2: 4889 bytes on wire (39112 bits), 4889 bytes captured (39112 bits) on interface 0.  
Ethernet II, Src: Vmware_9a:0c:c2 (00:50:56:9a:0c:c2), Dst: Sonicwal_b2:14:67 (c0:ea:e4:b2:14:67)
Internet Protocol Version 4, Src: 10.0.43.171, Dst: 24.17.210.106
Transmission Control Protocol, Src Port: 49443 (49443), Dst Port: 54416 (54416), Seq: 1, Ack: 208, Len: 4835
Secure Sockets Layer
    TLSv1.2 Record Layer: Handshake Protocol: Multiple Handshake Messages
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 4830
        Handshake Protocol: Server Hello
        Handshake Protocol: Certificate
        Handshake Protocol: Server Key Exchange
        Handshake Protocol: Certificate Request
        Handshake Protocol: Server Hello Done
```
The client was not responding with a certificate in the handshake.  

```text
Handshake Protocol: Certificate
    Handshake Type: Certificate (11)
    Length: 3
    Certificates Length: 0
```
The ADFS server returned the authentication error after the handshake completed. 
When we looked further at the Certificate Request packet, we discovered that the DN field in the certificate request packet had a single DN. The DN matched the test certificate used to initially configure ADFS transport for on premise testing. 
```text
Distinguished Names (44 bytes)
    Distinguished Name Length: 42
    Distinguished Name: (id-at-commonName=TMSCA,id-at-organizationName=Trust Manager)
        RDNSequence item: 1 item (id-at-organizationName=Trust Manager)
        RDNSequence item: 1 item (id-at-commonName=TMSCA)
```
The DN is used by client to filter the set of potential candidate certificates for client authentication. None of the PIV certificates had CA names in their trust chain which matched the test CA name so we hypothesized that this was causing the browser to conclude there were zero possible candidates and so complete the handshake without a client certificate.
#####Testing the Hypothesis
1. We tested this hypothesis by issuing client authentication certificates without UPN names from the test CA so as to match the DN being used by the ADFS server.
1. We mapped the accounts in AD to the names in the new certificates.  
1. We went to portal.office.com.  
1. We entered the UPN for the test forest user@certipath.com.  
1. We were promoted by IE to select a certificate. This was the new test certificate. The PIV certificate was not in the list.  
1. We were redirected back to O365 without error.  
1. We confirmed in the logs on the ADFS server we were authenticated as the correct principal.   
