# Changelog for talos_v1.6.0_stable
## [Talos 1.6.0](https://github.com/siderolabs/talos/releases/tag/v1.6.0) (2023-12-15)

Welcome to the v1.6.0 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### OAuth2 Machine Config Flow

Talos Linux when running on the `metal` platform can be configured to authenticate the machine configuration download using [OAuth2 device flow](https://www.talos.dev/v1.6/advanced/machine-config-oauth/).


### Network Device Selectors

Previously, [network device selectors](https://www.talos.dev/v1.6/talos-guides/network/device-selector/) only matched the first link, now the configuration is applied to all matching links.


### Extension Services

Talos now starts Extension Services early in the boot process, this allows guest agents to be started in maintenance mode.


### Linux Firmware

Starting with Talos 1.6, there is no Linux firmware included in the initramfs.
Customers who need Linux firmware can pull them as extension during install time using the image factory service.
If the initial boot requires firmware, a custom iso can be built with the firmware included using the image factory service.
This also ensures that the linux-firmware is not tied to a specific Talos version.


### Flannel Configuration

Talos Linux now supports customizing default Flannel manifest with extra arguments for flanneld.

```yaml
cluster:
  network:
    cni:
      flannel:
        extraArgs:
          - --iface-can-reach=192.168.1.1
```


### Ingress Firewall

Talos Linux now supports configuring the [ingress firewall rules](https://talos.dev/v1.6/talos-guides/network/ingress-firewall/).


### Kernel Arguments

Talos and Imager now supports dropping kernel arguments specified in `.machine.install.extraKernelArgs` or as `--extra-kernel-arg` to imager.
Any kernel argument that starts with a `-` is dropped. Kernel arguments to be dropped can be specified either as `-<key>` which would remove all arguments that start with `<key>` or as `-<key>=<value>` which would remove the exact argument.


### Kube-Scheduler Configuration

Talos now supports specifying the kube-scheduler configuration in the Talos configuration file.
It can be set under `cluster.scheduler.config` and kube-scheduler will be automatically configured to with the correct flags.


### Kubelet Credential Provider Configuration

Talos now supports specifying the kubelet credential provider configuration in the Talos configuration file.
It can be set under `machine.kubelet.credentialProviderConfig` and kubelet will be automatically configured to with the correct flags.
The credential binaries are expected to be present under `/usr/local/lib/kubelet/credentialproviders`.
Talos System Extensions can be used to install the credential binaries.


### KubePrism

[KubePrism](https://www.talos.dev/v1.6/kubernetes-guides/configuration/kubeprism/) is enabled by default on port 7445.


### Sysctl

Talos now handles sysctl/sysfs key names in line with sysctl.conf(5):

* if the first separator is '/', no conversion is done
* if the first separator is '.', dots and slashes are remapped

Example (both sysctls are equivalent):

```yaml
machine:
  sysctls:
    net/ipv6/conf/eth0.100/disable_ipv6: "1"
    net.ipv6.conf.eth0/100.disable_ipv6: "1"
```


### talosctl CLI

The command `images` deprecated in Talos 1.5 was removed, please use `talosctl images default` instead.


### Component Updates

Linux: 6.1.67
containerd: 1.7.10
CoreDNS: 1.11.1
Kubernetes: 1.29.0
Flannel: 0.23.0
etcd: 3.5.11
runc: 1.1.10

Talos is built with Go 1.21.5.


### User Disks

Talos Linux now supports specifying user disks in `.machine.disks` machine configuration links via `udev` symlinks, e.g. `/dev/disk/by-id/XXXX`.


### Contributors

* Andrey Smirnov
* Noel Georgi
* Dmitriy Matrenichev
* Oscar Utbult
* Serge Logvinov
* Andrey Smirnov
* Artem Chernyshev
* Utku Ozdemir
* Nico Berlee
* Radosław Piliszek
* Steve Francis
* Thomas Way
* ndbrew
* Andrei Kvapil
* Christian Rolland
* Drew Hess
* Enno Boland
* Florian Berchtold
* Henry Sachs
* Jacob McSwain
* Jacob McSwain
* Jared Davenport
* Mans Matulewicz
* Nebula
* Sascha Desch
* Spencer Smith
* Thomas Lemarchand
* Tim Jones
* Zachary Milonas
* budimanjojo
* guoguangwu
* mikucat0309

### Changes
<details><summary>218 commits</summary>
<p>

* siderolabs/talos@eddd188c9 release(v1.6.0): prepare release
* siderolabs/talos@d42fd10c0 chore: fix the gvisor test
* siderolabs/talos@333c462c5 feat: update Kubernetes to v1.29.0
* siderolabs/talos@61e6df169 fix: leave discovery service later in the reset sequence
* siderolabs/talos@ef15a1f23 feat: provide compatibility for future Talos 1.7
* siderolabs/talos@c155602ca fix: add a KubeSpan option to disable extra endpoint harvesting
* siderolabs/talos@5371eedd6 feat: send `actor id` to the SideroLink events sink
* siderolabs/talos@997f83f1f docs: cap max heading level
* siderolabs/talos@d9db4cf76 feat: update Kubernetes to v1.29.0-rc.2
* siderolabs/talos@d510df5df chore: enable kubespan+firewall for cilium tests
* siderolabs/talos@b61b30056 chore: optimize pcap dump
* siderolabs/talos@007d9f673 feat: update Linux to 6.1.67
* siderolabs/talos@7b7fb367e release(v1.6.0-beta.1): prepare release
* siderolabs/talos@fe6661128 fix: talosctl cluster create not to enforce kubeprism always
* siderolabs/talos@41fc05438 fix: support user disks via symlinks
* siderolabs/talos@1fe7f2840 docs: rework machine config documentation generation
* siderolabs/talos@e45794064 chore: fix the release.toml
* siderolabs/talos@591cfb456 fix: store and execute desired action on emergency action
* siderolabs/talos@fee63ac26 fix: trim leading spaces\newlines in inline manifest contents
* siderolabs/talos@cc16b9689 fix: skip writing the file if the contents haven't changed
* siderolabs/talos@ecee92c90 fix: do not panic in `merge.Merge` if map value is nil
* siderolabs/talos@c2259bff3 feat: update Go 1.21.5, Linux 6.1.65, etcd 3.5.11
* siderolabs/talos@c4dff49b3 release(v1.6.0-beta.0): prepare release
* siderolabs/talos@d8a435f0e fix: initialize boot assets with defaults early
* siderolabs/talos@c6835de17 fix: pick etcd adverised addresses from 'current' addresses
* siderolabs/talos@6b5bc8b85 feat: update Linux to 6.1.64
* siderolabs/talos@e71e3e416 feat: support extra arguments for `flanneld`
* siderolabs/talos@36c8ddb5e feat: implement ingress firewall rules
* siderolabs/talos@0b111ecb8 fix: support slices of enums and fix NfTablesConntrackStateMatch
* siderolabs/talos@9a8521741 feat: improve nftables backend
* siderolabs/talos@db4e2539d feat: update Kubernetes 1.29.0-rc.1 and other bumps
* siderolabs/talos@7a4a92854 feat: support sanitized kernel args
* siderolabs/talos@f041b2629 chore: add tests for mdadm extension
* siderolabs/talos@e46e6a312 feat: implement nftables backend
* siderolabs/talos@ba827bf8b chore: support getting multiple endpoints from the `Provision` rpc call
* siderolabs/talos@dd45dd06c chore: add custom node taints
* siderolabs/talos@8e2307466 docs: fix talosctl pcap argument
* siderolabs/talos@e4a050cb1 docs: fix talosctl inspect dependencies example indentation
* siderolabs/talos@fbcf4264f docs: fix talosctl dashboard cli docs
* siderolabs/talos@70d53ee13 chore: deprecate .persist and .extensions
* siderolabs/talos@95e33f6fc release(v1.6.0-alpha.2): prepare release
* siderolabs/talos@514e514ba feat: update Linux 6.1.63, containerd 1.7.9
* siderolabs/talos@aca8b5e17 fix: ignore kernel command line in container mode
* siderolabs/talos@020a0eb63 docs: fix table formatting for bootstraprequest
* siderolabs/talos@0eb245e04 docs: fix talosctl pcap example indentation
* siderolabs/talos@de6caf534 docs: fix table formatting for machineservice api
* siderolabs/talos@27d208c26 feat: implement OAuth2 device flow for machine config
* siderolabs/talos@5c8fa2a80 chore: start containerd early in boot
* siderolabs/talos@95a252cfc docs: fix link in what is new page
* siderolabs/talos@0d3c3ed71 feat: support kube scheduler config
* siderolabs/talos@06941b7e5 fix: allow rootfs propagation configuration for extension services
* siderolabs/talos@57dc796f3 docs: update lastRelease to v1.5.5 in _index.md
* siderolabs/talos@21d944a64 docs: add timezone information
* siderolabs/talos@4f1ad16c7 feat: support kubelet credentialprovider config
* siderolabs/talos@71a3bf0e3 fix: allow extra kernel args for secureboot installer
* siderolabs/talos@f38eaaab8 feat: rework secureboot and PCR signing key
* siderolabs/talos@6eade3d5e chore: add ability to rewrite uuids and set unique tokens for Talos
* siderolabs/talos@e9c7ac17a fix: set max msg recv size when proxying
* siderolabs/talos@e22ab440d feat: update Linux 6.1.61, containerd 1.7.8, runc 1.1.10
* siderolabs/talos@8245361f9 feat: show first 32 bytes of response body on download error
* siderolabs/talos@75d3987c0 chore: drop sha1 from genereated pcr json
* siderolabs/talos@6f32d2990 feat: add `.der` output `talosctl gen secureboot pcr`
* siderolabs/talos@87c40da6c fix: proper logging in machined on startup
* siderolabs/talos@a54da5f64 fix: image build for nanopi_4s
* siderolabs/talos@6f3cd0593 refactor: update packet capture to use 'afpacket' interface
* siderolabs/talos@813442dd7 fix: don't validate machine.install if installed
* siderolabs/talos@dff60069c feat: update Kubernetes to 1.29.0-alpha.3
* siderolabs/talos@c97db5dfe chore: bump Go dependencies
* siderolabs/talos@807a9950a fix: use custom Talos/kernel version when generating UKI
* siderolabs/talos@eb94468a6 docs: add documentation for Image Factory
* siderolabs/talos@2e78513e1 refactor: drop the dependency link platform -> network ctrl
* siderolabs/talos@6dc776b8a fix: when writing to META in the installer/imager, use fixed name
* siderolabs/talos@3703041e9 chore: remove uneeded code
* siderolabs/talos@cbe6e7622 fix: generate images for SBCs using imager
* siderolabs/talos@5dff164f1 fix: fix error output of cli action tracker
* siderolabs/talos@ef5056122 feat: update etcd to 3.5.10
* siderolabs/talos@45ae80873 chore: bump go-api-signature dependency to v0.3.1
* siderolabs/talos@ffa5e05cb fix: make Talos work on Rockpi 4c boards again
* siderolabs/talos@8eba4c599 feat: generate secrets bundle from the machine config
* siderolabs/talos@c7de745f6 chore: drop deprecated code
* siderolabs/talos@cc0c3ab69 docs: update rpi_generic.md
* siderolabs/talos@a009f5c60 fix: accept sysctl paths with dots
* siderolabs/talos@4919f6ee2 feat: add GOMEMLIMIT to shipped manifests with memory limits
* siderolabs/talos@73ee576ea chore: update sonobuouy library, drop the fork
* siderolabs/talos@c23bc2f4a chore: support OCI layout as a source for profile input
* siderolabs/talos@154bbd70f docs: fix talos version in guide for docker
* siderolabs/talos@11d1f6163 release(v1.6.0-alpha.1): prepare release
* siderolabs/talos@9dfae8467 chore: update dependencies
* siderolabs/talos@38ce3c827 feat: nocloud prefer mac address
* siderolabs/talos@401e89411 feat: customize image size
* siderolabs/talos@865f08f86 docs: kubeadm migration guide improvements
* siderolabs/talos@c3e418200 refactor: use COSI runtime with new controller runtime DB
* siderolabs/talos@c1ee24465 feat: update Kubernetes to v1.29.0-alpha.2
* siderolabs/talos@0ff7350ab fix: oracle integration fixes
* siderolabs/talos@675bada45 test: add config generation stability tests
* siderolabs/talos@f9639fb53 test: fix 'talosctl gen' tests
* siderolabs/talos@6142d87a0 feat: hostname configuration improvements on the NoCloud platform
* siderolabs/talos@7bb205ebe fix: don't use runtime-specs Mount struct in machine config
* siderolabs/talos@d1b27926c feat: update Go to 1.21.3
* siderolabs/talos@b87092ab6 fix: handle secure boot state policy pcr digest error
* siderolabs/talos@498aeb8c3 docs: fix incorrect image suffix
* siderolabs/talos@c14a5d4f7 feat: support service account auth in cli
* siderolabs/talos@336aee0fd fix: use tpm2 hash algorithm constants and allow non-SHA-256 PCRs
* siderolabs/talos@69d8054c9 chore: drop UpdateEndpointSuite
* siderolabs/talos@ef7be16c8 fix: clear the encryption config in META when STATE is reset
* siderolabs/talos@5fc60d2ca feat: add Solarflare SFC9000 support
* siderolabs/talos@9b5cfdd0b chore: add tests for iscsi
* siderolabs/talos@b897764f8 docs: update proxmox.md
* siderolabs/talos@159f45bde docs: fix typos in CLI calls to endpoints
* siderolabs/talos@0bd1bdd74 chore: allow insecure access to installer base image (imager)
* siderolabs/talos@10ed13067 fix: the node IP for kubelet shouldn't change if nothing matches
* siderolabs/talos@e7575ecaa feat: support n-5 latest Kubernetes versions
* siderolabs/talos@e71508ec1 chore: update dependencies
* siderolabs/talos@6d7fa4668 docs: add metal network configuration guide
* siderolabs/talos@2b548ad0d feat: update containerd to 1.7.x
* siderolabs/talos@62dcfe81e fix: update kubernetes library to support 1.29 upgrades
* siderolabs/talos@52caf0763 feat: update Kubernetes to 1.29.0-alpha.1
* siderolabs/talos@390137447 feat: enable KubePrism by default
* siderolabs/talos@1beb5e86e docs: add KubePrism video
* siderolabs/talos@a52d3cda3 chore: update gen and COSI runtime
* siderolabs/talos@29b201d61 feat: enable common h/w sensors
* siderolabs/talos@9c2ba7c6f chore: add tests for chelsio drivers
* siderolabs/talos@5ca4d58dc fix: generate of modules.dep when on the machine
* siderolabs/talos@5efcccb6b chore: bump kernel to 6.1.54
* siderolabs/talos@29c767a02 docs: add control plane nodes as users of apid also for control plane nodes
* siderolabs/talos@4874cfb95 chore: fix typo
* siderolabs/talos@96f2a62ea test: update upgrade tests versions
* siderolabs/talos@f3a370acb feat: update Flannel to 0.22.3
* siderolabs/talos@efdee6965 feat: update Kubernetes to 1.28.2
* siderolabs/talos@e3b494058 fix: build CPU ucode correctly for early loader
* siderolabs/talos@c5bd0ac5c refactor: reimplement the depmod extension rebuilder
* siderolabs/talos@0b883f52a docs: add notes about stable addressing
* siderolabs/talos@3ef670a9e chore: pull in dm modules
* siderolabs/talos@8f4a36b0d docs: update aws to add command to allow KubeSpan wireguard port
* siderolabs/talos@a7edd0523 fix: set default route priority for hcloud platform
* siderolabs/talos@87c1b3ddd fix: calculate UKI ISO size dynamically
* siderolabs/talos@9698e4547 fix: handle correctly change of listen address for maintenance service
* siderolabs/talos@a096f05a5 chore: update gRPC library and enable shared write buffers
* siderolabs/talos@9e78fecca chore: improve image signing process
* siderolabs/talos@f00567e20 chore: add PKG_KERNEL arg to customize used kernel
* siderolabs/talos@2960f93ba feat: add readonly information to the disks API response
* siderolabs/talos@735bf9ed0 feat: bring in Google vNIC driver
* siderolabs/talos@3f5232075 feat: upgrade-k8s without comments
* siderolabs/talos@e44875106 docs: update deploying-cilium.md
* siderolabs/talos@7046cae43 chore: update gopacket to reduce init memory allocs
* siderolabs/talos@da73b563d chore: update Go to 1.21.1
* siderolabs/talos@5e11f08a6 fix: trim file path in the container image
* siderolabs/talos@3d2dad4e6 chore: show securtiystate on dashboard
* siderolabs/talos@b48510874 chore: e2e-aws cleanup
* siderolabs/talos@1eebbce35 chore: add output flag for talosctl config info
* siderolabs/talos@3fbed806c chore: add tests for util-linux extensions
* siderolabs/talos@7c514a1a6 docs: update header links
* siderolabs/talos@6058c3602 fix: shorten VLAN link names to fit into the limit of 15 characters
* siderolabs/talos@9c2f765c8 fix: allow network device selector to match multiple links
* siderolabs/talos@a04b98637 fix: update kubernetes library for 1.28 upgrade pre-checks
* siderolabs/talos@f7473e477 feat: update default Kubernetes to 1.28.1
* siderolabs/talos@d693604a1 chore: fix default image list in the release notes
* siderolabs/talos@d91b5b3a3 feat: set environment variables early in the boot
* siderolabs/talos@c918c0855 fix: set correct (1 year) talosconfig expiration
* siderolabs/talos@79bbdf454 fix: set proper timeouts for KubePrism loadbalancer
* siderolabs/talos@b8fb55d5c fix: use a mount prefix when installing a bootloader
* siderolabs/talos@44f59a804 feat: improve imager APIs
* siderolabs/talos@2d3ac925e refactor: update NTP spike detector
* siderolabs/talos@af0cc70e3 test: update e2e-aws to use worker groups
* siderolabs/talos@d03dc7a8a chore: validate new system extensions
* siderolabs/talos@bbeb489aa chore: drop firmware from initramfs
* siderolabs/talos@3c9f7a7de chore: re-enable nolintlint and typecheck linters
* siderolabs/talos@c51e2c9b4 feat: update CoreDNS to 1.11.1
* siderolabs/talos@8670450d2 release(v1.6.0-alpha.0): prepare release
* siderolabs/talos@6778ded29 feat: add e2e-aws for nvidia extensions
* siderolabs/talos@74c07ed71 chore: update Go to 1.21
* siderolabs/talos@a28d72e9c fix: ova contents to be named `disk.*`
* siderolabs/talos@c0ea4d7ba fix: properly calculate overal of node address with subnet filters
* siderolabs/talos@d6b2719e2 chore: drone: move extensions step to a function
* siderolabs/talos@9608ef56d chore: allow bridge traffic with DHCP broadcast traffic
* siderolabs/talos@c99316457 docs: fix the installing system extensions doc
* siderolabs/talos@833895940 chore: add tests for zfs extension
* siderolabs/talos@cb468c41c fix: copy proper modules to arm64 squashfs
* siderolabs/talos@ea0d6e8c6 fix: prevent dashboard crashes when process info is not available
* siderolabs/talos@e9077a6fb feat: filter the hostname to produce nodename
* siderolabs/talos@dc8361c1d fix: properly GC images supplied with both tag and digest
* siderolabs/talos@ccfa8de11 fix: automatically change `rpi_4` board on upgrade
* siderolabs/talos@b56e8b7d9 fix: support 'List' type manifests
* siderolabs/talos@574d48e54 fix: use image digest when starting a container
* siderolabs/talos@175747cea fix: ntp query error with bare IPv6 address
* siderolabs/talos@c8b507fb2 docs: fix kubeprism typo
* siderolabs/talos@0cdcb2e0e docs: restructure docs for nvidia drivers for v1.4
* siderolabs/talos@676db9768 docs: fork docs for Talos 1.6
* siderolabs/talos@92ad18c18 fix: write correct capacity to the ovf
* siderolabs/talos@6b0373ebe chore: move bash tests to integration
* siderolabs/talos@52b3d8d37 docs: make Talos 1.5 documentation the default one
* siderolabs/talos@dc873df9b chore: fix the filenames of openstack images
* siderolabs/talos@b5c0e7b24 docs: update nvidia docs
* siderolabs/talos@9606e871e docs: update Jiva Pod Security Policy
* siderolabs/talos@a86ed4362 chore: update Kubernetes Go modules to 0.28.0
* siderolabs/talos@97b4e3e91 feat: update Kubernetes to 1.28.0
* siderolabs/talos@79ca1a3df feat: e2e-aws using tf code
* siderolabs/talos@bf3a5e011 chore: add version compatibility for Talos 1.6
* siderolabs/talos@969e8097c feat: update Kubernetes to 1.28.0-rc.1
* siderolabs/talos@ca41b611e chore: drone jsonnet cleanup
* siderolabs/talos@bc198e98e docs: retain cilium autoMount pending upstream hostPath fix
* siderolabs/talos@86c94eff8 refactor: docgen and config examples
* siderolabs/talos@ee6d639f6 fix: match routes on the priority properly
* siderolabs/talos@bff0d8f32 chore: fix dependencies in the release pipeline
* siderolabs/talos@e1b288679 refactor: compile regex in validation method on the first use
* siderolabs/talos@daa4c185a docs: add what's new and documentation for Talos 1.5
* siderolabs/talos@c4a1ca8d6 chore: remove <-errCh where possible in grpc methods
* siderolabs/talos@e0f383598 chore: clean up the output of the `imager`
* siderolabs/talos@fb536af4d chore: optimize memory usage of `tcell` library on init
* siderolabs/talos@7c86a365e chore: publish systemd-boot and systemd-stub assets
* siderolabs/talos@7d688ccfe fix: make encryption config provider default to `luks2` if not set
* siderolabs/talos@80238a05a chore: unify semver under `github.com/blang/semver/v4`
* siderolabs/talos@0f1920bdd chore: provide a resource to peek into Linux clock adjustments
* siderolabs/talos@4eab3017b fix: calculate log2i properly
* siderolabs/talos@bcf284530 fix: update providerid prefix for aws
* siderolabs/talos@ac2aff5cc fix: fix azure portion of cloud uploader
* siderolabs/talos@793dcedc9 fix: fast-wipe the system disk on talosctl reset
* siderolabs/talos@76fa45afb docs: update cilium instructions
</p>
</details>

### Changes since v1.6.0-beta.1
<details><summary>12 commits</summary>
<p>

* siderolabs/talos@eddd188c9 release(v1.6.0): prepare release
* siderolabs/talos@d42fd10c0 chore: fix the gvisor test
* siderolabs/talos@333c462c5 feat: update Kubernetes to v1.29.0
* siderolabs/talos@61e6df169 fix: leave discovery service later in the reset sequence
* siderolabs/talos@ef15a1f23 feat: provide compatibility for future Talos 1.7
* siderolabs/talos@c155602ca fix: add a KubeSpan option to disable extra endpoint harvesting
* siderolabs/talos@5371eedd6 feat: send `actor id` to the SideroLink events sink
* siderolabs/talos@997f83f1f docs: cap max heading level
* siderolabs/talos@d9db4cf76 feat: update Kubernetes to v1.29.0-rc.2
* siderolabs/talos@d510df5df chore: enable kubespan+firewall for cilium tests
* siderolabs/talos@b61b30056 chore: optimize pcap dump
* siderolabs/talos@007d9f673 feat: update Linux to 6.1.67
</p>
</details>

### Changes from siderolabs/extras
<details><summary>9 commits</summary>
<p>

* siderolabs/extras@113887a chore: update Go to 1.21.5
* siderolabs/extras@8bffd15 feat: bump dependencies
* siderolabs/extras@e8e801b feat: update Go to 1.21.4
* siderolabs/extras@d816a02 chore: move project to using kres
* siderolabs/extras@3893789 chore: move to github workflows
* siderolabs/extras@6d48418 feat: update Go to 1.21.3
* siderolabs/extras@09d7c3e chore: update releases
* siderolabs/extras@a011245 feat: update Go to 1.21.1
* siderolabs/extras@d3f54c7 feat: update Go to 1.20.8
</p>
</details>

### Changes from siderolabs/gen
<details><summary>2 commits</summary>
<p>

* siderolabs/gen@efca710 chore: add `FilterInPlace` method to maps and update module
* siderolabs/gen@36a3ae3 feat: update module
</p>
</details>

### Changes from siderolabs/go-blockdevice
<details><summary>3 commits</summary>
<p>

* siderolabs/go-blockdevice@d9313ea fix: define softraid partition
* siderolabs/go-blockdevice@a75c4cc chore: rekres
* siderolabs/go-blockdevice@8a2102a feat: luks resize
</p>
</details>

### Changes from siderolabs/go-kubernetes
<details><summary>7 commits</summary>
<p>

* siderolabs/go-kubernetes@fa05430 chore: support kube-scheduler config version
* siderolabs/go-kubernetes@68bf392 feat: add dropped API resource for 1.29
* siderolabs/go-kubernetes@09fa006 fix: retry Windows connection errors
* siderolabs/go-kubernetes@3aa47a4 feat: support Kubernetes 1.29 upgrades
* siderolabs/go-kubernetes@ae33a4a feat: introduce support for Kubernetes version compatibility checks
* siderolabs/go-kubernetes@cf2754e chore: update to use GHA
* siderolabs/go-kubernetes@44e26b3 feat: update removed feature gates for 1.28
</p>
</details>

### Changes from siderolabs/go-procfs
<details><summary>2 commits</summary>
<p>

* siderolabs/go-procfs@9f72b22 feat: support removing kernel args
* siderolabs/go-procfs@4b4a6ff chore: rekres
</p>
</details>

### Changes from siderolabs/go-retry
<details><summary>1 commit</summary>
<p>

* siderolabs/go-retry@23b6fc2 fix: provider modern error unwrapping
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>40 commits</summary>
<p>

* siderolabs/pkgs@3ae2450 chore: rekres to fix 'failed' build on merge
* siderolabs/pkgs@1e2a377 feat: update Linux to 6.1.67
* siderolabs/pkgs@617d342 fix: revert: update grub to fix loading large initramfs
* siderolabs/pkgs@364d295 feat: update Go to 1.21.5
* siderolabs/pkgs@841c63d feat: update zfs to 2.1.14
* siderolabs/pkgs@a084b9f feat: bump depenendencies
* siderolabs/pkgs@e61c784 feat: bump dependencies
* siderolabs/pkgs@70919d8 fix: update grub to fix loading large initramfs
* siderolabs/pkgs@3aea711 feat: bump dependencies
* siderolabs/pkgs@d59cb3e feat(lvm2): configure thin support
* siderolabs/pkgs@252a59f feat: bump dependencies
* siderolabs/pkgs@0bb2a79 feat: update Go to 1.21.4
* siderolabs/pkgs@f57b0a9 chore: fix kernel target to honor `PLATFORM`
* siderolabs/pkgs@5f84302 chore: move to using kres
* siderolabs/pkgs@d7509f1 chore: bump deps
* siderolabs/pkgs@3a66437 chore: add gh workflows
* siderolabs/pkgs@2e892fd feat: update versions
* siderolabs/pkgs@37348d6 feat: update Go to 1.21.3
* siderolabs/pkgs@34f3c41 feat: add Solarflare SFC9000 support
* siderolabs/pkgs@0c84090 feat: update releases
* siderolabs/pkgs@19cdf71 feat: enable common sensors
* siderolabs/pkgs@acee18e chore: bump kernel to 6.1.54
* siderolabs/pkgs@1d16fd2 feat: add Chelsio support
* siderolabs/pkgs@4504f83 chore: rename kconfig-hardened-check
* siderolabs/pkgs@847a9c3 chore: enable dm thin provisioning
* siderolabs/pkgs@1401505 chore: drop `-pkgs` for upstream kernel modules
* siderolabs/pkgs@a62471d feat: add binfmt_misc support
* siderolabs/pkgs@518c441 feat: add gVNIC support
* siderolabs/pkgs@7d9e60e feat: update Go to 1.21.1
* siderolabs/pkgs@d3d7d29 chore: bump deps
* siderolabs/pkgs@3b70656 chore: fix cacert perms
* siderolabs/pkgs@cca80b7 feat: update Linux to 6.1.46
* siderolabs/pkgs@2e1c0b9 fix: nonfree kmod pkg name
* siderolabs/pkgs@cff5beb feat: add btrfs support
* siderolabs/pkgs@7717b7e chore: bump deps
* siderolabs/pkgs@2f19f18 feat: update containerd to 1.6.23
* siderolabs/pkgs@30d4b74 feat: update Go to 1.21
* siderolabs/pkgs@eda123d feat: update runc to 1.1.9
* siderolabs/pkgs@30cd584 chore: enable pushing of non-free packages
* siderolabs/pkgs@fb247b5 chore: update kernel and microcode
</p>
</details>

### Changes from siderolabs/siderolink
<details><summary>7 commits</summary>
<p>

* siderolabs/siderolink@be3b095 feat: add support for event's actor ID
* siderolabs/siderolink@9304096 chore: allow to specify several endpoints
* siderolabs/siderolink@5ab8f9d feat: allow persistent keepalive to be set for the peer
* siderolabs/siderolink@71dd308 chore: provide unique_token and Talos version in ProvisionRequest
* siderolabs/siderolink@0ee5425 chore: revert sys moduel to 0.13.0
* siderolabs/siderolink@6be9ba7 chore: bump deps
* siderolabs/siderolink@448cbe1 chore: bump `golang.org/x/net` to 0.8.0
</p>
</details>

### Changes from siderolabs/tools
<details><summary>15 commits</summary>
<p>

* siderolabs/tools@336d248 feat: update Go to 1.21.5
* siderolabs/tools@b707a3a feat: bump dependencies
* siderolabs/tools@ff7fe96 feat: update Go to 1.21.4
* siderolabs/tools@6216d64 fix: org name
* siderolabs/tools@4334b92 chore: move to using kres
* siderolabs/tools@024ef25 chore: bump deps
* siderolabs/tools@5a22409 chore: refactor github actions
* siderolabs/tools@9a05d12 feat: move to gh workflow
* siderolabs/tools@a4a52e2 chore: add dummy gh workflow
* siderolabs/tools@9c09b00 feat: update dependencies
* siderolabs/tools@35948af feat: update Go to 1.21.3
* siderolabs/tools@09023c1 feat: update OpenSSL to 3.1.3
* siderolabs/tools@7fa8bb5 feat: update releases
* siderolabs/tools@fa388de feat: update Go to 1.21.1
* siderolabs/tools@33fb4b3 feat: update Go to 1.21
</p>
</details>

### Dependency Changes

* **github.com/Azure/azure-sdk-for-go/sdk/azcore**                            v1.9.0 **_new_**
* **github.com/Azure/azure-sdk-for-go/sdk/azidentity**                        v1.4.0 **_new_**
* **github.com/Azure/azure-sdk-for-go/sdk/security/keyvault/azcertificates**  v1.0.0 **_new_**
* **github.com/Azure/azure-sdk-for-go/sdk/security/keyvault/azkeys**          v1.0.1 **_new_**
* **github.com/Azure/azure-sdk-for-go/sdk/security/keyvault/azsecrets**       v1.0.1 **_new_**
* **github.com/aws/aws-sdk-go-v2/config**                                     v1.18.32 -> v1.25.6
* **github.com/aws/aws-sdk-go-v2/feature/ec2/imds**                           v1.13.7 -> v1.14.5
* **github.com/aws/smithy-go**                                                v1.14.0 -> v1.17.0
* **github.com/beevik/ntp**                                                   v1.2.0 -> v1.3.0
* **github.com/blang/semver/v4**                                              v4.0.0 **_new_**
* **github.com/containerd/cgroups/v3**                                        v3.0.2 **_new_**
* **github.com/containerd/containerd**                                        v1.6.23 -> v1.7.9
* **github.com/cosi-project/runtime**                                         v0.3.1 -> v0.3.19
* **github.com/distribution/reference**                                       v0.5.0 **_new_**
* **github.com/docker/docker**                                                v24.0.5 -> v24.0.7
* **github.com/fatih/color**                                                  v1.15.0 -> v1.16.0
* **github.com/foxboron/go-uefi**                                             32187aa193d0 -> 18b9ba9cd4c3
* **github.com/fsnotify/fsnotify**                                            v1.6.0 -> v1.7.0
* **github.com/google/go-cmp**                                                v0.5.9 -> v0.6.0
* **github.com/google/go-containerregistry**                                  v0.15.2 -> v0.16.1
* **github.com/google/uuid**                                                  v1.3.0 -> v1.4.0
* **github.com/gopacket/gopacket**                                            v1.1.1 -> v1.2.0
* **github.com/hetznercloud/hcloud-go/v2**                                    v2.0.0 -> v2.4.0
* **github.com/insomniacslk/dhcp**                                            0f9eb93a696c -> b0416c0f187a
* **github.com/jsimonetti/rtnetlink**                                         v1.3.4 -> v1.4.0
* **github.com/mattn/go-isatty**                                              v0.0.19 -> v0.0.20
* **github.com/mdp/qrterminal/v3**                                            v3.2.0 **_new_**
* **github.com/opencontainers/runtime-spec**                                  1c3f411f0417 -> v1.1.0-rc.1
* **github.com/pin/tftp/v3**                                                  v3.1.0 **_new_**
* **github.com/prometheus/procfs**                                            v0.11.1 -> v0.12.0
* **github.com/rivo/tview**                                                   6cc0565babaf -> 33a1d271f2b6
* **github.com/scaleway/scaleway-sdk-go**                                     v1.0.0-beta.20 -> v1.0.0-beta.21
* **github.com/siderolabs/extras**                                            v1.5.0 -> v1.6.0-1-g113887a
* **github.com/siderolabs/gen**                                               v0.4.5 -> v0.4.7
* **github.com/siderolabs/go-blockdevice**                                    v0.4.6 -> v0.4.7
* **github.com/siderolabs/go-kubernetes**                                     v0.2.2 -> v0.2.8
* **github.com/siderolabs/go-procfs**                                         v0.1.1 -> v0.1.2
* **github.com/siderolabs/go-retry**                                          v0.3.2 -> v0.3.3
* **github.com/siderolabs/pkgs**                                              v1.5.0-6-g2f2c9cd -> v1.6.0-5-g3ae2450
* **github.com/siderolabs/siderolink**                                        v0.3.1 -> v0.3.4
* **github.com/siderolabs/talos/pkg/machinery**                               v1.5.0 -> v1.6.0
* **github.com/siderolabs/tools**                                             v1.5.0 -> v1.6.0-1-g336d248
* **github.com/spf13/cobra**                                                  v1.7.0 -> v1.8.0
* **github.com/vmware-tanzu/sonobuoy**                                        v0.56.17 -> v0.57.1
* **go.etcd.io/etcd/api/v3**                                                  v3.5.9 -> v3.5.11
* **go.etcd.io/etcd/client/pkg/v3**                                           v3.5.9 -> v3.5.11
* **go.etcd.io/etcd/client/v3**                                               v3.5.9 -> v3.5.11
* **go.etcd.io/etcd/etcdutl/v3**                                              v3.5.9 -> v3.5.11
* **go.uber.org/zap**                                                         v1.25.0 -> v1.26.0
* **go4.org/netipx**                                                          ec4c8b891b28 -> 6213f710f925
* **golang.org/x/net**                                                        v0.13.0 -> v0.19.0
* **golang.org/x/oauth2**                                                     v0.15.0 **_new_**
* **golang.org/x/sync**                                                       v0.3.0 -> v0.5.0
* **golang.org/x/sys**                                                        v0.10.0 -> v0.15.0
* **golang.org/x/term**                                                       v0.10.0 -> v0.15.0
* **golang.org/x/text**                                                       v0.11.0 -> v0.14.0
* **golang.org/x/time**                                                       v0.3.0 -> v0.5.0
* **google.golang.org/grpc**                                                  v1.57.0 -> v1.59.0
* **k8s.io/api**                                                              v0.28.0 -> v0.29.0
* **k8s.io/apimachinery**                                                     v0.28.0 -> v0.29.0
* **k8s.io/apiserver**                                                        v0.28.0 -> v0.29.0
* **k8s.io/client-go**                                                        v0.28.0 -> v0.29.0
* **k8s.io/component-base**                                                   v0.28.0 -> v0.29.0
* **k8s.io/cri-api**                                                          v0.28.0 -> v0.29.0
* **k8s.io/klog/v2**                                                          v2.100.1 -> v2.110.1
* **k8s.io/kube-scheduler**                                                   v0.29.0 **_new_**
* **k8s.io/kubectl**                                                          v0.28.0 -> v0.29.0
* **k8s.io/kubelet**                                                          v0.28.0 -> v0.29.0
* **sigs.k8s.io/yaml**                                                        v1.3.0 -> v1.4.0

Previous release can be found at [v1.5.0](https://github.com/siderolabs/talos/releases/tag/v1.5.0)

## Images

```
ghcr.io/siderolabs/flannel:v0.23.0
ghcr.io/siderolabs/install-cni:v1.6.0-1-g113887a
registry.k8s.io/coredns/coredns:v1.11.1
gcr.io/etcd-development/etcd:v3.5.11
registry.k8s.io/kube-apiserver:v1.29.0
registry.k8s.io/kube-controller-manager:v1.29.0
registry.k8s.io/kube-scheduler:v1.29.0
registry.k8s.io/kube-proxy:v1.29.0
ghcr.io/siderolabs/kubelet:v1.29.0
ghcr.io/siderolabs/installer:v1.6.0
registry.k8s.io/pause:3.8
```

# Changelog for talos_v1.5.5_stable
## [Talos 1.5.5](https://github.com/siderolabs/talos/releases/tag/v1.5.5) (2023-11-09)

Welcome to the v1.5.5 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

Linux: 6.1.61
Kubernetes: 1.28.3
etcd: 3.5.10

Talos is built with Go 1.20.11.


### Contributors

* Andrey Smirnov
* Utku Ozdemir
* Artem Chernyshev

### Changes
<details><summary>9 commits</summary>
<p>

* siderolabs/talos@ad7361c72 release(v1.5.5): prepare release
* siderolabs/talos@5f70f05e9 fix: don't validate machine.install if installed
* siderolabs/talos@0b18d7403 fix: when writing to META in the installer/imager, use fixed name
* siderolabs/talos@6be1e5836 fix: fix error output of cli action tracker
* siderolabs/talos@059823c4b feat: update etcd to 3.5.10
* siderolabs/talos@8c503f0df chore: bump go-api-signature dependency to v0.3.1
* siderolabs/talos@61413ed11 fix: make Talos work on Rockpi 4c boards again
* siderolabs/talos@6fd9a71b3 feat: update Go 1.20.11, Linux 6.1.61, Kubernetes 1.28.3
* siderolabs/talos@9fe31bd42 fix: update gRPC library to 1.57.2
</p>
</details>

### Changes from siderolabs/extras
<details><summary>1 commit</summary>
<p>

* siderolabs/extras@b43c4e4 feat: update Go to 1.20.11
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>2 commits</summary>
<p>

* siderolabs/pkgs@ab5b0e5 feat: update Linux to 6.1.61
* siderolabs/pkgs@cd687eb feat: update Go to 1.20.11
</p>
</details>

### Changes from siderolabs/tools
<details><summary>1 commit</summary>
<p>

* siderolabs/tools@c95372c feat: update Go to 1.20.11
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/extras**               v1.5.0-2-g6241ac7 -> v1.5.0-3-gb43c4e4
* **github.com/siderolabs/pkgs**                 v1.5.0-13-g45cf9b0 -> v1.5.0-15-gab5b0e5
* **github.com/siderolabs/talos/pkg/machinery**  v1.5.4 -> v1.5.5
* **github.com/siderolabs/tools**                v1.5.0-2-g8adf637 -> v1.5.0-3-gc95372c
* **go.etcd.io/etcd/api/v3**                     v3.5.9 -> v3.5.10
* **go.etcd.io/etcd/client/pkg/v3**              v3.5.9 -> v3.5.10
* **go.etcd.io/etcd/client/v3**                  v3.5.9 -> v3.5.10
* **go.etcd.io/etcd/etcdutl/v3**                 v3.5.9 -> v3.5.10
* **google.golang.org/grpc**                     v1.57.1 -> v1.58.3
* **k8s.io/api**                                 v0.28.2 -> v0.28.3
* **k8s.io/apimachinery**                        v0.28.2 -> v0.28.3
* **k8s.io/apiserver**                           v0.28.2 -> v0.28.3
* **k8s.io/client-go**                           v0.28.2 -> v0.28.3
* **k8s.io/component-base**                      v0.28.2 -> v0.28.3
* **k8s.io/cri-api**                             v0.28.2 -> v0.28.3
* **k8s.io/kubectl**                             v0.28.2 -> v0.28.3
* **k8s.io/kubelet**                             v0.28.2 -> v0.28.3

Previous release can be found at [v1.5.4](https://github.com/siderolabs/talos/releases/tag/v1.5.4)

## Images

```
ghcr.io/siderolabs/flannel:v0.22.1
ghcr.io/siderolabs/install-cni:v1.5.0-3-gb43c4e4
registry.k8s.io/coredns/coredns:v1.10.1
gcr.io/etcd-development/etcd:v3.5.10
registry.k8s.io/kube-apiserver:v1.28.3
registry.k8s.io/kube-controller-manager:v1.28.3
registry.k8s.io/kube-scheduler:v1.28.3
registry.k8s.io/kube-proxy:v1.28.3
ghcr.io/siderolabs/kubelet:v1.28.3
ghcr.io/siderolabs/installer:v1.5.5
registry.k8s.io/pause:3.6
```

# Changelog for talos_v1.5.4_stable
## [Talos 1.5.4](https://github.com/siderolabs/talos/releases/tag/v1.5.4) (2023-10-17)

Welcome to the v1.5.4 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

Linux: 6.1.58

Talos is built with Go 1.21.3.


### Contributors

* Andrey Smirnov
* Thomas Way
* Utku Ozdemir

### Changes
<details><summary>9 commits</summary>
<p>

* siderolabs/talos@9cf7980e5 release(v1.5.4): prepare release
* siderolabs/talos@b72abb613 test: fix 'talosctl gen' tests
* siderolabs/talos@69f1ea283 fix: handle secure boot state policy pcr digest error
* siderolabs/talos@738092fda fix: use tpm2 hash algorithm constants and allow non-SHA-256 PCRs
* siderolabs/talos@21d874a8a fix: clear the encryption config in META when STATE is reset
* siderolabs/talos@58b16b9dc feat: support service account auth in cli
* siderolabs/talos@124c2ff13 fix: the node IP for kubelet shouldn't change if nothing matches
* siderolabs/talos@8f8392595 feat: update Linux to 6.1.58
* siderolabs/talos@db4c5ce99 feat: update Go to 1.20.10
</p>
</details>

### Changes from siderolabs/extras
<details><summary>1 commit</summary>
<p>

* siderolabs/extras@6241ac7 feat: update Go to 1.20.10
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>2 commits</summary>
<p>

* siderolabs/pkgs@45cf9b0 feat: update Linux to 6.1.58
* siderolabs/pkgs@873830b feat: update Go to 1.20.10
</p>
</details>

### Changes from siderolabs/tools
<details><summary>1 commit</summary>
<p>

* siderolabs/tools@8adf637 feat: update Go to 1.20.10
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/extras**               v1.5.0-1-g9d5f16f -> v1.5.0-2-g6241ac7
* **github.com/siderolabs/pkgs**                 v1.5.0-11-gd6d7236 -> v1.5.0-13-g45cf9b0
* **github.com/siderolabs/talos/pkg/machinery**  v1.5.3 -> v1.5.4
* **github.com/siderolabs/tools**                v1.5.0-1-g4d58a1b -> v1.5.0-2-g8adf637
* **golang.org/x/net**                           v0.13.0 -> v0.17.0
* **golang.org/x/sys**                           v0.10.0 -> v0.13.0
* **golang.org/x/term**                          v0.10.0 -> v0.13.0
* **golang.org/x/text**                          v0.11.0 -> v0.13.0
* **google.golang.org/grpc**                     v1.57.0 -> v1.57.1

Previous release can be found at [v1.5.3](https://github.com/siderolabs/talos/releases/tag/v1.5.3)

## Images

```
ghcr.io/siderolabs/flannel:v0.22.1
ghcr.io/siderolabs/install-cni:v1.5.0-2-g6241ac7
registry.k8s.io/coredns/coredns:v1.10.1
gcr.io/etcd-development/etcd:v3.5.9
registry.k8s.io/kube-apiserver:v1.28.2
registry.k8s.io/kube-controller-manager:v1.28.2
registry.k8s.io/kube-scheduler:v1.28.2
registry.k8s.io/kube-proxy:v1.28.2
ghcr.io/siderolabs/kubelet:v1.28.2
ghcr.io/siderolabs/installer:v1.5.4
registry.k8s.io/pause:3.6
```

# Changelog for talos_v1.5.3_stable
## [Talos 1.5.3](https://github.com/siderolabs/talos/releases/tag/v1.5.3) (2023-09-22)

Welcome to the v1.5.3 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### cgroups v1

Talos Linux is incompatible with cgroups v1 due to the Kubernetes issue
https://github.com/kubernetes/kubernetes/issues/120813 and new version of Linux kernel.

Talos Linux doesn't use cgroups v1 by default, and it has to be explicitly enabled with
a kernel argument: `talos.unified_cgroup_hierarchy=0`, so if you are not using cgroups v1,
you are not affected.


### Component Updates

Kubernetes: v1.28.2
Linux: 6.1.54


### Contributors

* Andrey Smirnov
* Noel Georgi

### Changes
<details><summary>11 commits</summary>
<p>

* siderolabs/talos@cb21c6710 release(v1.5.3): prepare release
* siderolabs/talos@c4c33fb9e feat: update Linux to 6.1.54
* siderolabs/talos@88c97678c feat: update Kubernetes to 1.28.2
* siderolabs/talos@721b69b40 fix: generate of modules.dep when on the machine
* siderolabs/talos@802aedd21 fix: build CPU ucode correctly for early loader
* siderolabs/talos@1a1472033 refactor: reimplement the depmod extension rebuilder
* siderolabs/talos@6e27fe3a6 fix: calculate UKI ISO size dynamically
* siderolabs/talos@43d4afc92 fix: set default route priority for hcloud platform
* siderolabs/talos@63a4257a9 fix: handle correctly change of listen address for maintenance service
* siderolabs/talos@e9c9dc50d chore: improve image signing process
* siderolabs/talos@2e13558ac fix: trim file path in the container image
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>2 commits</summary>
<p>

* siderolabs/pkgs@d6d7236 chore: bump kernel to 6.1.54
* siderolabs/pkgs@9bfb39a chore: rename kconfig-hardened-check
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/pkgs**                 v1.5.0-9-g7f9d6eb -> v1.5.0-11-gd6d7236
* **github.com/siderolabs/talos/pkg/machinery**  v1.5.2 -> v1.5.3
* **k8s.io/api**                                 v0.28.1 -> v0.28.2
* **k8s.io/apimachinery**                        v0.28.1 -> v0.28.2
* **k8s.io/apiserver**                           v0.28.1 -> v0.28.2
* **k8s.io/client-go**                           v0.28.1 -> v0.28.2
* **k8s.io/component-base**                      v0.28.1 -> v0.28.2
* **k8s.io/cri-api**                             v0.28.1 -> v0.28.2
* **k8s.io/kubectl**                             v0.28.1 -> v0.28.2
* **k8s.io/kubelet**                             v0.28.1 -> v0.28.2

Previous release can be found at [v1.5.2](https://github.com/siderolabs/talos/releases/tag/v1.5.2)

## Images

```
ghcr.io/siderolabs/flannel:v0.22.1
ghcr.io/siderolabs/install-cni:v1.5.0-1-g9d5f16f
registry.k8s.io/coredns/coredns:v1.10.1
gcr.io/etcd-development/etcd:v3.5.9
registry.k8s.io/kube-apiserver:v1.28.2
registry.k8s.io/kube-controller-manager:v1.28.2
registry.k8s.io/kube-scheduler:v1.28.2
registry.k8s.io/kube-proxy:v1.28.2
ghcr.io/siderolabs/kubelet:v1.28.2
ghcr.io/siderolabs/installer:v1.5.3
registry.k8s.io/pause:3.6
```

# Changelog for talos_v1.5.2_stable
## [Talos 1.5.2](https://github.com/siderolabs/talos/releases/tag/v1.5.2) (2023-09-07)

Welcome to the v1.5.2 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

Kubernetes: v1.28.1
Linux: 6.1.51

Talos is now built with Go 1.20.8.


### Contributors

* Andrey Smirnov

### Changes
<details><summary>12 commits</summary>
<p>

* siderolabs/talos@318c66b98 release(v1.5.2): prepare release
* siderolabs/talos@614e4e892 feat: update Go to 1.20.8
* siderolabs/talos@cb8eb9da1 feat: update Linux to 6.1.51
* siderolabs/talos@45c88aedd fix: update kubernetes library for 1.28 upgrade pre-checks
* siderolabs/talos@b8bd8ee43 fix: shorten VLAN link names to fit into the limit of 15 characters
* siderolabs/talos@2a2b64eee feat: update default Kubernetes to 1.28.1
* siderolabs/talos@e713043ff feat: set environment variables early in the boot
* siderolabs/talos@4552014b9 fix: set correct (1 year) talosconfig expiration
* siderolabs/talos@1804906c7 fix: set proper timeouts for KubePrism loadbalancer
* siderolabs/talos@dbfbeb7c9 refactor: update NTP spike detector
* siderolabs/talos@6ae5b1289 fix: ova contents to be named `disk.*`
* siderolabs/talos@9d6d580f4 fix: properly calculate overal of node address with subnet filters
</p>
</details>

### Changes from siderolabs/extras
<details><summary>1 commit</summary>
<p>

* siderolabs/extras@9d5f16f feat: update Go to 1.20.8
</p>
</details>

### Changes from siderolabs/go-kubernetes
<details><summary>1 commit</summary>
<p>

* siderolabs/go-kubernetes@44e26b3 feat: update removed feature gates for 1.28
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>2 commits</summary>
<p>

* siderolabs/pkgs@7f9d6eb feat: update Go to 1.20.8
* siderolabs/pkgs@99b6ac1 feat: update Linux to 6.1.51
</p>
</details>

### Changes from siderolabs/tools
<details><summary>1 commit</summary>
<p>

* siderolabs/tools@4d58a1b feat: update Go to 1.20.8
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/extras**               v1.5.0 -> v1.5.0-1-g9d5f16f
* **github.com/siderolabs/go-kubernetes**        v0.2.2 -> v0.2.3
* **github.com/siderolabs/pkgs**                 v1.5.0-7-gf62fa2c -> v1.5.0-9-g7f9d6eb
* **github.com/siderolabs/talos/pkg/machinery**  v1.5.1 -> v1.5.2
* **github.com/siderolabs/tools**                v1.5.0 -> v1.5.0-1-g4d58a1b
* **k8s.io/api**                                 v0.28.0 -> v0.28.1
* **k8s.io/apiserver**                           v0.28.0 -> v0.28.1
* **k8s.io/client-go**                           v0.28.0 -> v0.28.1
* **k8s.io/component-base**                      v0.28.0 -> v0.28.1
* **k8s.io/kubectl**                             v0.28.0 -> v0.28.1
* **k8s.io/kubelet**                             v0.28.0 -> v0.28.1

Previous release can be found at [v1.5.1](https://github.com/siderolabs/talos/releases/tag/v1.5.1)

## Images

```
ghcr.io/siderolabs/flannel:v0.22.1
ghcr.io/siderolabs/install-cni:v1.5.0-1-g9d5f16f
registry.k8s.io/coredns/coredns:v1.10.1
gcr.io/etcd-development/etcd:v3.5.9
registry.k8s.io/kube-apiserver:v1.28.1
registry.k8s.io/kube-controller-manager:v1.28.1
registry.k8s.io/kube-scheduler:v1.28.1
registry.k8s.io/kube-proxy:v1.28.1
ghcr.io/siderolabs/kubelet:v1.28.1
ghcr.io/siderolabs/installer:v1.5.2
registry.k8s.io/pause:3.6
```

# Changelog for talos_v1.5.1_stable
## [Talos 1.5.1](https://github.com/siderolabs/talos/releases/tag/v1.5.1) (2023-08-22)

Welcome to the v1.5.1 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

* Linux: 6.1.46


### Contributors

* Andrey Smirnov
* Utku Ozdemir

### Changes
<details><summary>11 commits</summary>
<p>

* siderolabs/talos@40a22cdf7 release(v1.5.1): prepare release
* siderolabs/talos@4fd4e16c0 fix: copy proper modules to arm64 squashfs
* siderolabs/talos@51c92e48a feat: update Linux to 6.1.46
* siderolabs/talos@2d2b8c895 fix: prevent dashboard crashes when process info is not available
* siderolabs/talos@a79ed5e47 fix: properly GC images supplied with both tag and digest
* siderolabs/talos@024053a5c fix: automatically change `rpi_4` board on upgrade
* siderolabs/talos@5c82445d2 fix: support 'List' type manifests
* siderolabs/talos@7b36ada79 fix: use image digest when starting a container
* siderolabs/talos@106078295 fix: ntp query error with bare IPv6 address
* siderolabs/talos@5b1d021d5 fix: write correct capacity to the ovf
* siderolabs/talos@3c8b0856b fix: restore compatibility with Kubernetes 1.26
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>1 commit</summary>
<p>

* siderolabs/pkgs@f62fa2c feat: update Linux to 6.1.46
</p>
</details>

### Dependency Changes

* **github.com/beevik/ntp**                      v1.2.0 -> v1.3.0
* **github.com/siderolabs/pkgs**                 v1.5.0-6-g2f2c9cd -> v1.5.0-7-gf62fa2c
* **github.com/siderolabs/talos/pkg/machinery**  v1.5.0 -> v1.5.1

Previous release can be found at [v1.5.0](https://github.com/siderolabs/talos/releases/tag/v1.5.0)

## Images

```
ghcr.io/siderolabs/flannel:v0.22.1
ghcr.io/siderolabs/install-cni:v1.5.0
registry.k8s.io/coredns/coredns:v1.10.1
gcr.io/etcd-development/etcd:v3.5.9
registry.k8s.io/kube-apiserver:v1.28.0
registry.k8s.io/kube-controller-manager:v1.28.0
registry.k8s.io/kube-scheduler:v1.28.0
registry.k8s.io/kube-proxy:v1.28.0
ghcr.io/siderolabs/kubelet:v1.28.0
ghcr.io/siderolabs/installer:v1.5.1
registry.k8s.io/pause:3.6
```

# Changelog for talos_v1.4.8_stable
## [Talos 1.4.8](https://github.com/siderolabs/talos/releases/tag/v1.4.8) (2023-08-10)

Welcome to the v1.4.8 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

Linux: 6.1.44

Talos is built with Go 1.20.7.


### Contributors

* Andrey Smirnov
* Andrey Smirnov

### Changes
<details><summary>3 commits</summary>
<p>

* siderolabs/talos@84c2961ab release(v1.4.8): prepare release
* siderolabs/talos@371586180 chore: update Go to 1.20.7, Linux to 6.1.44
* siderolabs/talos@85b5d1ddd fix: calculate log2i properly
</p>
</details>

### Changes from siderolabs/extras
<details><summary>1 commit</summary>
<p>

* siderolabs/extras@9b41398 chore: update go to 1.20.7
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>3 commits</summary>
<p>

* siderolabs/pkgs@13103d6 chore: update Go to 1.20.7
* siderolabs/pkgs@782d769 feat: update Linux to 6.1.44
* siderolabs/pkgs@11860e5 chore: enable pushing of non-free packages
</p>
</details>

### Changes from siderolabs/tools
<details><summary>1 commit</summary>
<p>

* siderolabs/tools@6889ef6 feat: update Go to 1.20.7
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/extras**               v1.4.0-3-g2b5a1e6 -> v1.4.0-4-g9b41398
* **github.com/siderolabs/pkgs**                 v1.4.1-16-g69266d9 -> v1.4.1-19-g13103d6
* **github.com/siderolabs/talos/pkg/machinery**  v1.4.7 -> v1.4.8
* **github.com/siderolabs/tools**                v1.4.0-4-g78b2dc6 -> v1.4.0-5-g6889ef6

Previous release can be found at [v1.4.7](https://github.com/siderolabs/talos/releases/tag/v1.4.7)

## Images

```
ghcr.io/siderolabs/flannel:v0.21.4
ghcr.io/siderolabs/install-cni:v1.4.0-4-g9b41398
docker.io/coredns/coredns:1.10.1
gcr.io/etcd-development/etcd:v3.5.9
registry.k8s.io/kube-apiserver:v1.27.4
registry.k8s.io/kube-controller-manager:v1.27.4
registry.k8s.io/kube-scheduler:v1.27.4
registry.k8s.io/kube-proxy:v1.27.4
ghcr.io/siderolabs/kubelet:v1.27.4
ghcr.io/siderolabs/installer:v1.4.8
registry.k8s.io/pause:3.6
```

# Changelog for talos_v1.4.7_stable
## [Talos 1.4.7](https://github.com/siderolabs/talos/releases/tag/v1.4.7) (2023-07-26)

Welcome to the v1.4.7 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

Kubernetes: 1.27.4
Linux: 6.1.41

Talos is built with Go 1.20.6.


### Contributors

* Andrey Smirnov

### Changes
<details><summary>6 commits</summary>
<p>

* siderolabs/talos@a1ee7612f release(v1.4.7): prepare release
* siderolabs/talos@95a3670f6 chore: workaround AWS AMI failures, disable Azure uploader
* siderolabs/talos@8f35f7dbe feat: update Linux to 6.1.41
* siderolabs/talos@696a6fb63 feat: update Kubernetes default to 1.27.4
* siderolabs/talos@7b5e94816 chore: optimize image generation time
* siderolabs/talos@d6af392e1 chore: update Go to 1.20.6
</p>
</details>

### Changes from siderolabs/extras
<details><summary>1 commit</summary>
<p>

* siderolabs/extras@2b5a1e6 feat: update Go to 1.20.6
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>2 commits</summary>
<p>

* siderolabs/pkgs@69266d9 feat: update Linux to 6.1.41
* siderolabs/pkgs@d5a3fd7 feat: update Go to 1.20.6
</p>
</details>

### Changes from siderolabs/tools
<details><summary>1 commit</summary>
<p>

* siderolabs/tools@78b2dc6 feat: update Go to 1.20.6
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/extras**               v1.4.0-2-gb2aba9d -> v1.4.0-3-g2b5a1e6
* **github.com/siderolabs/pkgs**                 v1.4.1-14-ge911ac5 -> v1.4.1-16-g69266d9
* **github.com/siderolabs/talos/pkg/machinery**  v1.4.6 -> v1.4.7
* **github.com/siderolabs/tools**                v1.4.0-3-gfac34e5 -> v1.4.0-4-g78b2dc6
* **k8s.io/api**                                 v0.27.3 -> v0.27.4
* **k8s.io/apimachinery**                        v0.27.3 -> v0.27.4
* **k8s.io/apiserver**                           v0.27.3 -> v0.27.4
* **k8s.io/client-go**                           v0.27.3 -> v0.27.4
* **k8s.io/component-base**                      v0.27.3 -> v0.27.4
* **k8s.io/kubectl**                             v0.27.3 -> v0.27.4
* **k8s.io/kubelet**                             v0.27.3 -> v0.27.4

Previous release can be found at [v1.4.6](https://github.com/siderolabs/talos/releases/tag/v1.4.6)

## Images

```
ghcr.io/siderolabs/flannel:v0.21.4
ghcr.io/siderolabs/install-cni:v1.4.0-3-g2b5a1e6
docker.io/coredns/coredns:1.10.1
gcr.io/etcd-development/etcd:v3.5.9
registry.k8s.io/kube-apiserver:v1.27.4
registry.k8s.io/kube-controller-manager:v1.27.4
registry.k8s.io/kube-scheduler:v1.27.4
registry.k8s.io/kube-proxy:v1.27.4
ghcr.io/siderolabs/kubelet:v1.27.4
ghcr.io/siderolabs/installer:v1.4.7
registry.k8s.io/pause:3.6
```

# Changelog for talos_v1.4.6_stable
## [Talos 1.4.6](https://github.com/siderolabs/talos/releases/tag/v1.4.6) (2023-06-28)

Welcome to the v1.4.6 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

Kubernetes: 1.27.3
Linux: 6.1.35

Talos is built with Go 1.20.5.


### Contributors

* Andrey Smirnov
* Alex Lubbock
* Noel Georgi
* Utku Ozdemir

### Changes
<details><summary>10 commits</summary>
<p>

* siderolabs/talos@8615b213e release(v1.4.6): prepare release
* siderolabs/talos@bb76a38d4 fix: provide stashed META values before installation
* siderolabs/talos@109a6c659 fix: allow time skew for generated kubeconfig
* siderolabs/talos@765f87b95 chore: optimize image compression
* siderolabs/talos@8c9f0495f fix: do not probe kernel args in dashboard if not needed
* siderolabs/talos@d759302d9 fix: skip DHCP RENEW if server IP in the lease is all zeroes
* siderolabs/talos@2b33a66d7 fix: upgrade-k8s use internal IP first, external IP fallback
* siderolabs/talos@b5bbb3f2e feat: update Linux to 6.1.36
* siderolabs/talos@1e9c3b3b8 feat: update default Kubernetes version to 1.27.3
* siderolabs/talos@21a490b11 chore: update to Go 1.20.5
</p>
</details>

### Changes from siderolabs/extras
<details><summary>1 commit</summary>
<p>

* siderolabs/extras@b2aba9d feat: update Go to 1.20.5
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>3 commits</summary>
<p>

* siderolabs/pkgs@e911ac5 feat: update Linux to 6.1.35
* siderolabs/pkgs@15a5cba fix: bump drbd to 9.2.4
* siderolabs/pkgs@91b8dd4 feat: update Go to 1.20.5
</p>
</details>

### Changes from siderolabs/tools
<details><summary>1 commit</summary>
<p>

* siderolabs/tools@fac34e5 feat: update Go to 1.20.5
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/extras**               v1.4.0-1-g9b07505 -> v1.4.0-2-gb2aba9d
* **github.com/siderolabs/pkgs**                 v1.4.1-11-g3e75ce2 -> v1.4.1-14-ge911ac5
* **github.com/siderolabs/talos/pkg/machinery**  v1.4.5 -> v1.4.6
* **github.com/siderolabs/tools**                v1.4.0-2-g5d0e9ab -> v1.4.0-3-gfac34e5
* **k8s.io/api**                                 v0.27.2 -> v0.27.3
* **k8s.io/apimachinery**                        v0.27.2 -> v0.27.3
* **k8s.io/apiserver**                           v0.27.2 -> v0.27.3
* **k8s.io/client-go**                           v0.27.2 -> v0.27.3
* **k8s.io/component-base**                      v0.27.2 -> v0.27.3
* **k8s.io/cri-api**                             v0.27.2 -> v0.27.3
* **k8s.io/kubectl**                             v0.27.2 -> v0.27.3
* **k8s.io/kubelet**                             v0.27.2 -> v0.27.3

Previous release can be found at [v1.4.5](https://github.com/siderolabs/talos/releases/tag/v1.4.5)

## Images

```
ghcr.io/siderolabs/flannel:v0.21.4
ghcr.io/siderolabs/install-cni:v1.4.0-2-gb2aba9d
docker.io/coredns/coredns:1.10.1
gcr.io/etcd-development/etcd:v3.5.9
registry.k8s.io/kube-apiserver:v1.27.3
registry.k8s.io/kube-controller-manager:v1.27.3
registry.k8s.io/kube-scheduler:v1.27.3
registry.k8s.io/kube-proxy:v1.27.3
ghcr.io/siderolabs/kubelet:v1.27.3
ghcr.io/siderolabs/installer:v1.4.6
registry.k8s.io/pause:3.6
```

## [Talos 1.4.1](https://github.com/siderolabs/talos/releases/tag/v1.4.1) (2023-04-27)

Welcome to the v1.4.1 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

* Linux: 6.1.25


### Contributors

* Andrey Smirnov
* Utku Ozdemir
* Noel Georgi
* Nico Berlee

### Changes
<details><summary>14 commits</summary>
<p>

* siderolabs/talos@647c6b4ef release(v1.4.1): prepare release
* siderolabs/talos@726d8d984 feat: update Linux to 6.1.25, fix virtio on arm64
* siderolabs/talos@ab09baf3d fix: bump max inhibit delay to 20 min
* siderolabs/talos@e94a19602 fix: udevd rules trigger
* siderolabs/talos@0cd177524 fix: display correct number of machines on dashboard
* siderolabs/talos@6b6e6c9c7 feat: clean up (garbage collect) system images which are not referenced
* siderolabs/talos@254086d6d fix: support kernel userspace module loading
* siderolabs/talos@0ef60514e feat: add startup probes to controller-manager and scheduler
* siderolabs/talos@9ce238794 fix: do not show control plane status for workers on dashboard
* siderolabs/talos@b92d9965f fix: allow `talosctl cp` to handle special files in `/proc`
* siderolabs/talos@c003fce72 chore: fix container image reproducibility
* siderolabs/talos@0a00a4ea7 fix: parse errors correctly
* siderolabs/talos@447c73b05 test: submit verbose flag to e2e tests
* siderolabs/talos@bf1cfe9c8 feat: show template URL in dashboard config URL tab
</p>
</details>

### Changes from siderolabs/go-blockdevice
<details><summary>1 commit</summary>
<p>

* siderolabs/go-blockdevice@076874a chore: resolve blockdevice symlinks
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>3 commits</summary>
<p>

* siderolabs/pkgs@0657493 chore: allow more than one commit per PR
* siderolabs/pkgs@6ddcc52 feat: update Linux to 6.1.25
* siderolabs/pkgs@a969180 feat: add multi-gen LRU kernel support
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/go-blockdevice**       v0.4.4 -> v0.4.5
* **github.com/siderolabs/pkgs**                 v1.4.1-5-ga333a84 -> v1.4.1-8-g0657493
* **github.com/siderolabs/talos/pkg/machinery**  v1.4.0 -> v1.4.1

Previous release can be found at [v1.4.0](https://github.com/siderolabs/talos/releases/tag/v1.4.0)

## Images

```
ghcr.io/siderolabs/flannel:v0.21.4
ghcr.io/siderolabs/install-cni:v1.4.0-1-g9b07505
docker.io/coredns/coredns:1.10.1
gcr.io/etcd-development/etcd:v3.5.8
registry.k8s.io/kube-apiserver:v1.27.1
registry.k8s.io/kube-controller-manager:v1.27.1
registry.k8s.io/kube-scheduler:v1.27.1
registry.k8s.io/kube-proxy:v1.27.1
ghcr.io/siderolabs/kubelet:v1.27.1
ghcr.io/siderolabs/installer:v1.4.1
registry.k8s.io/pause:3.6
```

## [Talos 1.3.7](https://github.com/siderolabs/talos/releases/tag/v1.3.7) (2023-04-06)

Welcome to the v1.3.7 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

* Linux: 5.15.106
* containerd: 1.6.20
* runc: 1.1.5
* Kubernetes: v1.26.3

Talos is built with Go 1.19.8.


### Contributors

* Andrey Smirnov
* Dmitriy Matrenichev

### Changes
<details><summary>8 commits</summary>
<p>

* siderolabs/talos@d17c9ee82 release(v1.3.7): prepare release
* siderolabs/talos@fe76c56fe fix: correctly parse static pod phase
* siderolabs/talos@dc001d28f fix: output of `talosctl logs` might be corruped
* siderolabs/talos@422e30a2f fix: always shutdown maintenance API service
* siderolabs/talos@19f7f7f39 feat: update Kubernetes to 1.26.3
* siderolabs/talos@13456dab3 fix: use 'no block' etcd dial with multiple endpoints
* siderolabs/talos@93dfa86d7 fix: nil pointer exception in syncLink
* siderolabs/talos@34677b931 feat: update Go 1.19.8, Linux 5.15.106
</p>
</details>

### Changes from siderolabs/extras
<details><summary>1 commit</summary>
<p>

* siderolabs/extras@75d687a chore: update Go to 1.19.8
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>2 commits</summary>
<p>

* siderolabs/pkgs@49b4ba8 feat: update Go 1.19.8, Linux 5.15.106
* siderolabs/pkgs@d1b0e28 feat: containerd 1.6.20, runc 1.1.5
</p>
</details>

### Changes from siderolabs/tools
<details><summary>1 commit</summary>
<p>

* siderolabs/tools@9a1d3ec feat: update Go to 1.19.8
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/extras**               v1.3.0-4-gcb97438 -> v1.3.0-5-g75d687a
* **github.com/siderolabs/pkgs**                 v1.3.0-15-g3b37079 -> v1.3.0-17-g49b4ba8
* **github.com/siderolabs/talos/pkg/machinery**  v1.3.6 -> v1.3.7
* **github.com/siderolabs/tools**                v1.3.0-3-ge225a7e -> v1.3.0-4-g9a1d3ec
* **k8s.io/api**                                 v0.26.2 -> v0.26.3
* **k8s.io/apiserver**                           v0.26.2 -> v0.26.3
* **k8s.io/client-go**                           v0.26.2 -> v0.26.3
* **k8s.io/component-base**                      v0.26.2 -> v0.26.3
* **k8s.io/kubectl**                             v0.26.2 -> v0.26.3
* **k8s.io/kubelet**                             v0.26.2 -> v0.26.3

Previous release can be found at [v1.3.6](https://github.com/siderolabs/talos/releases/tag/v1.3.6)

## Images

```
ghcr.io/siderolabs/flannel:v0.20.2
ghcr.io/siderolabs/install-cni:v1.3.0-5-g75d687a
docker.io/coredns/coredns:1.10.0
gcr.io/etcd-development/etcd:v3.5.7
registry.k8s.io/kube-apiserver:v1.26.3
registry.k8s.io/kube-controller-manager:v1.26.3
registry.k8s.io/kube-scheduler:v1.26.3
registry.k8s.io/kube-proxy:v1.26.3
ghcr.io/siderolabs/kubelet:v1.26.3
ghcr.io/siderolabs/installer:v1.3.7
registry.k8s.io/pause:3.6
```

## [Talos 1.2.3](https://github.com/siderolabs/talos/releases/tag/v1.2.3) (2022-09-20)

Welcome to the v1.2.3 release of Talos!



Please try out the release binaries and report any issues at
https://github.com/siderolabs/talos/issues.

### Component Updates

* Kubernetes: v1.25.1
* etcd: v3.5.5
* Linux: 5.15.68


### Contributors

* Andrey Smirnov
* Dmitriy Matrenichev
* Noel Georgi

### Changes
<details><summary>9 commits</summary>
<p>

* siderolabs/talos@40cb1b493 release(v1.2.3): prepare release
* siderolabs/talos@19cb6203c chore: add ice drivers
* siderolabs/talos@4e23aa2a7 feat: update etcd to v3.5.5
* siderolabs/talos@4754b59ce feat: update Kubernetes to v1.25.1
* siderolabs/talos@b00186463 chore: return InvalidArgument on invalid config in maintenance mode
* siderolabs/talos@1d7d8d5dd fix: set etcd options consistently
* siderolabs/talos@88861e770 chore: mark machine configuration validation failure as InvalidArgument
* siderolabs/talos@04406b0ba chore: add output of VLANSpec encoding to tests
* siderolabs/talos@1d522938d fix: ensure that custom Decoder gets called for netaddr.IP
</p>
</details>

### Changes from siderolabs/pkgs
<details><summary>1 commit</summary>
<p>

* siderolabs/pkgs@eb07d7c chore: bump kernel + enable intel ice drivers
</p>
</details>

### Dependency Changes

* **github.com/siderolabs/pkgs**     v1.2.0-10-g0f4351f -> v1.2.0-11-geb07d7c
* **go.etcd.io/etcd/api/v3**         v3.5.4 -> v3.5.5
* **go.etcd.io/etcd/client/pkg/v3**  v3.5.4 -> v3.5.5
* **go.etcd.io/etcd/client/v3**      v3.5.4 -> v3.5.5
* **go.etcd.io/etcd/etcdutl/v3**     v3.5.4 -> v3.5.5
* **go.uber.org/atomic**             v1.9.0 -> v1.10.0
* **go.uber.org/zap**                v1.22.0 -> v1.23.0
* **golang.org/x/net**               3211cb980234 -> bea034e7d591
* **golang.org/x/sync**              886fb9371eb4 -> f12130a52804
* **golang.org/x/sys**               fbc7d0a398ab -> aba9fc2a8ff2
* **k8s.io/api**                     v0.25.0 -> v0.25.1
* **k8s.io/apimachinery**            v0.25.0 -> v0.25.1
* **k8s.io/apiserver**               v0.25.0 -> v0.25.1
* **k8s.io/client-go**               v0.25.0 -> v0.25.1
* **k8s.io/component-base**          v0.25.0 -> v0.25.1
* **k8s.io/cri-api**                 v0.25.0 -> v0.25.1
* **k8s.io/kubectl**                 v0.25.0 -> v0.25.1
* **k8s.io/kubelet**                 v0.25.0 -> v0.25.1

Previous release can be found at [v1.2.2](https://github.com/siderolabs/talos/releases/tag/v1.2.2)

## Images

```
ghcr.io/siderolabs/flannel:v0.19.2
ghcr.io/siderolabs/install-cni:v1.2.0-1-g116c5a9
docker.io/coredns/coredns:1.9.3
gcr.io/etcd-development/etcd:v3.5.5
k8s.gcr.io/kube-apiserver:v1.25.1
k8s.gcr.io/kube-controller-manager:v1.25.1
k8s.gcr.io/kube-scheduler:v1.25.1
k8s.gcr.io/kube-proxy:v1.25.1
ghcr.io/siderolabs/kubelet:v1.25.1
ghcr.io/siderolabs/installer:v1.2.3
k8s.gcr.io/pause:3.6
```
