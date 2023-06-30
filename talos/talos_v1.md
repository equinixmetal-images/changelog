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

