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
