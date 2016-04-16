---
layout: default
title: Trust Stores
collection: networkconfig
permalink: networkconfig/trustedroots/
---
<div style="float:right; padding:10px; margin-right:20px; border-radius:10px; width:180px; height:40px; box-shadow:3px 3px 5px 0px; text-align:center; background-color:#CCC; color:#666666">
<div style="color:#000000">
<em>Moderate</em>
</div>
</div>

The root certificate and intermediate certificates are required to be added to the _Trust Store_ on all domain controllers, workstations and servers in the domain.

#### Addition of US Federal Certificate chains to the Trusted Root Certificate Authorities

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


#### Publish the Federal Common Policy Certificate Authority (COMMON) root certificate to the NTAuth Store

By publishing the CA certificate to the enterprise NTAuth store, the system administrator indicates that the CA is trusted for authentication using certain certificates.

This task will configure Active Directory to trust the CA chain that signed the users' authentication certificates. To configure Active Directory with the signing CA Certificate chain:

1.	On the Active Directory Domain Controller, launch an **elevated command prompt** to use the **certutil** utility
2.	To **Publish the Certificate** to the **Enterprise NTAuth store** type

        certutil –dpublish –f "path_to_root_CA_cert" NTAuthCA

3.	The CA is now trusted to issue certificates of this type
