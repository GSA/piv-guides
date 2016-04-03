---
layout: page_collection
title: Domain Controllers
collection: networkconfig
permalink: networkconfig/domaincontrollers/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Difficulty: Moderate</em>
</div>
</div>

### Why Domain Controller Certificates?
To use smartcards and / or PIV credentials for network authentication, all the Domain Controllers need to have Domain Controller Authentication certificates.  
  
>  Just like your users are using certificates, the domain controllers are also authenticating as _devices_ using certificates.  The users are authenticated and the domain controllers are authenticated, and each works together in the challenge response to create secure connections.  It's required for the protocols, and if you want to learn more - search for information on _PKINIT_ protocols.  

### What do the Domain Controller Certificates need to include?
The certificate for each domain controller must meet the following specific format requirements:

1.  The certificate **Key Usage** extension must contain:

            Digital Signature, Key Encipherment

1. The certificate **Enhanced Key Usage** extension must contain:

            Client Authentication (1.3.6.1.5.5.7.3.2)
            Server Authentication (1.3.6.1.5.5.7.3.1)

1. The certificate **Subject Alternative Name** extension must contain the Domain Name System (DNS) qualifier and name.  This must be the fully qualified domain controller name.  For example:  

            DNS Name=controller1.intranet.agency.gov

1. The certificate **Subject Alternative Name** must also contain the global unique identifier (GUID) of the domain controller object in the domain.

  *  To determine the Domain Controller GUID, start Ldp.exe and locate the domain-naming context. Double-click the name of the domain controller that you want to view. The list of attributes for that object contains "Object GUID" followed by a long number. The number is the GUID for that object. For example:

                Other Name: 1.3.6.1.4.1.311.25.1 = ac 4b 29 06 bb d6 5d 4f e3 9c 4c ab c3 6a 55 d9


1.  The domain controller certificate must be installed in the domain controller's local computer's certificate store.

### How do I issue Domain Controller Certificates?
This is a challenging question to answer.  US Federal Civilian agencies currently have a variety of policies on whether you should use a Domain Controller certificate issued from your agency's standalone or local Certificate Authority, or whether the certificate must be issued from a Certificate Authority managed and certified under the Federal Public Key Infrastructure (FPKI) Policy Authority  To help answer this question, we're compiling a list of known policies and options available to all US Federal Civilian agencies here (TODO: INSERT LINK TO A REPO or MD page).

The best option for now is to talk with your Chief Information Security Officer (CISO) or Information Security office for a definitive answer and direction.    
### Common Commands and Examples

Getting the GUID commands

```  
body { font-size: 12pt;
      background-color: #fff}

```

certutil -dcinfo
/ command to query domain controllers for certs and status
extensions for domain controller certs
