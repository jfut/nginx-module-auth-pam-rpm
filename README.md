# nginx-module-auth-pam RPM Packaging

[![Build Status](https://github.com/jfut/nginx-module-auth-pam-rpm/workflows/test/badge.svg?branch=master)](https://github.com/jfut/nginx-module-auth-pam-rpm/actions?query=workflow%3Atest)

RPM Packaging for [ngx_http_auth_pam_module](https://github.com/sto/ngx_http_auth_pam_module).

## Install an RPM package

- [Download](https://github.com/jfut/nginx-module-auth-pam-rpm/releases)
- `yum install nginx-module-auth-pam-1.5.2-n.elx.x86_64.rpm`
- Install:
    ```
    # el7
    yum install nginx-module-auth-pam-1.5.2-2.el7.x86_64.rpm

    # el8 + module 1.16 stream
    dnf install nginx-module-auth-pam-1.5.2-2.module_el8.1.16.x86_64.rpm

    # el8 + EPEL module mainline stream
    dnf install nginx-module-auth-pam-1.5.2-2.module_el8.mainline.x86_64.rpm
    ```
- Add `load_module` in `nginx.conf`:
    ```
    load_module "modules/ngx_http_auth_pam_module.so";
    ```
- Add your configuration for this module (See [the official documentation](https://github.com/sto/ngx_http_auth_pam_module)).
- `systemctl restart nginx.service`

## Usage

```
Usage:
    build [-d] [-h] BUILD_IMAGE_NAME:BUILD_IMAGE_TAG[:MODULE_VERSION]

    Options:
        -d Debug mode.

    Build for CentOS 8 + AppStream module:
        # build centos:8:1.14 1.14 (not supported)
        build centos:8:1.16

    Build for CentOS 8 + EPEL Stream module:
        build centos:8:mainline

    Build for CentOS 7:
        build centos:7
```

## Build RPM Packages with Docker

You can build RPM packages in Docker.

```
./build
```

- Debug shell

```
./build -d
/pkg/build-rpm /pkg/rpmbuild nginx-module-auth-pam.spec 1.16
```

## Release tag

e.g.:

```
git tag -a v1.5.2-2 -m "v1.5.2-2"
git push origin refs/tags/v1.5.2-2
```

## License

BSD-2-Clause

