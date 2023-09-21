# Changelog for flatcar_3510.2.8_stable
 _Changes since **Stable 3510.2.7**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-20588](https://nvd.nist.gov/vuln/detail/CVE-2023-20588), [CVE-2023-3772](https://nvd.nist.gov/vuln/detail/CVE-2023-3772), [CVE-2023-40283](https://nvd.nist.gov/vuln/detail/CVE-2023-40283), [CVE-2023-4128](https://nvd.nist.gov/vuln/detail/CVE-2023-4128), [CVE-2023-4206](https://nvd.nist.gov/vuln/detail/CVE-2023-4206), [CVE-2023-4207](https://nvd.nist.gov/vuln/detail/CVE-2023-4207), [CVE-2023-4208](https://nvd.nist.gov/vuln/detail/CVE-2023-4208), [CVE-2023-4273](https://nvd.nist.gov/vuln/detail/CVE-2023-4273), [CVE-2023-4569](https://nvd.nist.gov/vuln/detail/CVE-2023-4569))
 
 #### Changes:
 
 - Azure: Add support for Microsoft Azure Network Adapter (MANA) NICs on Azure ([scripts#1131](https://github.com/flatcar/scripts/pull/1131))
 
 #### Updates:
 
 - Linux ([5.15.129](https://lwn.net/Articles/943113) (includes [5.15.128](https://lwn.net/Articles/942866), [5.15.127](https://lwn.net/Articles/941775), [5.15.126](https://lwn.net/Articles/941296)))
 - ca-certificates ([3.93](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_93.html))# Changelog for flatcar_3510.2.6_stable
 _Changes since **Stable 3510.2.5**_
 
 #### Security fixes:
 
 - Linux ([CVE-2022-48502](https://nvd.nist.gov/vuln/detail/CVE-2022-48502), [CVE-2023-20593](https://nvd.nist.gov/vuln/detail/CVE-2023-20593), [CVE-2023-2898](https://nvd.nist.gov/vuln/detail/CVE-2023-2898), [CVE-2023-31248](https://nvd.nist.gov/vuln/detail/CVE-2023-31248), [CVE-2023-35001](https://nvd.nist.gov/vuln/detail/CVE-2023-35001), [CVE-2023-3611](https://nvd.nist.gov/vuln/detail/CVE-2023-3611), [CVE-2023-3776](https://nvd.nist.gov/vuln/detail/CVE-2023-3776), [CVE-2023-38432](https://nvd.nist.gov/vuln/detail/CVE-2023-38432), [CVE-2023-3863](https://nvd.nist.gov/vuln/detail/CVE-2023-3863))
 - linux-firmware ([CVE-2023-20593](https://nvd.nist.gov/vuln/detail/CVE-2023-20593))
 
 #### Updates:
 
 - Linux ([5.15.122](https://lwn.net/Articles/939104) (includes [5.15.121](https://lwn.net/Articles/939016), [5.15.120](https://lwn.net/Articles/937404)))
 - ca-certificates ([3.92](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_92.html))
 - linux-firmware ([20230625](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tag/?h=20230625))
# Changelog for flatcar_3510.2.5_stable
 _Changes since **Stable 3510.2.4**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-3338](https://nvd.nist.gov/vuln/detail/CVE-2023-3338), [CVE-2023-3390](https://nvd.nist.gov/vuln/detail/CVE-2023-3390))
 
 #### Bug fixes:
 
 - Resolved the conflicting FD usage of libselinux and systemd which caused, e.g., a systemd crash on certain watchdog interaction during shutdown (patch in systemd 252.11)
 
 #### Updates:
 
 - Linux ([5.15.119](https://lwn.net/Articles/936675) (includes [5.15.118](https://lwn.net/Articles/935584)))
 - systemd ([252.11](https://github.com/systemd/systemd-stable/releases/tag/v252.11) (from 252.5))# Changelog for flatcar_3510.2.4_stable
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