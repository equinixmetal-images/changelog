# Changelog for flatcar_3510.2.4_stable
 _Changes since **Stable 3510.2.3**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-2124](https://nvd.nist.gov/vuln/detail/CVE-2023-2124), [CVE-2023-3212](https://nvd.nist.gov/vuln/detail/CVE-2023-3212), [CVE-2023-35788](https://nvd.nist.gov/vuln/detail/CVE-2023-35788))
 
 #### Bug fixes:
 
 
 #### Changes:
 
 - Changed ext4 inode size of root partition to 256 bytes. This improves compatibility with applications and is necessary for 2038 readiness ([Flatcar#1082](https://github.com/flatcar/Flatcar/issues/1082))
 
 #### Updates:
 
 - Linux ([5.15.117](https://lwn.net/Articles/934622) (includes [5.15.116](https://lwn.net/Articles/934320), [5.15.115](https://lwn.net/Articles/933909), [5.15.114](https://lwn.net/Articles/933280)))
 - ca-certificates ([3.91](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_91.html))# Changelog for flatcar_3510.2.3_stable
_Changes since **Stable 3510.2.2**_
 
#### Security fixes:
 
- Linux ([CVE-2022-48425](https://nvd.nist.gov/vuln/detail/CVE-2022-48425))
 
#### Updates:
 
- Linux ([5.15.113](https://lwn.net/Articles/932883) (includes [5.15.112](https://lwn.net/Articles/932134)))
- ca-certificates ([3.90](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_90.html))