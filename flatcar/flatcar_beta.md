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