---
layout: page
title: How do I enable Microsoft AD for PIV Logon?
permalink: /3_ad/
---
<script>
$(function() {
  $( "#accordion" ).accordion({
    heightStyle: "content",
    collapsible: "true"
  });
});
</script>
#### Overview

Smart Card Authentication to Active Directory requires that Smartcard workstations, Active Directory, and Active Directory domain controllers be configured properly. Active Directory must trust a certification authority to authenticate users based on certificates from that CA. Both Smartcard workstations and domain controllers must be configured with correctly configured certificates.

As with any PKI implementation, all parties must trust the Root CA to which the issuing CA chains. Both the domain controllers and the smartcard workstations trust this root.

#### Before you get started:
-  Required: Active Directory must have the third-party issuing CA in the NTAuth store to authenticate users to active directory.
-  Required: Domain controllers must be configured with a domain controller certificate to authenticate smartcard users.
-  Optional: Active Directory can be configured to distribute the third-party root CA to the trusted root CA store of all domain members using the Group Policy.

#### Complete the following steps:

<div id="accordion" markdown="1">

### 1. Add the root CA to the trusted roots in an Active Directory Group Policy object.
<div markdown="1">
To configure Group Policy in the Windows 2000 domain to distribute the third-party CA to the trusted root store of all domain computers:

1.  Click Start, point to Programs, point to Administrative Tools, and then click **Active Directory Users and Computers**.
1.  In the left pane, locate the domain in which the policy you want to edit is applied.
1.  Right-click the domain, and then click **Properties**.
1.  Click the **Group Policy** tab.
1.  Click the **Default Domain Policy Group Policy** object, and then click **Edit**. A new window opens.
1.  In the left pane, expand the following items:

    -  Computer Configuration
    -  Windows Settings
    -  Security Settings
    -  Public Key Policy

1.  Right-click Trusted Root Certification Authorities.
1.  Select All Tasks, and then click Import.
1.  Follow the instructions in the wizard to import the certificate.
1.  Click OK.
1.  Close the Group Policy window.
</div>

### 2. Add the third-party issuing the CA to the NTAuth store in Active Directory.
<div markdown="1">
The smart card logon certificate must be issued from a CA that is in the NTAuth store. By default, Microsoft Enterprise CAs are added to the NTAuth store.

-  If the CA that issued the smart card logon certificate or the domain controller certificates is not properly posted in the NTAuth store, the smart card logon process does not work. The corresponding answer is "Unable to verify the credentials".
-  The NTAuth store is located in the Configuration container for the forest. For example, a sample location is as follows:  

        LDAP://server1.name.com/CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=name,DC=com

-  By default, this store is created when you install a Microsoft Enterprise CA. The object can also be created manually by using ADSIedit.msc in the Windows 2000 Support tools or by using LDIFDE. For more information, click the following article number to view the article in the Microsoft Knowledge Base:  

[295663](https://support.microsoft.com/en-us/kb/295663) How to import third-party certification authority (CA) certificates into the Enterprise NTAuth store

-  The relevant attribute is cACertificate, which is an octet String, multiple-valued list of ASN-encoded certificates.  
After you put the third-party CA in the NTAuth store, Domain-based Group Policy places a registry key (a thumbprint of the certificate) in the following location on all computers in the domain:  

        HKEY_LOCAL_MACHINE\Software\Microsoft\EnterpriseCertificates\NTAuth\Certificates

This is refreshed every eight hours on workstations (the typical Group Policy pulse interval).
</div>

### 3. Request and install a domain controller certificate.
<div markdown="1">
Request and install a domain controller certificate on the domain controller(s). Each domain controller that is going to authenticate smartcard users must have a domain controller certificate.  

If you install a Microsoft Enterprise CA in an Active Directory forest, all domain controllers automatically enroll for a domain controller certificate. For more information about requirements for domain controller certificates from a third-party CA, click the following article number to view the article in the Microsoft Knowledge Base:  

[291010](https://support.microsoft.com/en-us/kb/291010) Requirements for domain controller certificates from a third-party CA
</div>

### 4. Correlate PIV card Certificates with active directory accounts.
<div markdown="1">
Placeholder.
</div>
</div>

#### Troubleshooting

  Placeholder.

#### References

  This guide was derived from a [Microsoft Knowledgebase Article](https://support.microsoft.com/en-us/kb/281245)

#### Related Playbooks

-  [How do I enable Microsoft AD for Admin access?]({{ site.baseurl }}/4_adadmin/)
-  [How do I enable a domain to assert assurance in AD?]({{ site.baseurl }}/5_domainassert/)
-  [How do I validate trust stores on a Windows platform?]({{ site.baseurl }}/9_trustwindows/)
