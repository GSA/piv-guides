---
layout: default
title: Network Tuning
collection: networkconfig
permalink: networkconfig/11_tuning/
---

## Network Tuning

### Cached Logon Credential Limit
When a user authenticates to a Windows system, their logon credentials are cached to enable logon in the event the domain controller is unavailable. The [United States Government Configuration Baseline (USGCB) for Windows 7](https://usgcb.nist.gov/usgcb/microsoft/download_win7.html) specifies that ***Interactive logon: Number of previous logons to cache (in case domain controller is not available)*** should be set to ***2***. In practice, this limit may be too low in Smart Card Logon environments, especially given the need to cache recovery credentials on mobile workstations.

The ***Number of previous logons to cache*** can be modified in local or group policy in the following location
***Computer Configuration\Windows Settings\Security Settings\Local Policies\Security options***

More information is available on [Microsoft TechNet](https://technet.microsoft.com/en-us/library/jj852209%28v=ws.11%29.aspx)

### CRL Retrieval Timeout Settings
By default, Windows will timeout downloading CRLs after 15 seconds. Some CRLs in the government environment are very large which may lead to timeouts. The default timeout value can be modified using local or group policy by modifying the ***Default URL retrieval timeout*** value found in the ***Certificate Path Validation Settings***, ***Network Retrieval**  tab, located in ***Computer Configuration\Windows Settings\Security Settings\Public Key Policies***

Source and step-by-step instructions:&nbsp; [Manage Network Retrieval and Path Validation](https://technet.microsoft.com/en-us/library/cc771429%28v=ws.11%29.aspx)

### OCSP Response Caching Behavior
By default, Microsoft Windows will retrieve and cache 50 OCSP Responses for any one issuing CA before switching to CRL mode. Depending on the size of the CRL, this may be a poor performance decision. For environments where workstations routinely interact with large CRLs, a large value may signficantly reduce network bandwidth consumption.  This value can be increased by setting the *CryptnetCachedOcspSwitchToCrlCount* DWORD value in the following registry key:
HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\SystemCertificates\ChainEngine\Config

Source:&nbsp; [Optimizing the Revocation Experience](https://technet.microsoft.com/en-us/library/ee619783%28v=ws.10%29.aspx)


### Windows 2008 R2 Server  and Large CRLs
The CRL processing logic on Windows Server 2008 R2 does not handle large CRLs very efficiently. This can lead to timeouts during Smart Card Logon or Client Authenticated TLS. A [hotfix](https://support.microsoft.com/en-us/help/2831238/crl-processing-causes-high-cpu-usage--heavy-network-traffic--and-servi) is available that can nearly double CRL processing speed. The hotfix is not needed on Windows 2012 R2 as these improvements are already built in.

From the [hotfix](https://support.microsoft.com/en-us/help/2831238/crl-processing-causes-high-cpu-usage--heavy-network-traffic--and-servi) page: 
> The hotfix packages provide the following improvements to the Windows
> Server 2008 R2-based domain controller:  Improves performance by
> eliminating concurrent multiple threads fetching against the same the
> same CRL. All successive fetch requests will then have to wait for the
> first fetch to complete and then share the result before they
> continue.
> 
>  - Optimizes memory usage for CRL decoding logic.
>  - Optimizes memory allocation for on-wire fetching.
