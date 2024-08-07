# Equinix Metal published images

Equinix Metal publishes images on the platform that have been built with the fleet's requirements in mind. These images are tested/validated against the fleet and are known to work with our metal. For most operating systems we publish fresh images on monthly basis, this guarantees a smooth user experience and reduces install times.

Images are kept as close to upstream releases as possible. It is not always possible (for a number of reasons) for us to publish a full changelog for every operating system which can be provisioned on our platform, but we strive to keep this changelog as comprehensive and up to date as possible.

# Changelog

The changelog aims to show what packages have changed since the last published image, what kernel and what deviations from upstream (if any) per new published image.

If there is any information that would be helpful but is missing from the changelog, [please raise an issue](https://github.com/equinixmetal-images/changelog/issues/new) and we will do our best to add it going forward.

# Equinix Metal Operating System Support Schedule

This is the list with latest details on the OSs Equinix Metal repackages and publishes for customers. Please, note that certain OSs, when they are approaching EOL (End Of Life) upstream, may not be supported in the newest hardware due to driver or other compatibility issues.

| OS                      | Version | Upstream EOL  | EM Estimated EOL |  Changelog                      | Notes |
| ---                     | ---   | ---             | ---        | ---                                                           | --- |
| Ubuntu                  | 20.04 | Apr, 2030       | Jan, 2030  | [x86_64](ubuntu/x86_64/20_04.md) [arm64](ubuntu/aarch64/20_04.md) | |
| Ubuntu                  | 22.04 | Apr, 2032       | Jan, 2032  | [x86_64](ubuntu/x86_64/22_04.md) [arm64](ubuntu/aarch64/22_04.md) | |
| Ubuntu                  | 24.04 | Apr, 2034       | Jan, 2034  | [x86_64](ubuntu/x86_64/24_04.md) [arm64](ubuntu/aarch64/24_04.md) | |
| Debian                  | 11    | Jun, 2026       | Mar, 2026  | [x86_64](debian/x86_64/11.md) [arm64](debian/aarch64/11.md)       | |
| RedHat Enterprise Linux | 8     | May, 2024       | N/A        | [x86_64](rhel/x86_64/8.md)                                        | |
| RedHat Enterprise Linux | 9     | TBA             | N/A        | [x86_64](rhel/x86_64/9.md)                                        | |
| AlmaLinux OS            | 8     | May, 2024       | Feb, 2024  | [x86_64](alma/x86_64/8.md) [arm64](alma/aarch64/8.md)             | |
| AlmaLinux OS            | 9     | May, 2027       | Feb, 2027  | [x86_64](alma/x86_64/9.md) [arm64](alma/aarch64/9.md)             | |
| Rocky Linux             | 8     | May, 2024       | Feb, 2024  | [x86_64](rocky/x86_64/8.md) [arm64](rocky/aarch64/8.md)           | |
| Rocky Linux             | 9     | May, 2025       | Feb, 2025  | [x86_64](rocky/x86_64/9.md) [arm64](rocky/aarch64/9.md)           | |
| Alpine                  | 3     | Rolling Release | N/A        | [x86_64](alpine/x86_64/3.md) [arm64](alpine/aarch64/3.md)         | |
| VMware ESXi             | 7.0   | Apr, 2025       | Jan, 2025  | TBA                                                               | |
| VMware ESXi             | 8.0   | TBA             | TBA        | TBA                                                               | |
| VMware VCF              | 5.1   | TBA             | TBA        | TBA                                                               | |
| Windows Server          | 2022  | Oct, 2026       |            | [x86_64](windows%202022/windows_2022.md)                          | |
| Windows Server          | 2019  | Jan, 2024       | Sept, 2024 | [x86_64](windows%202019/windows_2019.md)                          | |
| Flatcar Linux           | stable | Rolling release | N/A       | Rolling release                       | Available                 | |
| Flatcar Linux           | beta  | Rolling release | N/A        | Rolling release                       | Available                 | |
| FreeBSD                 | 13.2  | Jan, 2026       | Jan, 2026  | [x86_64](freebsd/x86_64/13_2.md) [arm64](freebsd/arm64/13_2.md)   | |
| FreeBSD                 | 14.0  | Jan, 2029       | Jan, 2029  | [x86_64](freebsd/x86_64/14_0.md) [arm64](freebsd/arm64/14_0.md)   | |
| VyOS                    | 1.4   | TBA             | TBA        | [1.4](vyos/vyos_1_4.md)                                           | |

## EOL Operating Systems

The following OSes have been officialy EOL'ed at Equinix Metal and are no longer available. The Changelogs for these OSes have been deleted from this repository (but can still be retrieved via the commit history).

| OS                      | Version |
| ---                     | ---   |
| CentOS                  | 7,8   |
| Debian                  | 10    |
| RedHat Enterprise Linux | 7     |
| Ubuntu                  | 14.04,16.04,18.04 |
| VMware ESXi             | 6.5,6.7 |
