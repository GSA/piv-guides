---
layout: page_collection
title: Trust Stores
collection: networkconfig
permalink: networkconfig/trustedroots/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Difficulty: Moderate</em>
</div>
</div>


### Addition of US Federal Certificate chains to the Trusted Root Certificate Authorities

The root certificate and intermediate CA certs are required by the domain controller to establish trust between the parent CA and the end users and applications. 

This allows the domain controller to issue trusted certificates to PIV cards within the directory and confirm the validity of smart card certificates during an access attempt.

Active Directory must be configured to trust a certification authority to authenticate users based on certificates from that CA. 

Both workstations and domain controllers must be configured to trust the certificates 

This task will configure Active Directory to trust the Certification Authority chain that signed the users' authentication certificates. To configure Active Directory with the signing CA Certificate chain:

1.	On your Active Directory Domain Controller server, select **Active Directory Users and Computers**
2.	In the **Management Console**, right click the **Domain** and click **Properties**
3.	Once you're on the **Group Policy Tab**, click **Open** to open the **Group Policy Management Console plug-in**
4.	Right Click **Default Domain Policy** and click **Edit**
5.	Expand the **Computer Configuration** section and open **Windows Settings > Security Settings > Public Key**
6.	Right click **Trusted Root Certification Authorities** and select **Import**
7.	Follow the prompts in the Wizard to import the **Root Certificate** for the CA and click OK

From here, follow these steps to import the intermediate certificate(s):

1.	Right click **Intermediate Certification Authorities** and select **Import**
2.	Follow the prompts in the Wizard to import the **Intermediate Certificate(s)** for the CA and click OK


### Publish the CA Certificates to the NTAuth Store

By publishing the CA certificate to the enterprise NTAuth store, the system administrator indicates that the CA is trusted to issue certain certificates. This allows the correct certificates to be issued to smartcards and thus enables logon through PIV card authentication.

This task will configure Active Directory to trust the CA chain that signed the users' authentication certificates. To configure Active Directory with the signing CA Certificate chain:

1.	On the Active Directory Domain Controller, launch an **elevated command prompt** to use the **certutil** utility
2.	To **Publish the Certificate** to the **Enterprise NTAuth store** type

        certutil –dpublish –f "path_to_root_CA_cert" NTAuthCA

3.	The CA is now trusted to issue certificates of this type


