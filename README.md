# nginx-module-auth-pam RPM Packaging

[![Build Status](https://github.com/jfut/nginx-module-auth-pam-rpm/workflows/test/badge.svg?branch=master)](https://github.com/jfut/nginx-module-auth-pam-rpm/actions?query=workflow%3Atest)

[ngx_http_auth_pam_module](https://github.com/sto/ngx_http_auth_pam_module) RPM Packaging for RHEL/AlmaLinux/Rocky Linux/others.

## Install an RPM package

- [Download](https://github.com/jfut/nginx-module-auth-pam-rpm/releases)
- Install:
    - RHEL/AlmaLinux/Rocky Linux 10
    ```bash
    # Non-modular package version 1.26 for x86_64
    dnf install nginx-module-auth-pam-1.5.5-7.el10.x86_64.rpm

    # Non-modular package version 1.26 for x86_64_v2
    dnf install nginx-module-auth-pam-1.5.5-7.el10.x86_64_v2.rpm

    # Non-modular package version 1.26 for aarch64
    dnf install nginx-module-auth-pam-1.5.5-7.el10.aarch64.rpm
    ```
    - RHEL/AlmaLinux/Rocky Linux 9 x86_64
    ```bash
    # Non-modular package version 1.20
    dnf install nginx-module-auth-pam-1.5.5-7.el9.x86_64.rpm

    # AppStream module 1.22 stream
    dnf install nginx-module-auth-pam-1.5.5-7.module_el9.1.22.x86_64.rpm

    # AppStream module 1.24 stream
    dnf install nginx-module-auth-pam-1.5.5-7.module_el9.1.24.x86_64.rpm

    # AppStream module 1.26 stream
    dnf install nginx-module-auth-pam-1.5.5-7.module_el9.1.26.x86_64.rpm
    ```
    - RHEL/AlmaLinux/Rocky Linux 8 x86_64
    ```bash
    # AppStream module 1.16 stream
    dnf install nginx-module-auth-pam-1.5.5-7.module_el8.1.16.x86_64.rpm

    # AppStream module 1.18 stream
    dnf install nginx-module-auth-pam-1.5.5-7.module_el8.1.18.x86_64.rpm

    # AppStream module 1.20 stream
    dnf install nginx-module-auth-pam-1.5.5-7.module_el8.1.20.x86_64.rpm

    # AppStream module 1.22 stream
    dnf install nginx-module-auth-pam-1.5.5-7.module_el8.1.22.x86_64.rpm

    # AppStream module 1.24 stream
    dnf install nginx-module-auth-pam-1.5.5-7.module_el8.1.24.x86_64.rpm

    # EPEL module mainline stream (version: 1.23)
    # EPEL 8 Modularity was going away on February 15, 2023
    dnf install nginx-module-auth-pam-1.5.5-7.module_el8.epel.mainline.x86_64.rpm
    ```
- Add your configuration for this module (See [the official documentation](https://github.com/sto/ngx_http_auth_pam_module)).
- Restart nginx:
    ```bash
    systemctl restart nginx.service
    ```

If `include /usr/share/nginx/modules/*.conf;` is enabled in `nginx.conf`, this module is enabled by default. If you want to disable the module once installed, simply comment out the contents of `/usr/share/nginx/modules/mod-http-auth-pam.conf`.

## Usage

```bash
Usage:
    build [-d] [-h] [-p PLATFORM] BUILD_IMAGE_NAME:BUILD_IMAGE_TAG[:REPOSITORY][:MODULE_VERSION]

    Options:
        -d Debug mode.

    Build for RHEL/AlmaLinux/Rocky Linux 10 + AppStream module:
        build almalinux:10

    Build for RHEL/AlmaLinux/Rocky Linux 9 + AppStream module:
        build almalinux:9
        build almalinux:9:appstream:1.22
        build almalinux:9:appstream:1.24
        build almalinux:9:appstream:1.26

    Build for RHEL/AlmaLinux/Rocky Linux 8 + AppStream module:
        # build almalinux:8 (version 1.14 is not supported)
        build almalinux:8:appstream:1.16
        build almalinux:8:appstream:1.18
        build almalinux:8:appstream:1.20
        build almalinux:8:appstream:1.22
        build almalinux:8:appstream:1.24

    Build for RHEL/AlmaLinux/Rocky Linux 8 + EPEL Stream module:
        # EPEL 8 Modularity was going away on February 15, 2023
        build almalinux:8:epel-modular:mainline

    Build for RHEL/AlmaLinux/Rocky Linux 10 linux/arm64/v8(aarch64) + AppStream module:
        build -p linux/arm64/v8 almalinux:10

    Build for RHEL/AlmaLinux/Rocky Linux 9 linux/arm64/v8(aarch64) + AppStream module:
        build -p linux/arm64/v8 almalinux:9
        build -p linux/arm64/v8 almalinux:9:appstream:1.22
        build -p linux/arm64/v8 almalinux:9:appstream:1.24
```

## Build RPM Packages with Docker

You can build RPM packages in Docker.

```
# el10 + Non-modular package version
./build almalinux:10
```

- Debug shell

```bash
# el10 + debug shell
BUILD_HOSTNAME=el10.example.org ./build -d almalinux:10
/pkg/build-rpm /pkg/rpmbuild nginx-module-auth-pam.spec

# el9 + linux/arm64/v8 + debug shell
BUILD_HOSTNAME=el9.example.org ./build -d -p linux/arm64/v8 almalinux:9
/pkg/build-rpm /pkg/rpmbuild nginx-module-auth-pam.spec

# el8 + Modular package version + debug shell
BUILD_HOSTNAME=el8.example.org ./build -d almalinux:8:appstream:1.24
/pkg/build-rpm /pkg/rpmbuild nginx-module-auth-pam.spec appstream 1.24
```

## Release

1. Edit the `Draft` on the release page.
2. Update the new version `name` and `tag` on the edit page.
3. Check `Set as a pre-release` and press the `Publish release` button.
4. Wait for the build by GitHub Actions to finish.
    - If the build fails due to errors such as download errors of source files, execute `Re-run failed jobs`.
5. Once all release files are automatically uploaded, check `Set as the latest release` and press the `Publish release` button.

## License

BSD-2-Clause
