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

### Domain Controller certificates

Include:
Getting the GUID commands
certutil / command to query domain controllers for certs and status
extensions for domain controller certs
where to get domain controller certs and options


Work with the Federal Public Key Infrastructure management team to request a domain controller certificate for your domain controller(s). Each domain controller that is going to authenticate smartcard users must have a domain controller certificate.  

The certificate for each domain controller must meet the following specific format requirements:

*  The certificate must have a CRL distribution-point extension that points to a valid certificate revocation list (CRL).
    *  Optionally, the certificate Subject section should contain the directory path of the server object (the distinguished name), for example:  
            CN=controller1.agency.gov OU=Domain Controllers DC=agency DC=gov  
    *  The certificate Key Usage section must contain:  
            Digital Signature, Key Encipherment

    *  Optionally, the certificate Basic Constraints section should contain:

            [Subject Type=End Entity, Path Length Constraint=None]

    *  The certificate Enhanced Key Usage section must contain:

            Client Authentication (1.3.6.1.5.5.7.3.2)
            Server Authentication (1.3.6.1.5.5.7.3.1)

    *  The certificate Subject Alternative Name section must contain the Domain Name System (DNS) name. If SMTP replication is used, the certificate Subject Alternative Name section must also contain the globally unique identifier (GUID) of the domain controller object in the directory.
        *  To determine the Domain Controller GUID, start Ldp.exe and locate the domain-naming context. Double-click the name of the domain controller that you want to view. The list of attributes for that object contains "Object GUID" followed by a long number. The number is the GUID for that object. For example:

                Other Name: 1.3.6.1.4.1.311.25.1 = ac 4b 29 06 bb d6 5d 4f e3 9c 4c ab c3 6a 55 d9 DNS Name=controller1.agency.gov


*  The domain controller certificate must be installed in the local computer's certificate store.

