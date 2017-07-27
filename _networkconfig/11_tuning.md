---
layout: default
title: Network Tuning
collection: networkconfig
permalink: networkconfig/11_tuning/
---

### Network Tuning

Certificate Revocation Lists (CRLs) in Federal government environment could reach 20 MB. The default network time out setting for CRL retrieval is too low to fully download the CRL and needs to increase higher.
This link has steps to reset CRL timeout.

	https://technet.microsoft.com/en-us/library/cc771429(v=ws.11).aspx

CRL checking is a backup for OCSP checking, which timeout at default of 50. to resetting this number use following link:

	https://technet.microsoft.com/en-us/library/ee619783(v=ws.10).aspx#Defining Default Behavior
	
On Windows Server 2008 R2 or Windows 7, CRL processing may cause high CPU and network traffic usage. To alleviate the issue, apply following pathch:

    https://support.microsoft.com/en-us/help/2831238/crl-processing-causes-high-cpu-usage,-heavy-network-traffic,-and-servi
