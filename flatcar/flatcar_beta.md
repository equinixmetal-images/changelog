# Changelog for flatcar_3975.1.1_beta
 _Changes since **Beta 3975.1.0**_
 
 #### Security fixes:
 
 - openssh ([CVE-2024-6387](https://nvd.nist.gov/vuln/detail/CVE-2024-6387))
 
 #### Updates:
 
 - Linux ([6.6.36](https://lwn.net/Articles/979850))
 - openssh ([9.7_p1](https://www.openssh.com/txt/release-9.7))# Changelog for flatcar_3913.1.0_beta
 _Changes since **Beta 3874.1.0**_
 
 #### Security fixes:
 
 - Downgraded xz-utils to 5.4.2 as precaution even though Flatcar is not affected of the SSH backdoor ([CVE-2024-3094](https://nvd.nist.gov/vuln/detail/CVE-2024-3094))
 - coreutils ([CVE-2024-0684](https://nvd.nist.gov/vuln/detail/CVE-2024-0684))
 - dnsmasq ([CVE-2023-28450](https://nvd.nist.gov/vuln/detail/CVE-2023-28450), [CVE-2023-50387](https://nvd.nist.gov/vuln/detail/CVE-2023-50387), [CVE-2023-50868](https://nvd.nist.gov/vuln/detail/CVE-2023-50868))
 - gcc ([CVE-2023-4039](https://nvd.nist.gov/vuln/detail/CVE-2023-4039))
 - glibc ([CVE-2023-5156](https://nvd.nist.gov/vuln/detail/CVE-2023-5156), [CVE-2023-6246](https://nvd.nist.gov/vuln/detail/CVE-2023-6246), [CVE-2023-6779](https://nvd.nist.gov/vuln/detail/CVE-2023-6779), [CVE-2023-6780](https://nvd.nist.gov/vuln/detail/CVE-2023-6780))
 - gnupg ([gnupg-2024-01-25](https://gnupg.org/blog/20240125-smartcard-backup-key.html))
 - gnutls ([CVE-2024-0567](https://nvd.nist.gov/vuln/detail/CVE-2024-0567), [CVE-2024-0553](https://nvd.nist.gov/vuln/detail/CVE-2024-0553))
 - libuv ([CVE-2024-24806](https://nvd.nist.gov/vuln/detail/CVE-2024-24806))
 - libxml2 ([CVE-2024-25062](https://nvd.nist.gov/vuln/detail/CVE-2024-25062))
 - openssl ([CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678), [CVE-2023-6129](https://nvd.nist.gov/vuln/detail/CVE-2023-6129), [CVE-2023-6237](https://nvd.nist.gov/vuln/detail/CVE-2023-6237), [CVE-2024-0727](https://nvd.nist.gov/vuln/detail/CVE-2024-0727))
 - sudo ([CVE-2023-42465](https://nvd.nist.gov/vuln/detail/CVE-2023-42465))
 - vim ([CVE-2023-48231](https://nvd.nist.gov/vuln/detail/CVE-2023-48231), [CVE-2023-48232](https://nvd.nist.gov/vuln/detail/CVE-2023-48232), [CVE-2023-48233](https://nvd.nist.gov/vuln/detail/CVE-2023-48233), [CVE-2023-48234](https://nvd.nist.gov/vuln/detail/CVE-2023-48234), [CVE-2023-48235](https://nvd.nist.gov/vuln/detail/CVE-2023-48235), [CVE-2023-48236](https://nvd.nist.gov/vuln/detail/CVE-2023-48236), [CVE-2023-48237](https://nvd.nist.gov/vuln/detail/CVE-2023-48237), [CVE-2023-48706](https://nvd.nist.gov/vuln/detail/CVE-2023-48706))
 
 #### Bug fixes:
 
 - Disabled user-configdrive.service on OpenStack when config drive is used, which caused the hostname to be overwritten. The coreos-cloudinit.service unit already runs on OpenStack if the system is not configured via ignition. ([Flatcar#1385](https://github.com/flatcar/Flatcar/issues/1385))
 - Fixed `toolbox` to prevent mounted `ctr` snapshots from being garbage-collected ([toolbox#9](https://github.com/flatcar/toolbox/pull/9))
 - Removed custom CloudSigma coreos-cloudinit service configuration since it will be called with the cloudsigma oem anyway. The restart of the service can also cause the serial port to be stuck in an nondeterministic state which breaks future runs.
 
 #### Changes:
 
 - A new format `qemu_uefi_secure` is introduced to test Flatcar for SecureBoot-enabled features. The format will be later merged into `qemu_uefi`.
 - Added Ignition Clevis support for encrypted disks unlocked with a TPM2 device or a Tang server ([scripts#1560](https://github.com/flatcar/scripts/pull/1560))
 - Added Scaleway images ([flatcar/scripts#1683](https://github.com/flatcar/scripts/pull/1683))
 - Added support for unlocking the rootfs with a TPM set up by systemd-cryptenroll ([bootengine#93](https://github.com/flatcar/bootengine/pull/93))
 - Disabled real-time priority for multipathd as it prevents the cgroups2 cpu controller from working. ([flatcar/scripts#1771](https://github.com/flatcar/scripts/pull/1771))
 - Enabled the GRUB TPM2 module to measure the boot code path and files into PCR 8+9 in UEFI ([scripts#1861](https://github.com/flatcar/scripts/pull/1861))
 - Provided a ZFS-2.2.2 Flatcar extension as optional systemd-sysext image with the release. Write 'zfs' to `/etc/flatcar/enabled-sysext.conf` through Ignition and the sysext will be installed during provisioning. ZFS support is experimental and ZFS is not supported for the root partition. ([flatcar/scripts#1742](https://github.com/flatcar/scripts/pull/1742))
 - Removed Linux drivers for Mellanox Technologies Switch ASICs family and Spectrum/Spectrum-2/Spectrum-3/Spectrum-4 Ethernet Switch ASICs to reduce the initrd size on AMD64 by ~5MB ([flatcar/scripts#1734](https://github.com/flatcar/scripts/pull/1734)). This change is part of the effort to reduce the initrd size ([flatcar#1381](https://github.com/flatcar/Flatcar/issues/1381)).
 - Removed coreos-cloudinit support for automatic keys conversion (e.g `reboot-strategy` -> `reboot_strategy`) ([scripts#1687](https://github.com/flatcar/scripts/pull/1687))
 - SDK: Unified qemu image formats, so that the `qemu_uefi` build target provides the regular `qemu` and the `qemu_uefi_secure` artifacts ([scripts#1847](https://github.com/flatcar/scripts/pull/1847))
 
 #### Updates:
 
 - Go ([1.20.14](https://go.dev/doc/devel/release#go1.20.14))
 - Ignition ([2.18.0](https://coreos.github.io/ignition/release-notes/#ignition-2180-2024-03-01) (includes [2.17.0](https://coreos.github.io/ignition/release-notes/#ignition-2170-2023-11-20), [2.16.2](https://coreos.github.io/ignition/release-notes/#ignition-2162-2023-07-12), [2.16.1](https://coreos.github.io/ignition/release-notes/#ignition-2161-2023-07-10) and [2.16.0](https://coreos.github.io/ignition/release-notes/#ignition-2160-2023-06-29)))
 - Linux Firmware ([20240312](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tag/?h=20240312) (includes [20240220](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tag/?h=20240220)))
 - audit ([3.1.1](https://github.com/linux-audit/audit-userspace/releases/tag/v3.1.1))
 - bind-tools ([9.16.48](https://bind9.readthedocs.io/en/v9.16.48/notes.html#notes-for-bind-9-16-48))
 - c-ares ([1.25.0](https://c-ares.org/changelog.html#1_25_0))
 - cJSON ([1.7.17](https://github.com/DaveGamble/cJSON/releases/tag/v1.7.17))
 - ca-certificates ([3.99](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_99.html))
 - checkpolicy ([3.6](https://github.com/SELinuxProject/selinux/releases/tag/3.6))
 - curl ([8.6.0](https://curl.se/changes.html#8_6_0))
 - ethtool ([6.6](https://git.kernel.org/pub/scm/network/ethtool/ethtool.git/tree/NEWS?h=v6.6))
 - glibc ([2.38](https://sourceware.org/pipermail/libc-alpha/2023-July/150524.html))
 - gnupg ([2.4.4](https://lists.gnupg.org/pipermail/gnupg-announce/2024q1/000481.html) (includes [2.2.42](https://dev.gnupg.org/T6307)))
 - less ([643](https://www.greenwoodsoftware.com/less/news.643.html))
 - libbsd ([0.11.8](https://lists.freedesktop.org/archives/libbsd/2024-January/000377.html))
 - libcap-ng ([0.8.4](https://github.com/stevegrubb/libcap-ng/releases/tag/v0.8.4))
 - libgcrypt ([1.10.3](https://git.gnupg.org/cgi-bin/gitweb.cgi?p=libgcrypt.git;a=blob;f=NEWS;h=b767dc1170eb479b9a311cca4074c58e4eedaf0b;hb=aa1610866f8e42bdc272584f0a717f32ee050a22))
 - libidn2 ([2.3.7](https://gitlab.com/libidn/libidn2/-/blob/v2.3.7/NEWS) (includes https://gitlab.com/libidn/libidn2/-/releases/v2.3.4)))
 - libksba ([1.6.6](https://git.gnupg.org/cgi-bin/gitweb.cgi?p=libksba.git;a=blob;f=NEWS;h=48b42025773e88fbb78d015d1f154fef4c80ef9f;hb=5b220df6f8216a9d5f6139c7b17f075374a27480))
 - libnvme ([1.7.1](https://github.com/linux-nvme/libnvme/releases/tag/v1.7.1) (includes [1.7](https://github.com/linux-nvme/libnvme/releases/tag/v1.7)))
 - libpsl ([0.21.5](https://github.com/rockdaboot/libpsl/blob/0.21.5/NEWS))
 - libseccomp ([2.5.5](https://github.com/seccomp/libseccomp/releases/tag/v2.5.5))
 - libselinux ([3.6](https://github.com/SELinuxProject/selinux/releases/tag/3.6))
 - libsemanage ([3.6](https://github.com/SELinuxProject/selinux/releases/tag/3.6))
 - libsepol ([3.6](https://github.com/SELinuxProject/selinux/releases/tag/3.6))
 - libuv ([1.48.0](https://github.com/libuv/libuv/releases/tag/v1.48.0))
 - libverto ([0.3.2](https://github.com/latchset/libverto/releases/tag/0.3.2))
 - libxml2 ([2.12.5](https://gitlab.gnome.org/GNOME/libxml2/-/releases/v2.12.5) (includes [2.12.4](https://gitlab.gnome.org/GNOME/libxml2/-/blob/v2.12.4/NEWS)))
 - lsof ([4.99.3](https://github.com/lsof-org/lsof/releases/tag/4.99.3) (includes [4.99.2](https://github.com/lsof-org/lsof/releases/tag/4.99.2) and [4.99.1](https://github.com/lsof-org/lsof/releases/tag/4.99.1)))
 - mime-types ([2.1.54](https://pagure.io/mailcap/blob/9699055a1b4dfb90f7594ee2e8dda705fa56d3b8/f/NEWS))
 - multipath-tools ([0.9.7](https://github.com/opensvc/multipath-tools/commits/0.9.7))
 - nvme-cli ([2.7.1](https://github.com/linux-nvme/nvme-cli/releases/tag/v2.7.1) (includes [2.7](https://github.com/linux-nvme/nvme-cli/releases/tag/v2.7)))
 - openssl ([3.2.1](https://github.com/openssl/openssl/blob/openssl-3.2.1/CHANGES.md))
 - policycoreutils ([3.6](https://github.com/SELinuxProject/selinux/releases/tag/3.6))
 - semodule-utils ([3.6](https://github.com/SELinuxProject/selinux/releases/tag/3.6))
 - shim ([15.8](https://github.com/rhboot/shim/releases/tag/15.8))
 - sqlite ([3.45.1](https://www.sqlite.org/releaselog/3_45_1.html))
 - sudo ([1.9.15p5](https://www.sudo.ws/releases/stable/#1.9.15p5))
 - systemd ([255.3](https://github.com/systemd/systemd-stable/releases/tag/v255.3) (from 252.11))
 - thin-provisioning-tools ([1.0.10](https://github.com/jthornber/thin-provisioning-tools/commits/v1.0.10/))
 - traceroute ([2.1.5](https://sourceforge.net/projects/traceroute/files/traceroute/traceroute-2.1.5/) (includes [2.1.4](https://sourceforge.net/projects/traceroute/files/traceroute/traceroute%202.1.4/)))
 - usbutils ([017](https://git.kernel.org/pub/scm/linux/kernel/git/gregkh/usbutils.git/tree/NEWS?h=v017))
 - util-linux ([2.39.3](https://github.com/util-linux/util-linux/blob/v2.39.3/Documentation/releases/v2.39.3-ReleaseNotes))
 - vim ([9.0.2167](https://github.com/vim/vim/commits/v9.0.2167/))
 - xmlsec ([1.3.3](https://github.com/lsh123/xmlsec/releases/tag/1.3.3))
 - SDK: python ([3.11.8](https://www.get-python.org/downloads/release/python-3118/))
 - SDK: qemu ([8.1.5](https://wiki.qemu.org/ChangeLog/8.1))
 - SDK: Rust ([1.76.0](https://github.com/rust-lang/rust/releases/tag/1.76.0))


 _Changes since **Alpha 3913.0.0**_
 
 #### Security fixes:
 
 - Downgraded xz-utils to 5.4.2 as precaution even though Flatcar is not affected of the SSH backdoor ([CVE-2024-3094](https://nvd.nist.gov/vuln/detail/CVE-2024-3094))
 
 #### Bug fixes:
 
 - Disabled user-configdrive.service on OpenStack when config drive is used, which caused the hostname to be overwritten. The coreos-cloudinit.service unit already runs on OpenStack if the system is not configured via ignition. ([Flatcar#1385](https://github.com/flatcar/Flatcar/issues/1385))
 - Fixed `toolbox` to prevent mounted `ctr` snapshots from being garbage-collected ([toolbox#9](https://github.com/flatcar/toolbox/pull/9))
 
 #### Changes:
 
 - Added support for unlocking the rootfs with a TPM set up by systemd-cryptenroll ([bootengine#93](https://github.com/flatcar/bootengine/pull/93))
 - Disabled real-time priority for multipathd as it prevents the cgroups2 cpu controller from working. ([scripts#1771](https://github.com/flatcar/scripts/pull/1771))
 - Enabled the GRUB TPM2 module to measure the boot code path and files into PCR 8+9 in UEFI ([scripts#1861](https://github.com/flatcar/scripts/pull/1861))
 - SDK: Unified qemu image formats, so that the `qemu_uefi` build target provides the regular `qemu` and the `qemu_uefi_secure` artifacts ([scripts#1847](https://github.com/flatcar/scripts/pull/1847))
 
 #### Updates:
 
 - ca-certificates ([3.99](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_99.html))
# Changelog for flatcar_3850.1.0_beta
 _Changes since **Beta 3815.1.0**_
 
 #### Security fixes:
 
 - Linux ([CVE-2022-27672](https://nvd.nist.gov/vuln/detail/CVE-2022-27672), [CVE-2022-36402](https://nvd.nist.gov/vuln/detail/CVE-2022-36402), [CVE-2022-36402](https://nvd.nist.gov/vuln/detail/CVE-2022-36402), [CVE-2022-40982](https://nvd.nist.gov/vuln/detail/CVE-2022-40982), [CVE-2022-4269](https://nvd.nist.gov/vuln/detail/CVE-2022-4269), [CVE-2022-45886](https://nvd.nist.gov/vuln/detail/CVE-2022-45886), [CVE-2022-45887](https://nvd.nist.gov/vuln/detail/CVE-2022-45887), [CVE-2022-45919](https://nvd.nist.gov/vuln/detail/CVE-2022-45919), [CVE-2022-48425](https://nvd.nist.gov/vuln/detail/CVE-2022-48425), [CVE-2023-0160](https://nvd.nist.gov/vuln/detail/CVE-2023-0160), [CVE-2023-0160](https://nvd.nist.gov/vuln/detail/CVE-2023-0160), [CVE-2023-0459](https://nvd.nist.gov/vuln/detail/CVE-2023-0459), [CVE-2023-1032](https://nvd.nist.gov/vuln/detail/CVE-2023-1032), [CVE-2023-1076](https://nvd.nist.gov/vuln/detail/CVE-2023-1076), [CVE-2023-1077](https://nvd.nist.gov/vuln/detail/CVE-2023-1077), [CVE-2023-1079](https://nvd.nist.gov/vuln/detail/CVE-2023-1079), [CVE-2023-1118](https://nvd.nist.gov/vuln/detail/CVE-2023-1118), [CVE-2023-1192](https://nvd.nist.gov/vuln/detail/CVE-2023-1192), [CVE-2023-1194](https://nvd.nist.gov/vuln/detail/CVE-2023-1194), [CVE-2023-1206](https://nvd.nist.gov/vuln/detail/CVE-2023-1206), [CVE-2023-1281](https://nvd.nist.gov/vuln/detail/CVE-2023-1281), [CVE-2023-1380](https://nvd.nist.gov/vuln/detail/CVE-2023-1380), [CVE-2023-1380](https://nvd.nist.gov/vuln/detail/CVE-2023-1380), [CVE-2023-1513](https://nvd.nist.gov/vuln/detail/CVE-2023-1513), [CVE-2023-1583](https://nvd.nist.gov/vuln/detail/CVE-2023-1583), [CVE-2023-1611](https://nvd.nist.gov/vuln/detail/CVE-2023-1611), [CVE-2023-1670](https://nvd.nist.gov/vuln/detail/CVE-2023-1670), [CVE-2023-1829](https://nvd.nist.gov/vuln/detail/CVE-2023-1829), [CVE-2023-1855](https://nvd.nist.gov/vuln/detail/CVE-2023-1855), [CVE-2023-1859](https://nvd.nist.gov/vuln/detail/CVE-2023-1859), [CVE-2023-1989](https://nvd.nist.gov/vuln/detail/CVE-2023-1989), [CVE-2023-1990](https://nvd.nist.gov/vuln/detail/CVE-2023-1990), [CVE-2023-1998](https://nvd.nist.gov/vuln/detail/CVE-2023-1998), [CVE-2023-2002](https://nvd.nist.gov/vuln/detail/CVE-2023-2002), [CVE-2023-2002](https://nvd.nist.gov/vuln/detail/CVE-2023-2002), [CVE-2023-20569](https://nvd.nist.gov/vuln/detail/CVE-2023-20569), [CVE-2023-20588](https://nvd.nist.gov/vuln/detail/CVE-2023-20588), [CVE-2023-20593](https://nvd.nist.gov/vuln/detail/CVE-2023-20593), [CVE-2023-2124](https://nvd.nist.gov/vuln/detail/CVE-2023-2124), [CVE-2023-21255](https://nvd.nist.gov/vuln/detail/CVE-2023-21255), [CVE-2023-21264](https://nvd.nist.gov/vuln/detail/CVE-2023-21264), [CVE-2023-2156](https://nvd.nist.gov/vuln/detail/CVE-2023-2156), [CVE-2023-2156](https://nvd.nist.gov/vuln/detail/CVE-2023-2156), [CVE-2023-2163](https://nvd.nist.gov/vuln/detail/CVE-2023-2163), [CVE-2023-2163](https://nvd.nist.gov/vuln/detail/CVE-2023-2163), [CVE-2023-2194](https://nvd.nist.gov/vuln/detail/CVE-2023-2194), [CVE-2023-2235](https://nvd.nist.gov/vuln/detail/CVE-2023-2235), [CVE-2023-2248](https://nvd.nist.gov/vuln/detail/CVE-2023-2248), [CVE-2023-2248](https://nvd.nist.gov/vuln/detail/CVE-2023-2248), [CVE-2023-2269](https://nvd.nist.gov/vuln/detail/CVE-2023-2269), [CVE-2023-2269](https://nvd.nist.gov/vuln/detail/CVE-2023-2269), [CVE-2023-2483](https://nvd.nist.gov/vuln/detail/CVE-2023-2483), [CVE-2023-25012](https://nvd.nist.gov/vuln/detail/CVE-2023-25012), [CVE-2023-25775](https://nvd.nist.gov/vuln/detail/CVE-2023-25775), [CVE-2023-25775](https://nvd.nist.gov/vuln/detail/CVE-2023-25775), [CVE-2023-2598](https://nvd.nist.gov/vuln/detail/CVE-2023-2598), [CVE-2023-26545](https://nvd.nist.gov/vuln/detail/CVE-2023-26545), [CVE-2023-28466](https://nvd.nist.gov/vuln/detail/CVE-2023-28466), [CVE-2023-28866](https://nvd.nist.gov/vuln/detail/CVE-2023-28866), [CVE-2023-2898](https://nvd.nist.gov/vuln/detail/CVE-2023-2898), [CVE-2023-2985](https://nvd.nist.gov/vuln/detail/CVE-2023-2985), [CVE-2023-30456](https://nvd.nist.gov/vuln/detail/CVE-2023-30456), [CVE-2023-30772](https://nvd.nist.gov/vuln/detail/CVE-2023-30772), [CVE-2023-3090](https://nvd.nist.gov/vuln/detail/CVE-2023-3090), [CVE-2023-31085](https://nvd.nist.gov/vuln/detail/CVE-2023-31085), [CVE-2023-3117](https://nvd.nist.gov/vuln/detail/CVE-2023-3117), [CVE-2023-31248](https://nvd.nist.gov/vuln/detail/CVE-2023-31248), [CVE-2023-3141](https://nvd.nist.gov/vuln/detail/CVE-2023-3141), [CVE-2023-31436](https://nvd.nist.gov/vuln/detail/CVE-2023-31436), [CVE-2023-31436](https://nvd.nist.gov/vuln/detail/CVE-2023-31436), [CVE-2023-3212](https://nvd.nist.gov/vuln/detail/CVE-2023-3212), [CVE-2023-3220](https://nvd.nist.gov/vuln/detail/CVE-2023-3220), [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233), [CVE-2023-32233](https://nvd.nist.gov/vuln/detail/CVE-2023-32233), [CVE-2023-32247](https://nvd.nist.gov/vuln/detail/CVE-2023-32247), [CVE-2023-32247](https://nvd.nist.gov/vuln/detail/CVE-2023-32247), [CVE-2023-32248](https://nvd.nist.gov/vuln/detail/CVE-2023-32248), [CVE-2023-32248](https://nvd.nist.gov/vuln/detail/CVE-2023-32248), [CVE-2023-32250](https://nvd.nist.gov/vuln/detail/CVE-2023-32250), [CVE-2023-32250](https://nvd.nist.gov/vuln/detail/CVE-2023-32250), [CVE-2023-32252](https://nvd.nist.gov/vuln/detail/CVE-2023-32252), [CVE-2023-32252](https://nvd.nist.gov/vuln/detail/CVE-2023-32252), [CVE-2023-32254](https://nvd.nist.gov/vuln/detail/CVE-2023-32254), [CVE-2023-32254](https://nvd.nist.gov/vuln/detail/CVE-2023-32254), [CVE-2023-32257](https://nvd.nist.gov/vuln/detail/CVE-2023-32257), [CVE-2023-32257](https://nvd.nist.gov/vuln/detail/CVE-2023-32257), [CVE-2023-32258](https://nvd.nist.gov/vuln/detail/CVE-2023-32258), [CVE-2023-32258](https://nvd.nist.gov/vuln/detail/CVE-2023-32258), [CVE-2023-3268](https://nvd.nist.gov/vuln/detail/CVE-2023-3268), [CVE-2023-3268](https://nvd.nist.gov/vuln/detail/CVE-2023-3268), [CVE-2023-3269](https://nvd.nist.gov/vuln/detail/CVE-2023-3269), [CVE-2023-3269](https://nvd.nist.gov/vuln/detail/CVE-2023-3269), [CVE-2023-3312](https://nvd.nist.gov/vuln/detail/CVE-2023-3312), [CVE-2023-3312](https://nvd.nist.gov/vuln/detail/CVE-2023-3312), [CVE-2023-3317](https://nvd.nist.gov/vuln/detail/CVE-2023-3317), [CVE-2023-33203](https://nvd.nist.gov/vuln/detail/CVE-2023-33203), [CVE-2023-33250](https://nvd.nist.gov/vuln/detail/CVE-2023-33250), [CVE-2023-33250](https://nvd.nist.gov/vuln/detail/CVE-2023-33250), [CVE-2023-33288](https://nvd.nist.gov/vuln/detail/CVE-2023-33288), [CVE-2023-3355](https://nvd.nist.gov/vuln/detail/CVE-2023-3355), [CVE-2023-3390](https://nvd.nist.gov/vuln/detail/CVE-2023-3390), [CVE-2023-33951](https://nvd.nist.gov/vuln/detail/CVE-2023-33951), [CVE-2023-33951](https://nvd.nist.gov/vuln/detail/CVE-2023-33951), [CVE-2023-33952](https://nvd.nist.gov/vuln/detail/CVE-2023-33952), [CVE-2023-33952](https://nvd.nist.gov/vuln/detail/CVE-2023-33952), [CVE-2023-34255](https://nvd.nist.gov/vuln/detail/CVE-2023-34255), [CVE-2023-34256](https://nvd.nist.gov/vuln/detail/CVE-2023-34256), [CVE-2023-34256](https://nvd.nist.gov/vuln/detail/CVE-2023-34256), [CVE-2023-34319](https://nvd.nist.gov/vuln/detail/CVE-2023-34319), [CVE-2023-34324](https://nvd.nist.gov/vuln/detail/CVE-2023-34324), [CVE-2023-35001](https://nvd.nist.gov/vuln/detail/CVE-2023-35001), [CVE-2023-35788](https://nvd.nist.gov/vuln/detail/CVE-2023-35788), [CVE-2023-35823](https://nvd.nist.gov/vuln/detail/CVE-2023-35823), [CVE-2023-35823](https://nvd.nist.gov/vuln/detail/CVE-2023-35823), [CVE-2023-35824](https://nvd.nist.gov/vuln/detail/CVE-2023-35824), [CVE-2023-35824](https://nvd.nist.gov/vuln/detail/CVE-2023-35824), [CVE-2023-35826](https://nvd.nist.gov/vuln/detail/CVE-2023-35826), [CVE-2023-35826](https://nvd.nist.gov/vuln/detail/CVE-2023-35826), [CVE-2023-35827](https://nvd.nist.gov/vuln/detail/CVE-2023-35827), [CVE-2023-35828](https://nvd.nist.gov/vuln/detail/CVE-2023-35828), [CVE-2023-35828](https://nvd.nist.gov/vuln/detail/CVE-2023-35828), [CVE-2023-35829](https://nvd.nist.gov/vuln/detail/CVE-2023-35829), [CVE-2023-35829](https://nvd.nist.gov/vuln/detail/CVE-2023-35829), [CVE-2023-3609](https://nvd.nist.gov/vuln/detail/CVE-2023-3609), [CVE-2023-3610](https://nvd.nist.gov/vuln/detail/CVE-2023-3610), [CVE-2023-3610](https://nvd.nist.gov/vuln/detail/CVE-2023-3610), [CVE-2023-3611](https://nvd.nist.gov/vuln/detail/CVE-2023-3611), [CVE-2023-37453](https://nvd.nist.gov/vuln/detail/CVE-2023-37453), [CVE-2023-37453](https://nvd.nist.gov/vuln/detail/CVE-2023-37453), [CVE-2023-3772](https://nvd.nist.gov/vuln/detail/CVE-2023-3772), [CVE-2023-3773](https://nvd.nist.gov/vuln/detail/CVE-2023-3773), [CVE-2023-3776](https://nvd.nist.gov/vuln/detail/CVE-2023-3776), [CVE-2023-3777](https://nvd.nist.gov/vuln/detail/CVE-2023-3777), [CVE-2023-38409](https://nvd.nist.gov/vuln/detail/CVE-2023-38409), [CVE-2023-38426](https://nvd.nist.gov/vuln/detail/CVE-2023-38426), [CVE-2023-38427](https://nvd.nist.gov/vuln/detail/CVE-2023-38427), [CVE-2023-38428](https://nvd.nist.gov/vuln/detail/CVE-2023-38428), [CVE-2023-38429](https://nvd.nist.gov/vuln/detail/CVE-2023-38429), [CVE-2023-38430](https://nvd.nist.gov/vuln/detail/CVE-2023-38430), [CVE-2023-38431](https://nvd.nist.gov/vuln/detail/CVE-2023-38431), [CVE-2023-38432](https://nvd.nist.gov/vuln/detail/CVE-2023-38432), [CVE-2023-38432](https://nvd.nist.gov/vuln/detail/CVE-2023-38432), [CVE-2023-3863](https://nvd.nist.gov/vuln/detail/CVE-2023-3863), [CVE-2023-3863](https://nvd.nist.gov/vuln/detail/CVE-2023-3863), [CVE-2023-3865](https://nvd.nist.gov/vuln/detail/CVE-2023-3865), [CVE-2023-3865](https://nvd.nist.gov/vuln/detail/CVE-2023-3865), [CVE-2023-3866](https://nvd.nist.gov/vuln/detail/CVE-2023-3866), [CVE-2023-3866](https://nvd.nist.gov/vuln/detail/CVE-2023-3866), [CVE-2023-3867](https://nvd.nist.gov/vuln/detail/CVE-2023-3867), [CVE-2023-39189](https://nvd.nist.gov/vuln/detail/CVE-2023-39189), [CVE-2023-39191](https://nvd.nist.gov/vuln/detail/CVE-2023-39191), [CVE-2023-39192](https://nvd.nist.gov/vuln/detail/CVE-2023-39192), [CVE-2023-39192](https://nvd.nist.gov/vuln/detail/CVE-2023-39192), [CVE-2023-39193](https://nvd.nist.gov/vuln/detail/CVE-2023-39193), [CVE-2023-39193](https://nvd.nist.gov/vuln/detail/CVE-2023-39193), [CVE-2023-39194](https://nvd.nist.gov/vuln/detail/CVE-2023-39194), [CVE-2023-39197](https://nvd.nist.gov/vuln/detail/CVE-2023-39197), [CVE-2023-39197](https://nvd.nist.gov/vuln/detail/CVE-2023-39197), [CVE-2023-39198](https://nvd.nist.gov/vuln/detail/CVE-2023-39198), [CVE-2023-4004](https://nvd.nist.gov/vuln/detail/CVE-2023-4004), [CVE-2023-4015](https://nvd.nist.gov/vuln/detail/CVE-2023-4015), [CVE-2023-40283](https://nvd.nist.gov/vuln/detail/CVE-2023-40283), [CVE-2023-40791](https://nvd.nist.gov/vuln/detail/CVE-2023-40791), [CVE-2023-4128](https://nvd.nist.gov/vuln/detail/CVE-2023-4128), [CVE-2023-4132](https://nvd.nist.gov/vuln/detail/CVE-2023-4132), [CVE-2023-4133](https://nvd.nist.gov/vuln/detail/CVE-2023-4133), [CVE-2023-4133](https://nvd.nist.gov/vuln/detail/CVE-2023-4133), [CVE-2023-4134](https://nvd.nist.gov/vuln/detail/CVE-2023-4134), [CVE-2023-4134](https://nvd.nist.gov/vuln/detail/CVE-2023-4134), [CVE-2023-4147](https://nvd.nist.gov/vuln/detail/CVE-2023-4147), [CVE-2023-4155](https://nvd.nist.gov/vuln/detail/CVE-2023-4155), [CVE-2023-4194](https://nvd.nist.gov/vuln/detail/CVE-2023-4194), [CVE-2023-4206](https://nvd.nist.gov/vuln/detail/CVE-2023-4206), [CVE-2023-4207](https://nvd.nist.gov/vuln/detail/CVE-2023-4207), [CVE-2023-4208](https://nvd.nist.gov/vuln/detail/CVE-2023-4208), [CVE-2023-4244](https://nvd.nist.gov/vuln/detail/CVE-2023-4244), [CVE-2023-4273](https://nvd.nist.gov/vuln/detail/CVE-2023-4273), [CVE-2023-42752](https://nvd.nist.gov/vuln/detail/CVE-2023-42752), [CVE-2023-42752](https://nvd.nist.gov/vuln/detail/CVE-2023-42752), [CVE-2023-42753](https://nvd.nist.gov/vuln/detail/CVE-2023-42753), [CVE-2023-42753](https://nvd.nist.gov/vuln/detail/CVE-2023-42753), [CVE-2023-42754](https://nvd.nist.gov/vuln/detail/CVE-2023-42754), [CVE-2023-42756](https://nvd.nist.gov/vuln/detail/CVE-2023-42756), [CVE-2023-44466](https://nvd.nist.gov/vuln/detail/CVE-2023-44466), [CVE-2023-4563](https://nvd.nist.gov/vuln/detail/CVE-2023-4563), [CVE-2023-4569](https://nvd.nist.gov/vuln/detail/CVE-2023-4569), [CVE-2023-45862](https://nvd.nist.gov/vuln/detail/CVE-2023-45862), [CVE-2023-45863](https://nvd.nist.gov/vuln/detail/CVE-2023-45863), [CVE-2023-45871](https://nvd.nist.gov/vuln/detail/CVE-2023-45871), [CVE-2023-45871](https://nvd.nist.gov/vuln/detail/CVE-2023-45871), [CVE-2023-45898](https://nvd.nist.gov/vuln/detail/CVE-2023-45898), [CVE-2023-4610](https://nvd.nist.gov/vuln/detail/CVE-2023-4610), [CVE-2023-4611](https://nvd.nist.gov/vuln/detail/CVE-2023-4611), [CVE-2023-4623](https://nvd.nist.gov/vuln/detail/CVE-2023-4623), [CVE-2023-4623](https://nvd.nist.gov/vuln/detail/CVE-2023-4623), [CVE-2023-46343](https://nvd.nist.gov/vuln/detail/CVE-2023-46343), [CVE-2023-46813](https://nvd.nist.gov/vuln/detail/CVE-2023-46813), [CVE-2023-46838](https://nvd.nist.gov/vuln/detail/CVE-2023-46838), [CVE-2023-46838](https://nvd.nist.gov/vuln/detail/CVE-2023-46838), [CVE-2023-46862](https://nvd.nist.gov/vuln/detail/CVE-2023-46862), [CVE-2023-46862](https://nvd.nist.gov/vuln/detail/CVE-2023-46862), [CVE-2023-4881](https://nvd.nist.gov/vuln/detail/CVE-2023-4881), [CVE-2023-4921](https://nvd.nist.gov/vuln/detail/CVE-2023-4921), [CVE-2023-50431](https://nvd.nist.gov/vuln/detail/CVE-2023-50431), [CVE-2023-50431](https://nvd.nist.gov/vuln/detail/CVE-2023-50431), [CVE-2023-5090](https://nvd.nist.gov/vuln/detail/CVE-2023-5090), [CVE-2023-51042](https://nvd.nist.gov/vuln/detail/CVE-2023-51042), [CVE-2023-51043](https://nvd.nist.gov/vuln/detail/CVE-2023-51043), [CVE-2023-5158](https://nvd.nist.gov/vuln/detail/CVE-2023-5158), [CVE-2023-51779](https://nvd.nist.gov/vuln/detail/CVE-2023-51779), [CVE-2023-51780](https://nvd.nist.gov/vuln/detail/CVE-2023-51780), [CVE-2023-51781](https://nvd.nist.gov/vuln/detail/CVE-2023-51781), [CVE-2023-51782](https://nvd.nist.gov/vuln/detail/CVE-2023-51782), [CVE-2023-5197](https://nvd.nist.gov/vuln/detail/CVE-2023-5197), [CVE-2023-5345](https://nvd.nist.gov/vuln/detail/CVE-2023-5345), [CVE-2023-5633](https://nvd.nist.gov/vuln/detail/CVE-2023-5633), [CVE-2023-5717](https://nvd.nist.gov/vuln/detail/CVE-2023-5717), [CVE-2023-5972](https://nvd.nist.gov/vuln/detail/CVE-2023-5972), [CVE-2023-6039](https://nvd.nist.gov/vuln/detail/CVE-2023-6039), [CVE-2023-6111](https://nvd.nist.gov/vuln/detail/CVE-2023-6111), [CVE-2023-6121](https://nvd.nist.gov/vuln/detail/CVE-2023-6121), [CVE-2023-6176](https://nvd.nist.gov/vuln/detail/CVE-2023-6176), [CVE-2023-6200](https://nvd.nist.gov/vuln/detail/CVE-2023-6200), [CVE-2023-6531](https://nvd.nist.gov/vuln/detail/CVE-2023-6531), [CVE-2023-6546](https://nvd.nist.gov/vuln/detail/CVE-2023-6546), [CVE-2023-6560](https://nvd.nist.gov/vuln/detail/CVE-2023-6560), [CVE-2023-6606](https://nvd.nist.gov/vuln/detail/CVE-2023-6606), [CVE-2023-6610](https://nvd.nist.gov/vuln/detail/CVE-2023-6610), [CVE-2023-6610](https://nvd.nist.gov/vuln/detail/CVE-2023-6610), [CVE-2023-6622](https://nvd.nist.gov/vuln/detail/CVE-2023-6622), [CVE-2023-6817](https://nvd.nist.gov/vuln/detail/CVE-2023-6817), [CVE-2023-6915](https://nvd.nist.gov/vuln/detail/CVE-2023-6915), [CVE-2023-6915](https://nvd.nist.gov/vuln/detail/CVE-2023-6915), [CVE-2023-6931](https://nvd.nist.gov/vuln/detail/CVE-2023-6931), [CVE-2023-6932](https://nvd.nist.gov/vuln/detail/CVE-2023-6932), [CVE-2023-7192](https://nvd.nist.gov/vuln/detail/CVE-2023-7192), [CVE-2024-0193](https://nvd.nist.gov/vuln/detail/CVE-2024-0193), [CVE-2024-0443](https://nvd.nist.gov/vuln/detail/CVE-2024-0443), [CVE-2024-0565](https://nvd.nist.gov/vuln/detail/CVE-2024-0565), [CVE-2024-0582](https://nvd.nist.gov/vuln/detail/CVE-2024-0582), [CVE-2024-0584](https://nvd.nist.gov/vuln/detail/CVE-2024-0584), [CVE-2024-0607](https://nvd.nist.gov/vuln/detail/CVE-2024-0607), [CVE-2024-0607](https://nvd.nist.gov/vuln/detail/CVE-2024-0607), [CVE-2024-0639](https://nvd.nist.gov/vuln/detail/CVE-2024-0639), [CVE-2024-0641](https://nvd.nist.gov/vuln/detail/CVE-2024-0641), [CVE-2024-0646](https://nvd.nist.gov/vuln/detail/CVE-2024-0646), [CVE-2024-0775](https://nvd.nist.gov/vuln/detail/CVE-2024-0775), [CVE-2024-0775](https://nvd.nist.gov/vuln/detail/CVE-2024-0775), [CVE-2024-1085](https://nvd.nist.gov/vuln/detail/CVE-2024-1085), [CVE-2024-1085](https://nvd.nist.gov/vuln/detail/CVE-2024-1085), [CVE-2024-1086](https://nvd.nist.gov/vuln/detail/CVE-2024-1086), [CVE-2024-1086](https://nvd.nist.gov/vuln/detail/CVE-2024-1086), [CVE-2024-1312](https://nvd.nist.gov/vuln/detail/CVE-2024-1312), [CVE-2024-22705](https://nvd.nist.gov/vuln/detail/CVE-2024-22705), [CVE-2024-23849](https://nvd.nist.gov/vuln/detail/CVE-2024-23849), [CVE-2024-23849](https://nvd.nist.gov/vuln/detail/CVE-2024-23849))
 - binutils ([CVE-2023-1972](https://nvd.nist.gov/vuln/detail/CVE-2023-1972))
 - curl ([CVE-2023-46218](https://nvd.nist.gov/vuln/detail/CVE-2023-46218), [CVE-2023-46219](https://nvd.nist.gov/vuln/detail/CVE-2023-46219))
 - docker ([CVE-2024-24557](https://nvd.nist.gov/vuln/detail/CVE-2024-24557))
 - gnutls ([CVE-2023-5981](https://nvd.nist.gov/vuln/detail/CVE-2023-5981))
 - intel-microcode ([CVE-2023-23583](https://nvd.nist.gov/vuln/detail/CVE-2023-23583))
 - libxml2 ([CVE-2023-45322](https://nvd.nist.gov/vuln/detail/CVE-2023-45322))
 - openssh ([CVE-2023-48795](https://nvd.nist.gov/vuln/detail/CVE-2023-48795), [CVE-2023-51384](https://nvd.nist.gov/vuln/detail/CVE-2023-51384), [CVE-2023-51385](https://nvd.nist.gov/vuln/detail/CVE-2023-51385))
 - openssl ([CVE-2023-3817](https://nvd.nist.gov/vuln/detail/CVE-2023-3817), [CVE-2023-5363](https://nvd.nist.gov/vuln/detail/CVE-2023-5363), [CVE-2023-5678](https://nvd.nist.gov/vuln/detail/CVE-2023-5678))
 - runc ([CVE-2024-21626](https://nvd.nist.gov/vuln/detail/CVE-2024-21626))
 - traceroute ([CVE-2023-46316](https://nvd.nist.gov/vuln/detail/CVE-2023-46316))
 - vim ([CVE-2023-5344](https://nvd.nist.gov/vuln/detail/CVE-2023-5344), [CVE-2023-5441](https://nvd.nist.gov/vuln/detail/CVE-2023-5441), [CVE-2023-5535](https://nvd.nist.gov/vuln/detail/CVE-2023-5535), [CVE-2023-46246](https://nvd.nist.gov/vuln/detail/CVE-2023-46246))
 - SDK: perl ([CVE-2023-47038](https://nvd.nist.gov/vuln/detail/CVE-2023-47038))
 
 #### Bug fixes:
 
 - Added a workaround for old airgapped/proxied update-engine clients to be able to update to this release ([Flatcar#1332](https://github.com/flatcar/Flatcar/issues/1332), [update_engine#38](https://github.com/flatcar/update_engine/pull/38))
 - Fixed the handling of OEM update payloads in a Nebraska response with self-hosted packages ([ue-rs#49](https://github.com/flatcar/ue-rs/pull/49))
 - Forwarded the proxy environment variables of `update-engine.service` to the postinstall script to support fetching OEM systemd-sysext payloads through a proxy ([Flatcar#1326](https://github.com/flatcar/Flatcar/issues/1326))
 
 #### Changes:
 
 - Added a `flatcar-update --oem-payloads <yes|no>` flag to skip providing OEM payloads, e.g., for downgrades ([init#114](https://github.com/flatcar/init/pull/114))
 - Update generation SLSA provenance info from v0.2 to v1.0.
 
 #### Updates:
 
- Linux ([6.6.16](https://lwn.net/Articles/961011) (includes [6.6.15](https://lwn.net/Articles/960441), [6.6.14](https://lwn.net/Articles/959512), [6.6.13](https://lwn.net/Articles/958862), [6.6.12](https://lwn.net/Articles/958342), [6.6.11](https://lwn.net/Articles/957375), [6.6.10](https://lwn.net/Articles/957008), [6.6.9](https://lwn.net/Articles/956525), [6.6.8](https://lwn.net/Articles/955813), [6.6.7](https://lwn.net/Articles/954990/), [6.6](https://kernelnewbies.org/Linux_6.6)))
- Linux Firmware ([20231211](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tag/?h=20231211))
- Go ([1.20.13](https://go.dev/doc/devel/release#go1.20.13))
- bash ([5.2_p21](https://git.savannah.gnu.org/cgit/bash.git/log/?id=2bb3cbefdb8fd019765b1a9cc42ecf37ff22fec6))
- binutils ([2.41](https://lists.gnu.org/archive/html/info-gnu/2023-07/msg00009.html))
- bpftool ([6.5.7](https://kernelnewbies.org/Linux_6.5#Tracing.2C_perf_and_BPF))
- c-ares ([1.21.0](https://c-ares.org/changelog.html#1_21_0))
- ca-certificates ([3.97](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_97.html))
- containerd ([1.7.13](https://github.com/containerd/containerd/releases/tag/v1.7.13) (includes [1.7.11](https://github.com/containerd/containerd/releases/tag/v1.7.11)))
- coreutils ([9.4](https://lists.gnu.org/archive/html/info-gnu/2023-08/msg00007.html))
- curl ([8.5.0](https://curl.se/changes.html#8_5_0))
- docker ([24.0.9](https://github.com/moby/moby/releases/tag/v24.0.9))
- elfutils ([0.190](https://sourceware.org/git/?p=elfutils.git;a=blob;f=NEWS;h=0420d3b8376877c1b11712f1aad90a2e2b6f6d06;hb=c1058da5a450e33e72b72abb53bc3ffd7f6b361b))
- gawk ([5.3.0](https://lwn.net/Articles/949829/))
- gentoolkit ([0.6.3](https://gitweb.gentoo.org/proj/gentoolkit.git/log/?h=gentoolkit-0.6.3))
- gettext ([0.22.4](https://savannah.gnu.org/news/?id=10544))
- glib ([2.78.3](https://gitlab.gnome.org/GNOME/glib/-/blob/2.78.3/NEWS))
- gnutls ([3.8.2](https://lists.gnupg.org/pipermail/gnutls-help/2023-November/004837.html))
- groff ([1.23.0](https://lists.gnu.org/archive/html/info-gnu/2023-07/msg00001.html))
- hwdata ([0.376](https://github.com/vcrhonek/hwdata/commits/v0.376))
- intel-microcode ([20231114_p20231114](https://github.com/intel/Intel-Linux-Processor-Microcode-Data-Files/releases/tag/microcode-20231114))
- iproute2 ([6.6.0](https://marc.info/?l=linux-netdev&m=169929000929786&w=2))
- ipset ([7.19](https://git.netfilter.org/ipset/tree/ChangeLog?id=ce6db35a0ea950e850ebe7c50ce46908c1c3bb2b))
- jq ([1.7.1](https://github.com/jqlang/jq/releases/tag/jq-1.7.1) (includes [1.7](https://github.com/jqlang/jq/releases/tag/jq-1.7)))
- kbd ([2.6.4](https://github.com/legionus/kbd/releases/tag/v2.6.4))
- kmod ([31](https://github.com/kmod-project/kmod/blob/v31/NEWS))
- libarchive ([3.7.2](https://github.com/libarchive/libarchive/releases/tag/v3.7.2))
- libdnet ([1.16.4](https://github.com/ofalk/libdnet/releases/tag/libdnet-1.16.4))
- libksba ([1.6.5](https://git.gnupg.org/cgi-bin/gitweb.cgi?p=libksba.git;a=blob;f=NEWS;h=369cfb5d91bf232685a6c5b156453a624e11ed67;hb=7b3e4785e54280d1a13c5bc839bdc6722d898ac7))
- libnsl ([2.0.1](https://github.com/thkukuk/libnsl/releases/tag/v2.0.1))
- libxslt ([1.1.39](https://gitlab.gnome.org/GNOME/libxslt/-/releases/v1.1.39))
- lsof ([4.99.0](https://github.com/lsof-org/lsof/blob/4.99.0/00DIST#L5523))
- lz4 ([1.9.4](https://github.com/lz4/lz4/releases/tag/v1.9.4))
- openssh ([9.6p1](https://www.openssh.com/releasenotes.html#9.6p1))
- openssl ([3.0.12](https://github.com/openssl/openssl/blob/openssl-3.0.12/NEWS.md#major-changes-between-openssl-3011-and-openssl-3012-24-oct-2023))
- readline ([8.2_p7](https://git.savannah.gnu.org/cgit/readline.git/log/?id=bfe9c573a9e376323929c80b2b71c59727fab0cc))
- runc ([1.1.12](https://github.com/opencontainers/runc/releases/tag/v1.1.12))
- selinux-base ([2.20231002](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20231002))
- selinux-base-policy ([2.20231002](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20231002))
- selinux-container ([2.20231002](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20231002))
- selinux-dbus ([2.20231002](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20231002))
- selinux-sssd ([2.20231002](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20231002))
- selinux-unconfined ([2.20231002](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20231002))
- sqlite ([3.44.2](https://www.sqlite.org/releaselog/3_44_2.html))
- strace ([6.6](https://github.com/strace/strace/releases/tag/v6.6))
- traceroute ([2.1.3](https://sourceforge.net/projects/traceroute/files/traceroute/traceroute-2.1.3/))
- usbutils ([016](https://git.kernel.org/pub/scm/linux/kernel/git/gregkh/usbutils.git/tree/NEWS?h=v016))
- util-linux ([2.39.2](https://github.com/util-linux/util-linux/blob/v2.39.2/Documentation/releases/v2.39.2-ReleaseNotes))
- vim ([9.0.2092](https://github.com/vim/vim/commits/v9.0.2092/))
- whois ([5.5.20](https://github.com/rfc1036/whois/blob/v5.5.20/debian/changelog))
- xmlsec ([1.3.2](https://github.com/lsh123/xmlsec/releases/tag/xmlsec_1_3_2))
- xz-utils ([5.4.5](https://github.com/tukaani-project/xz/releases/tag/v5.4.5))
- zlib ([1.3](https://github.com/madler/zlib/releases/tag/v1.3))
- SDK: perl ([5.38.2](https://perldoc.perl.org/5.38.2/perldelta))
- SDK: portage ([3.0.59](https://gitweb.gentoo.org/proj/portage.git/tree/NEWS?h=portage-3.0.59))
- SDK: python ([3.11.7](https://www.python.org/downloads/release/python-3117/))
- SDK: repo (2.37)
- SDK: Rust ([1.75.0](https://github.com/rust-lang/rust/releases/tag/1.75.0) (includes [1.74.1](https://github.com/rust-lang/rust/releases/tag/1.74.1)))

 
 _Changes since **Alpha 3850.0.0**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-46838](https://nvd.nist.gov/vuln/detail/CVE-2023-46838), [CVE-2023-50431](https://nvd.nist.gov/vuln/detail/CVE-2023-50431), [CVE-2023-6610](https://nvd.nist.gov/vuln/detail/CVE-2023-6610), [CVE-2023-6915](https://nvd.nist.gov/vuln/detail/CVE-2023-6915), [CVE-2024-1085](https://nvd.nist.gov/vuln/detail/CVE-2024-1085), [CVE-2024-1086](https://nvd.nist.gov/vuln/detail/CVE-2024-1086), [CVE-2024-23849](https://nvd.nist.gov/vuln/detail/CVE-2024-23849))
 - docker ([CVE-2024-24557](https://nvd.nist.gov/vuln/detail/CVE-2024-24557))
 - runc ([CVE-2024-21626](https://nvd.nist.gov/vuln/detail/CVE-2024-21626))
 
 #### Bug fixes:
 
 - Added a workaround for old airgapped/proxied update-engine clients to be able to update to this release ([Flatcar#1332](https://github.com/flatcar/Flatcar/issues/1332), [update_engine#38](https://github.com/flatcar/update_engine/pull/38))
 - Fixed the handling of OEM update payloads in a Nebraska response with self-hosted packages ([ue-rs#49](https://github.com/flatcar/ue-rs/pull/49))
 - Forwarded the proxy environment variables of `update-engine.service` to the postinstall script to support fetching OEM systemd-sysext payloads through a proxy ([Flatcar#1326](https://github.com/flatcar/Flatcar/issues/1326))
 
 #### Changes:
 
 - Added a `flatcar-update --oem-payloads <yes|no>` flag to skip providing OEM payloads, e.g., for downgrades ([init#114](https://github.com/flatcar/init/pull/114))
 
 #### Updates:
 
 - Linux ([6.6.16](https://lwn.net/Articles/961011) (includes [6.6.15](https://lwn.net/Articles/960441), [6.6.14](https://lwn.net/Articles/959512), [6.6.13](https://lwn.net/Articles/958862)))
 - ca-certificates ([3.97](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_97.html))
 - containerd ([1.7.13](https://github.com/containerd/containerd/releases/tag/v1.7.13))
 - docker ([24.0.9](https://github.com/moby/moby/releases/tag/v24.0.9))
 - runc ([1.1.12](https://github.com/opencontainers/runc/releases/tag/v1.1.12))
# Changelog for flatcar_3815.1.0_beta
 _Changes since **Beta 3760.1.1**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-1193](https://nvd.nist.gov/vuln/detail/CVE-2023-1193), [CVE-2023-51779](https://nvd.nist.gov/vuln/detail/CVE-2023-51779), [CVE-2023-51780](https://nvd.nist.gov/vuln/detail/CVE-2023-51780), [CVE-2023-51781](https://nvd.nist.gov/vuln/detail/CVE-2023-51781), [CVE-2023-51782](https://nvd.nist.gov/vuln/detail/CVE-2023-51782), [CVE-2023-6531](https://nvd.nist.gov/vuln/detail/CVE-2023-6531), [CVE-2023-6606](https://nvd.nist.gov/vuln/detail/CVE-2023-6606), [CVE-2023-6622](https://nvd.nist.gov/vuln/detail/CVE-2023-6622), [CVE-2023-6817](https://nvd.nist.gov/vuln/detail/CVE-2023-6817), [CVE-2023-6931](https://nvd.nist.gov/vuln/detail/CVE-2023-6931))
 - Go ([CVE-2023-39326](https://nvd.nist.gov/vuln/detail/CVE-2023-39326), [CVE-2023-45285](https://nvd.nist.gov/vuln/detail/CVE-2023-45285))
 - VMWare: open-vm-tools ([CVE-2023-34058](https://nvd.nist.gov/vuln/detail/CVE-2023-34058), [CVE-2023-34059](https://nvd.nist.gov/vuln/detail/CVE-2023-34059))
 - nghttp2 ([CVE-2023-44487](https://nvd.nist.gov/vuln/detail/CVE-2023-44487))
 - samba ([CVE-2023-4091](https://nvd.nist.gov/vuln/detail/CVE-2023-4091))
 - zlib ([CVE-2023-45853](https://nvd.nist.gov/vuln/detail/CVE-2023-45853))
 
 #### Bug fixes:
 
 - AWS: Fixed the Amazon SSM agent that was crashing. ([Flatcar#1307](https://github.com/flatcar/Flatcar/issues/1307))
 - Fixed a bug resulting in coreos-cloudinit resetting the instance hostname to 'localhost' if no metadata could be found ([coreos-cloudinit#25](https://github.com/flatcar/coreos-cloudinit/pull/25), [Flatcar#1262](https://github.com/flatcar/Flatcar/issues/1262)), with contributions from [MichaelEischer](https://github.com/MichaelEischer)
 - Fixed supplying extension update payloads with a custom base URL in Nebraska ([Flatcar#1281](https://github.com/flatcar/Flatcar/issues/1281))
 - Set TTY used for fetching server_context to RAW mode before running cloudinit on cloudsigma ([scripts#1280](https://github.com/flatcar/scripts/pull/1280))
 
 #### Changes:
 
 - **Torcx, the mechanism to provide a custom Docker version, was replaced by systemd-sysext in the OS image**. Learn more about sysext and how to customise OS images [here](https://www.flatcar.org/docs/latest/provisioning/sysext/) and read the blogpost about the replacement [here](https://www.flatcar.org/blog/2023/12/extending-flatcar-say-goodbye-to-torcx-and-hello-to-systemd-sysext/).
   - Torcx entered deprecation 2 years ago in favour of [deploying plain Docker binaries](https://www.flatcar.org/docs/latest/container-runtimes/use-a-custom-docker-or-containerd-version/)
    (which is now also a legacy option because systemd-sysext offers a more robust and better structured way of customisation, including OS independent updates).
   - Torcx has been removed entirely; if you use Torcx to extend the Flatcar base OS image, please refer to our [conversion script](https://www.flatcar.org/docs/latest/provisioning/sysext/#torcx-deprecation) and to the sysext documentation mentioned above for migrating.
   - Consequently, `update_engine` will not perform torcx sanity checks post-update anymore.
   - Relevant changes: [scripts#1216](https://github.com/flatcar/scripts/pull/1216), [update_engine#30](https://github.com/flatcar/update_engine/pull/30), [Mantle#466](https://github.com/flatcar/mantle/pull/466), [Mantle#465](https://github.com/flatcar/mantle/pull/465).
- cri-tools, runc, containerd, docker, and docker-cli are now built from Gentoo upstream ebuilds. Docker received a major version upgrade - it was updated to Docker 24 (from Docker 20; see "updates").
  - **NOTE:** The docker btrfs storage driver has been de-prioritised; BTRFS backed storage will now default to the `overlay2` driver
    ([changelog](https://docs.docker.com/engine/release-notes/23.0/#bug-fixes-and-enhancements-6), [upstream pr](https://github.com/moby/moby/pull/42661)).
    Using the btrfs driver can still be enforced by creating a respective [docker config](https://docs.docker.com/storage/storagedriver/btrfs-driver/#configure-docker-to-use-the-btrfs-storage-driver) at `/etc/docker/daemon.json`.
  - **NOTE:** If you are already using btrfs-backed Docker storage and are upgrading to this new version, Docker will automatically use the `btrfs` storage driver for backwards-compatibility with your deployment.
    - **Docker will remove the `btrfs` driver entirely in a future version. Please consider migrating your deployments to the `overlay2` driver.**
 - GCP OEM images now use a systemd-sysext image for layering additional platform-specific software on top of `/usr` and being part of the OEM A/B updates ([flatcar#1146](https://github.com/flatcar/Flatcar/issues/1146)) 
 
 #### Updates:
 
 - Azure: WALinuxAgent ([v2.9.1.1](https://github.com/Azure/WALinuxAgent/releases/tag/v2.9.1.1))
 - DEV, AZURE: python ([3.11.6](https://docs.python.org/release/3.11.6/whatsnew/changelog.html#python-3-11-6))
 - DEV: iperf ([3.15](https://github.com/esnet/iperf/releases/tag/3.15))
 - DEV: smartmontools ([7.4](https://www.smartmontools.org/browser/tags/RELEASE_7_4/smartmontools/NEWS))
 - Go ([1.20.12](https://go.dev/doc/devel/release#go1.20.12) (includes [1.20.11](https://go.dev/doc/devel/release#go1.20.11)))
 - Linux ([6.1.73](https://lwn.net/Articles/958343) (includes [6.1.72](https://lwn.net/Articles/957376), [6.1.71](https://lwn.net/Articles/957009), [6.1.70](https://lwn.net/Articles/956526), [6.1.69](https://lwn.net/Articles/955814), [6.1.68](https://lwn.net/Articles/954989/), [6.1.67](https://lwn.net/Articles/954455), [6.1.60](https://lwn.net/Articles/948817) and [6.1.59](https://lwn.net/Articles/948297)))
 - Linux Firmware ([20231111](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tag/?h=20231111) (includes [20231030](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tag/?h=20231030)))
 - SDK: Rust ([1.73.0](https://github.com/rust-lang/rust/releases/tag/1.73.0))
 - SDK: python packaging ([23.2](https://github.com/pypa/packaging/releases/tag/23.2)), platformdirs ([3.11.0](https://github.com/platformdirs/platformdirs/releases/tag/3.11.0)) 
 - VMWare: open-vm-tools ([12.3.5](https://github.com/vmware/open-vm-tools/releases/tag/stable-12.3.5))
 - acpid ([2.0.34](https://sourceforge.net/p/acpid2/code/ci/2.0.34/tree/Changelog))
 - ca-certificates ([3.96.1](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_96_1.html) (includes [3.96](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_96.html)))
 - containerd ([1.7.10](https://github.com/containerd/containerd/releases/tag/v1.7.10) includes ([1.7.9](https://github.com/containerd/containerd/releases/tag/v1.7.9) and [1.7.8](https://github.com/containerd/containerd/releases/tag/v1.7.8)))
 - cri-tools ([1.27.0](https://github.com/kubernetes-sigs/cri-tools/releases/tag/v1.27.0))
 - ding-libs ([0.6.2](https://github.com/SSSD/ding-libs/releases/tag/0.6.2))
 - docker ([24.0.6](https://docs.docker.com/engine/release-notes/24.0/), includes changes from [23.0](https://docs.docker.com/engine/release-notes/23.0/))
 - efibootmgr ([18](https://github.com/rhboot/efibootmgr/releases/tag/18))
 - efivar ([38](https://github.com/rhboot/efivar/releases/tag/38))
 - ethtool ([6.5](https://git.kernel.org/pub/scm/network/ethtool/ethtool.git/tree/NEWS?h=v6.5))
 - hwdata ([0.375](https://github.com/vcrhonek/hwdata/releases/tag/v0.375) includes ([0.374](https://github.com/vcrhonek/hwdata/commits/v0.374)))
 - iproute2 ([6.5.0](https://marc.info/?l=linux-netdev&m=169401822317373&w=2))
 - ipvsadm ([1.31](https://git.kernel.org/pub/scm/utils/kernel/ipvsadm/ipvsadm.git/tag/?h=v1.31) (includes [1.28](https://git.kernel.org/pub/scm/utils/kernel/ipvsadm/ipvsadm.git/tag/?h=v1.28), [1.29](https://git.kernel.org/pub/scm/utils/kernel/ipvsadm/ipvsadm.git/tag/?h=v1.29) and [1.30](https://git.kernel.org/pub/scm/utils/kernel/ipvsadm/ipvsadm.git/tag/?h=v1.30)))
 - json-c ([0.17](https://github.com/json-c/json-c/blob/json-c-0.17-20230812/ChangeLog))
 - libffi ([3.4.4](https://github.com/libffi/libffi/releases/tag/v3.4.4) (includes [3.4.2](https://github.com/libffi/libffi/releases/tag/v3.4.2) and [3.4.3](https://github.com/libffi/libffi/releases/tag/v3.4.3)))
 - liblinear (246)
 - libmnl ([1.0.5](https://git.netfilter.org/libmnl/log/?h=libmnl-1.0.5))
 - libnetfilter_conntrack ([1.0.9](https://git.netfilter.org/libnetfilter_conntrack/log/?h=libnetfilter_conntrack-1.0.9))
 - libnetfilter_cthelper ([1.0.1](https://git.netfilter.org/libnetfilter_cthelper/log/?id=8cee0347cc6969c39bb64000dfaa676a8f9e30f0))
 - libnetfilter_cttimeout ([1.0.1](https://git.netfilter.org/libnetfilter_cttimeout/log/?id=068d36d6291f53a0a609ab1f695aa06e94ce3d30))
 - libnfnetlink ([1.0.2](https://git.netfilter.org/libnfnetlink/log/?h=libnfnetlink-1.0.2))
 - libsodium ([1.0.19](https://github.com/jedisct1/libsodium/releases/tag/1.0.19-RELEASE))
 - libunistring ([1.1](https://git.savannah.gnu.org/gitweb/?p=libunistring.git;a=blob;f=NEWS;h=5a43ddd7011d62a952733f6c0b7ad52aa4f385c7;hb=8006860b710aae2e8442088c3ddc7d819dfa8ac7))
 - libunwind ([1.7.2](https://github.com/libunwind/libunwind/releases/tag/v1.7.2) (includes [1.7.0](https://github.com/libunwind/libunwind/releases/tag/v1.7.0)))
 - liburing ([2.3](https://github.com/axboe/liburing/blob/liburing-2.3/CHANGELOG))
 - mpc ([1.3.1](https://sympa.inria.fr/sympa/arc/mpc-discuss/2022-12/msg00049.html) (includes [1.3.0](https://sympa.inria.fr/sympa/arc/mpc-discuss/2022-12/msg00028.html))
 - mpfr ([4.2.1](https://gitlab.inria.fr/mpfr/mpfr/-/blob/4.2.1/NEWS))
 - nghttp2 ([1.57.0](https://github.com/nghttp2/nghttp2/releases/tag/v1.57.0) (includes [1.52.0](https://github.com/nghttp2/nghttp2/releases/tag/v1.57.0), [1.53.0](https://github.com/nghttp2/nghttp2/releases/tag/v1.53.0), [1.54.0](https://github.com/nghttp2/nghttp2/releases/tag/v1.54.0), [1.55.0](https://github.com/nghttp2/nghttp2/releases/tag/v1.55.0), [1.55.1](https://github.com/nghttp2/nghttp2/releases/tag/v1.55.1) and [1.56.0](https://github.com/nghttp2/nghttp2/releases/tag/v1.56.0)))
 - nspr ([4.35](https://hg.mozilla.org/projects/nspr/log/b563bfc16c887c48b038b7b441fcc4e40a126d3b))
 - ntp ([4.2.8p17](https://www.ntp.org/support/securitynotice/4_2_8p17-release-announcement/))
 - nvme-cli ([v2.6](https://github.com/linux-nvme/nvme-cli/releases/tag/v2.6), libnvme [v1.6](https://github.com/linux-nvme/libnvme/releases/tag/v1.6))
 - protobuf ([21.12](https://github.com/protocolbuffers/protobuf/releases/tag/v21.12) (includes [21.10](https://github.com/protocolbuffers/protobuf/releases/tag/v21.10) and [21.11](https://github.com/protocolbuffers/protobuf/releases/tag/v21.11)))
 - samba ([4.18.8](https://www.samba.org/samba/history/samba-4.18.8.html))
 - sqlite ([3.43.2](https://www.sqlite.org/releaselog/3_43_2.html))
 - squashfs-tools ([4.6.1](https://github.com/plougher/squashfs-tools/releases/tag/4.6.1) (includes [4.6](https://github.com/plougher/squashfs-tools/releases/tag/4.6)))
 - thin-provisioning-tools ([1.0.6](https://github.com/jthornber/thin-provisioning-tools/blob/v1.0.6/CHANGES))

 _Changes since **Alpha 3815.0.0**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-1193](https://nvd.nist.gov/vuln/detail/CVE-2023-1193), [CVE-2023-51779](https://nvd.nist.gov/vuln/detail/CVE-2023-51779), [CVE-2023-51780](https://nvd.nist.gov/vuln/detail/CVE-2023-51780), [CVE-2023-51781](https://nvd.nist.gov/vuln/detail/CVE-2023-51781), [CVE-2023-51782](https://nvd.nist.gov/vuln/detail/CVE-2023-51782), [CVE-2023-6531](https://nvd.nist.gov/vuln/detail/CVE-2023-6531), [CVE-2023-6606](https://nvd.nist.gov/vuln/detail/CVE-2023-6606), [CVE-2023-6622](https://nvd.nist.gov/vuln/detail/CVE-2023-6622), [CVE-2023-6817](https://nvd.nist.gov/vuln/detail/CVE-2023-6817), [CVE-2023-6931](https://nvd.nist.gov/vuln/detail/CVE-2023-6931))
 
 #### Bug fixes:
 
 - AWS: Fixed the Amazon SSM agent that was crashing. ([Flatcar#1307](https://github.com/flatcar/Flatcar/issues/1307))
 - Fixed a bug resulting in coreos-cloudinit resetting the instance hostname to 'localhost' if no metadata could be found ([coreos-cloudinit#25](https://github.com/flatcar/coreos-cloudinit/pull/25), [Flatcar#1262](https://github.com/flatcar/Flatcar/issues/1262)), with contributions from [MichaelEischer](https://github.com/MichaelEischer)
 - Fixed supplying extension update payloads with a custom base URL in Nebraska ([Flatcar#1281](https://github.com/flatcar/Flatcar/issues/1281))

  
 #### Updates:
 
 - Linux ([6.1.73](https://lwn.net/Articles/958343) (includes [6.1.72](https://lwn.net/Articles/957376), [6.1.71](https://lwn.net/Articles/957009), [6.1.70](https://lwn.net/Articles/956526), [6.1.69](https://lwn.net/Articles/955814), [6.1.68](https://lwn.net/Articles/954989/) and [6.1.67](https://lwn.net/Articles/954455)))
 - ca-certificates ([3.96.1](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_96_1.html) (includes [3.96](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_96.html)))# Changelog for flatcar_3760.1.1_beta
 _Changes since **Beta 3760.1.0**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-6121](https://nvd.nist.gov/vuln/detail/CVE-2023-6121))
 
 #### Bug fixes:
 
 - Deleted files in `/etc` that have a tmpfiles rule that normally would recreate them will now show up again through the `/etc` lowerdir ([Flatcar#1265](https://github.com/flatcar/Flatcar/issues/1265), [bootengine#79](https://github.com/flatcar/bootengine/pull/79))
 - Fixed the missing `/etc/extensions/` symlinks for the inbuilt Docker/containerd systemd-sysext images on update from Beta 3760.1.0 ([update_engine#32](https://github.com/flatcar/update_engine/pull/32))
 - GCP: Fixed OS Login enabling ([scripts#1445](https://github.com/flatcar/scripts/pull/1445))
 
 #### Changes:
 
 - linux kernel: added zstd support for squashfs kernel module ([scripts#1297](https://github.com/flatcar/scripts/pull/1297))
 
 #### Updates:
 
 - Linux ([6.1.66](https://lwn.net/Articles/954112) (includes [6.1.65](https://lwn.net/Articles/953648/), [6.1.64](https://lwn.net/Articles/953132), [6.1.63](https://lwn.net/Articles/952003)))
 - afterburn ([5.5.0](https://github.com/coreos/afterburn/releases/tag/v5.5.0))
 - ca-certificates ([3.95](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_95.html))# Changelog for flatcar_3760.1.0_beta
:warning: From Alpha 3794.0.0 Torcx has been removed - please assert that you don't rely on specific Torcx mechanism but now use systemd-sysext. See [here](https://www.flatcar.org/docs/latest/provisioning/sysext/) for more information.

 _Changes since **Beta 3745.1.0**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-35827](https://nvd.nist.gov/vuln/detail/CVE-2023-35827), [CVE-2023-46813](https://nvd.nist.gov/vuln/detail/CVE-2023-46813), [CVE-2023-46862](https://nvd.nist.gov/vuln/detail/CVE-2023-46862), [CVE-2023-5178](https://nvd.nist.gov/vuln/detail/CVE-2023-5178), [CVE-2023-5717](https://nvd.nist.gov/vuln/detail/CVE-2023-5717))
 - curl ([CVE-2023-38545](https://nvd.nist.gov/vuln/detail/CVE-2023-38545), [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546))
 - glibc ([CVE-2023-4911](https://nvd.nist.gov/vuln/detail/CVE-2023-4911))
 - go ([CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325), [CVE-2023-39325](https://nvd.nist.gov/vuln/detail/CVE-2023-39325))
 - grub ([CVE-2023-4692](https://nvd.nist.gov/vuln/detail/CVE-2023-4692), [CVE-2023-4693](https://nvd.nist.gov/vuln/detail/CVE-2023-4693))
 - libtirpc ([libtirpc-rhbg-2138317](http://git.linux-nfs.org/?p=steved/libtirpc.git;a=commit;h=4a2d85c64110ee9e21a8c4f9dafd6b0ae621506d), [libtirpc-rhbg-2150611](http://git.linux-nfs.org/?p=steved/libtirpc.git;a=commit;h=f7f0abdf267698de3f74a0285405b1b01f40893b), [libtirpc-rhbg-2224666](http://git.linux-nfs.org/?p=steved/libtirpc.git;a=commit;h=1d2e10afb2ffc35cb3623f57a15f712359f18e75))
 
 #### Bug fixes:
 
 - Added AWS EKS support for versions 1.24-1.28. Fixed `/usr/share/amazon/eks/download-kubelet.sh` to include download paths for these versions. ([scripts#1210](https://github.com/flatcar/scripts/pull/1210))
 - Fixed iterating over the OEM update payload signatures which prevented the AWS OEM update to 3745.x.y ([update-engine#31](https://github.com/flatcar/update_engine/pull/31))
 - Fixed quotes handling for update-engine ([Flatcar#1209](https://github.com/flatcar/Flatcar/issues/1209))
 - Made `sshkeys.service` more robust to only run `coreos-metadata-sshkeys@core.service` when not masked and also retry on failure ([init#112](https://github.com/flatcar/init/pull/112))
 
 #### Changes:
 
 - Brightbox: The regular OpenStack image should now be used, it includes Afterburn for instance metadata attributes
 - OpenStack: An uncompressed image is provided for simpler import (since the images use qcow2 inline compression, there is no benefit in using the `.gz` or `.bz2` images)
 
 #### Updates:
 
 - Go ([1.20.10](https://go.dev/doc/devel/release#go1.20.10) (includes [1.20.9](https://go.dev/doc/devel/release#go1.20.9)))
 - Linux ([6.1.62](https://lwn.net/Articles/950700) (includes [6.1.61](https://lwn.net/Articles/949826), [6.1.60](https://lwn.net/Articles/948817) and includes [6.1.59](https://lwn.net/Articles/948299)))
 - containerd ([1.7.7](https://github.com/containerd/containerd/releases/tag/v1.7.7))
 - curl ([8.4.0](https://curl.se/changes.html#8_4_0))
 - libnl ([3.8.0](https://github.com/thom311/libnl/compare/libnl3_7_0...libnl3_8_0))
 - libtirpc ([1.3.4](https://marc.info/?l=linux-nfs&m=169667640909830&w=2))
 - libxml2 ([2.11.5](https://gitlab.gnome.org/GNOME/libxml2/-/releases/v2.11.5))
 - openssh ([9.5p1](https://www.openssh.com/releasenotes.html#9.5p1))
 - pigz ([2.8](https://zlib.net/pipermail/pigz-announce_zlib.net/2023-August/000018.html))
 - strace([6.4](https://github.com/strace/strace/releases/tag/v6.4))
 - whois ([5.5.18](https://github.com/rfc1036/whois/blob/v5.5.18/debian/changelog))
 
 _Changes since **Alpha 3760.0.0**_
 
 #### Security fixes:
 
 - Linux ([CVE-2023-35827](https://nvd.nist.gov/vuln/detail/CVE-2023-35827), [CVE-2023-46813](https://nvd.nist.gov/vuln/detail/CVE-2023-46813), [CVE-2023-46862](https://nvd.nist.gov/vuln/detail/CVE-2023-46862), [CVE-2023-5178](https://nvd.nist.gov/vuln/detail/CVE-2023-5178), [CVE-2023-5717](https://nvd.nist.gov/vuln/detail/CVE-2023-5717))
 
 #### Bug fixes:
 
 - Fixed iterating over the OEM update payload signatures which prevented the AWS OEM update to 3745.x.y ([update-engine#31](https://github.com/flatcar/update_engine/pull/31))
 - Made `sshkeys.service` more robust to only run `coreos-metadata-sshkeys@core.service` when not masked and also retry on failure ([init#112](https://github.com/flatcar/init/pull/112))
 
 #### Changes:
 
 - Brightbox: The regular OpenStack image should now be used, it includes Afterburn for instance metadata attributes
 - OpenStack: An uncompressed image is provided for simpler import (since the images use qcow2 inline compression, there is no benefit in using the `.gz` or `.bz2` images)
 
 #### Updates:
 
 - Linux ([6.1.62](https://lwn.net/Articles/950700) (includes [6.1.61](https://lwn.net/Articles/949826), [6.1.60](https://lwn.net/Articles/948817) and includes [6.1.59](https://lwn.net/Articles/948299)))# Changelog for flatcar_3745.1.0_beta
_Changes since **Beta 3732.1.0**_
 
 #### Security fixes:
 
 - curl ([CVE-2023-38039](https://nvd.nist.gov/vuln/detail/CVE-2023-38039), [CVE-2023-38545](https://nvd.nist.gov/vuln/detail/CVE-2023-38545), [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546))
 - glibc ([CVE-2023-4527](https://nvd.nist.gov/vuln/detail/CVE-2023-4527), [CVE-2023-4806](https://nvd.nist.gov/vuln/detail/CVE-2023-4806))
 - lua ([CVE-2022-33099](https://nvd.nist.gov/vuln/detail/CVE-2022-33099))
 - mit-krb5 ([CVE-2023-36054](https://nvd.nist.gov/vuln/detail/CVE-2023-36054))
 - procps ([CVE-2023-4016](https://nvd.nist.gov/vuln/detail/CVE-2023-4016))
 - samba ([CVE-2021-44142](https://nvd.nist.gov/vuln/detail/CVE-2021-44142), [CVE-2022-1615](https://nvd.nist.gov/vuln/detail/CVE-2022-1615))
 
 #### Bug fixes:
 
 - Disabled systemd-networkd's RoutesToDNS setting by default to fix provisioning failures observed in VMs with multiple network interfaces on Azure ([scripts#1206](https://github.com/flatcar/scripts/pull/1206))
 - Fixed the postinstall hook failure when updating from Azure instances without OEM systemd-sysext images to Flatcar Alpha 3745.x.y ([update_engine#29](https://github.com/flatcar/update_engine/pull/29))
 
 #### Changes:
 
 - AWS OEM images now use a systemd-sysext image for layering additional platform-specific software on top of `/usr`
 - Reworked the VMware OEM software to be shipped as A/B updated systemd-sysext image
 - SDK: Experimental support for [prefix builds](https://github.com/flatcar/scripts/blob/main/PREFIX.md) to create distro independent, portable, self-contained applications w/ all dependencies included. With contributions from [chewi](https://github.com/chewi) and [HappyTobi](https://github.com/HappyTobi).
 - Started shipping default ssh client and ssh daemon configs in `/etc/ssh/ssh_config` and `/etc/ssh/sshd_config` which include config snippets in `/etc/ssh/ssh_config.d` and `/etc/ssh/sshd_config.d`, respectively.
 - The open-vm-tools package in VMware OEM now comes with vmhgfs-fuse, udev rules, pam and vgauth
 - To make Kubernetes work by default, `/usr/libexec/kubernetes/kubelet-plugins/volume/exec` is now a symlink to the writable folder `/var/kubernetes/kubelet-plugins/volume/exec` ([Flatcar#1193](https://github.com/flatcar/Flatcar/issues/1193))
 
 #### Updates:
 
 - Linux ([6.1.58](https://lwn.net/Articles/947820) (includes [6.1.57](https://lwn.net/Articles/947298), [6.1.56](https://lwn.net/Articles/946854)))
 - Linux Firmware ([20230919](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tag/?h=20230919))
 - bind-tools ([9.16.42](https://bind9.readthedocs.io/en/v9.16.42/notes.html#notes-for-bind-9-16-42))
 - ca-certificates ([3.94](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_94.html))
 - checkpolicy ([3.5](https://github.com/SELinuxProject/selinux/releases/tag/3.5))
 - curl ([8.3.0](https://curl.se/changes.html#8_3_0))
 - gcc ([13.2](https://gcc.gnu.org/gcc-13/changes.html))
 - gzip ([1.13](https://savannah.gnu.org/news/?id=10501))
 - libgcrypt ([1.10.2](https://git.gnupg.org/cgi-bin/gitweb.cgi?p=libgcrypt.git;a=blob;f=NEWS;h=c9a239615f8070427a96688b1be40a81e59e9b8a;hb=1c5cbacf3d88dded5063e959ee68678ff7d0fa56))
 - libselinux ([3.5](https://github.com/SELinuxProject/selinux/releases/tag/3.5))
 - libsemanage ([3.5](https://github.com/SELinuxProject/selinux/releases/tag/3.5))
 - libsepol ([3.5](https://github.com/SELinuxProject/selinux/releases/tag/3.5))
 - lua ([5.4.6](https://www.lua.org/manual/5.4/readme.html#changes))
 - mit-krb5 ([1.21.2](http://web.mit.edu/kerberos/krb5-1.21/))
 - openssh ([9.4p1](https://www.openssh.com/releasenotes.html#9.4p1))
 - policycoreutils ([3.5](https://github.com/SELinuxProject/selinux/releases/tag/3.5))
 - procps ([4.0.4](https://gitlab.com/procps-ng/procps/-/releases/v4.0.4) (includes [4.0.3](https://gitlab.com/procps-ng/procps/-/releases/v4.0.3) and [4.0.0](https://gitlab.com/procps-ng/procps/-/releases/v4.0.0)))
 - rpcsvc-proto ([1.4.4](https://github.com/thkukuk/rpcsvc-proto/releases/tag/v1.4.4))
 - samba ([4.18.4](https://wiki.samba.org/index.php/Samba_4.18_Features_added/changed#Samba_4.18.4))
 - selinux-base ([2.20221101](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20221101))
 - selinux-base-policy ([2.20221101](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20221101))
 - selinux-container ([2.20221101](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20221101))
 - selinux-sssd ([2.20221101](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20221101))
 - selinux-unconfined ([2.20221101](https://github.com/SELinuxProject/refpolicy/releases/tag/RELEASE_2_20221101))
 - semodule-utils ([3.5](https://github.com/SELinuxProject/selinux/releases/tag/3.5))
 - SDK: Rust ([1.72.1](https://github.com/rust-lang/rust/releases/tag/1.72.1))
 - VMWARE: libdnet ([1.16.2](https://github.com/ofalk/libdnet/releases/tag/libdnet-1.16.2) (includes [1.16](https://github.com/ofalk/libdnet/releases/tag/libdnet-1.16)))

 _Changes since **Alpha 3745.0.0**_
 
 #### Security fixes:
 
 - curl ([CVE-2023-38545](https://nvd.nist.gov/vuln/detail/CVE-2023-38545), [CVE-2023-38546](https://nvd.nist.gov/vuln/detail/CVE-2023-38546))
 
 #### Bug fixes:
 
 - Disabled systemd-networkd's RoutesToDNS setting by default to fix provisioning failures observed in VMs with multiple network interfaces on Azure ([scripts#1206](https://github.com/flatcar/scripts/pull/1206))
 - Fixed the postinstall hook failure when updating from Azure instances without OEM systemd-sysext images to Flatcar Alpha 3745.x.y ([update_engine#29](https://github.com/flatcar/update_engine/pull/29))
 
 #### Changes:
 
 - To make Kubernetes work by default, `/usr/libexec/kubernetes/kubelet-plugins/volume/exec` is now a symlink to the writable folder `/var/kubernetes/kubelet-plugins/volume/exec` ([Flatcar#1193](https://github.com/flatcar/Flatcar/issues/1193))
 
 #### Updates:
 
 - Linux ([6.1.58](https://lwn.net/Articles/947820) (includes [6.1.57](https://lwn.net/Articles/947298), [6.1.56](https://lwn.net/Articles/946854)))
 - ca-certificates ([3.94](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_94.html))# Changelog for flatcar_3602.1.6_beta
 _Changes since **Beta 3602.1.5**_
 
 #### Changes:
 
 - Azure: Add support for Microsoft Azure Network Adapter (MANA) NICs on Azure ([scripts#1131](https://github.com/flatcar/scripts/pull/1131))
 
 #### Updates:
 
 - Linux ([5.15.132](https://lwn.net/Articles/944877) (includes [5.15.131](https://lwn.net/Articles/943755), [5.15.130](https://lwn.net/Articles/943404)))
 - ca-certificates ([3.93](https://firefox-source-docs.mozilla.org/security/nss/releases/nss_3_93.html))# Changelog for flatcar_3602.1.5_beta
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