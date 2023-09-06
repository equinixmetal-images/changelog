# Changelog for flatcar_3602.1.5_beta
 _Changes since **Beta 3602.1.4**_
 
 #### Security fixes:
 
 - Linux ([CVE-2022-40982](https://nvd.nist.gov/vuln/detail/CVE-2022-40982), [CVE-2022-41804](https://nvd.nist.gov/vuln/detail/CVE-2022-41804), [CVE-2023-20569](https://nvd.nist.gov/vuln/detail/CVE-2023-20569), [CVE-2023-20588](https://nvd.nist.gov/vuln/detail/CVE-2023-20588), [CVE-2023-40283](https://nvd.nist.gov/vuln/detail/CVE-2023-40283), [CVE-2023-4128](https://nvd.nist.gov/vuln/detail/CVE-2023-4128), [CVE-2023-23908](https://nvd.nist.gov/vuln/detail/CVE-2023-23908))
 
 #### Bug fixes:
 
 - Fixed the restart of Systemd services when the main process is being killed by a SIGHUP signal ([flatcar#1157](https://github.com/flatcar/Flatcar/issues/1157))
 
 #### Updates:
 
 - Linux ([5.15.129](https://lwn.net/Articles/943113) (includes [5.15.128](https://lwn.net/Articles/942866), [5.15.127](https://lwn.net/Articles/941775), [5.15.126](https://lwn.net/Articles/941296), [5.15.125](https://lwn.net/Articles/940801)))# Changelog for flatcar_3602.1.4_beta
 _Changes since **Beta 3602.1.3**_
 
 #### Security fixes:
 
 - Linux ([CVE-2022-48502](https://nvd.nist.gov/vuln/detail/CVE-2022-48502), [CVE-2023-20593](https://nvd.nist.gov/vuln/detail/CVE-2023-20593), [CVE-2023-2898](https://nvd.nist.gov/vuln/detail/CVE-2023-2898), [CVE-2023-31248](https://nvd.nist.gov/vuln/detail/CVE-2023-31248), [CVE-2023-35001](https://nvd.nist.gov/vuln/detail/CVE-2023-35001), [CVE-2023-3611](https://nvd.nist.gov/vuln/detail/CVE-2023-3611), [CVE-2023-3776](https://nvd.nist.gov/vuln/detail/CVE-2023-3776), [CVE-2023-38432](https://nvd.nist.gov/vuln/detail/CVE-2023-38432), [CVE-2023-3863](https://nvd.nist.gov/vuln/detail/CVE-2023-3863))
 - OpenSSH ([CVE-2023-38408](https://nvd.nist.gov/vuln/detail/CVE-2023-38408))
 - linux-firmware ([CVE-2023-20593](https://nvd.nist.gov/vuln/detail/CVE-2023-20593))

 #### Updates:
 
 - Linux ([5.15.124](https://lwn.net/Articles/940339) (includes [5.15.123](https://lwn.net/Articles/939424), [5.15.122](https://lwn.net/Articles/939104), [5.15.121](https://lwn.net/Articles/939016)))
 - ca-certificates ([3.92](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_92.html))
 - linux-firmware ([20230625](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tag/?h=20230625))
# Changelog for flatcar_3602.1.3_beta
 _Changes since **Beta 3602.1.2**_

 #### Updates:
 
 - Linux ([5.15.120](https://lwn.net/Articles/937404))# Changelog for flatcar_3602.1.2_beta
 _Changes since **Beta 3602.1.1**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-3338](https://nvd.nist.gov/vuln/detail/CVE-2023-3338), [CVE-2023-3390](https://nvd.nist.gov/vuln/detail/CVE-2023-3390))
 
 #### Bug fixes:
 
 - Ensured that the folder `/var/log/sssd` is created if it doesn't exist, required for `sssd.service` ([Flatcar#1096](https://github.com/flatcar/Flatcar/issues/1096))
 - Worked around a bash regression in `flatcar-install` and added error reporting for disk write failures ([Flatcar#1059](https://github.com/flatcar/Flatcar/issues/1059))
 
 #### Changes:
 
 - Changed ext4 inode size of root partition to 256 bytes. This improves compatibility with applications and is necessary for 2038 readiness ([Flatcar#1082](https://github.com/flatcar/Flatcar/issues/1082))
 
 #### Updates:
 
 - Linux ([5.15.119](https://lwn.net/Articles/936675) (includes [5.15.118](https://lwn.net/Articles/935584)))
 - ca-certificates ([3.91](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_91.html))