# nginx-module-auth-pam RPM Packaging

[![Build Status](https://github.com/jfut/nginx-module-auth-pam-rpm/workflows/test/badge.svg?branch=master)](https://github.com/jfut/nginx-module-auth-pam-rpm/actions?query=workflow%3Atest)

RPM Packaging for [ngx_http_auth_pam_module](https://github.com/sto/ngx_http_auth_pam_module).

## Install an RPM package

- [Download](https://github.com/jfut/nginx-module-auth-pam-rpm/releases)
- `yum install nginx-module-auth-pam-x.y.z-n.elx.x86_64.rpm`
- Add `load_module` in `nginx.conf`:
    ```
    load_module "modules/ngx_http_auth_pam_module.so";
    ```
- Add your configuration for this module (See [the official documentation](https://github.com/sto/ngx_http_auth_pam_module)).
- `systemctl restart nginx.service`

## Usage

```
Usage:
    build [-d] [-h] BUILD_IMAGE_NAME

    Options:
        -d Debug mode.

    Build for CentOS 8:
        build -i centos:8

    Build for CentOS 7:
        build -i centos:7
```

## Build RPM Packages with Docker

You can build RPM packages in Docker.

```
./build
```

- Debug shell

```
./build -d
/pkg/build-rpm /pkg/rpmbuild nginx-module-auth-pam.spec
```

## Release tag

e.g.:

```
git tag -a v1.5.1-1 -m "v1.5.1-1"
git push origin refs/tags/v1.5.1-1
```

## License

BSD-2-Clause

