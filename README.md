# ModSecurity RPM for AlmaLinux 8

This repository provides an unofficial RPM package for ModSecurity v3 on AlmaLinux 8.

The package is intended for testing and verification of Nginx WAF integration using the ModSecurity-nginx connector.

## Overview

This RPM installs ModSecurity under:

```text
/opt/modsecurity
```

Example runtime library path:

```text
/opt/modsecurity/lib64/libmodsecurity.so.3
```

The package includes:

* ModSecurity runtime libraries
* ModSecurity headers
* pkg-config files
* example configuration files
* ldconfig configuration for `/opt/modsecurity/lib64`

This package can be used together with an Nginx build that includes the ModSecurity-nginx connector.

## Repository Layout

```text
README.md
SPEC/
RPMS/
Logs/
```

RPM files are stored under:

```text
RPMS/
```

## Install

Install the built RPM package with:

```bash
sudo dnf localinstall RPMS/*.rpm
```

If RPM files are stored under an architecture subdirectory, use:

```bash
sudo dnf localinstall RPMS/x86_64/*.rpm
```

A more general command is:

```bash
sudo dnf localinstall $(find RPMS -type f -name '*.rpm' | sort)
```

## Verify Installation

Check installed files:

```bash
rpm -ql modsecurity | grep /opt/modsecurity
```

Check that the runtime library is visible to the dynamic linker:

```bash
ldconfig -p | grep libmodsecurity
```

Expected example:

```text
libmodsecurity.so.3 => /opt/modsecurity/lib64/libmodsecurity.so.3
```

## Example Paths

Main installation directory:

```text
/opt/modsecurity
```

Library directory:

```text
/opt/modsecurity/lib64
```

Header directory:

```text
/opt/modsecurity/include
```

pkg-config directory:

```text
/opt/modsecurity/lib64/pkgconfig
```

Example configuration files:

```text
/opt/modsecurity/share/modsecurity.conf-recommended
/opt/modsecurity/share/unicode.mapping
```

ldconfig configuration:

```text
/etc/ld.so.conf.d/modsecurity.conf
```

## Nginx Integration Notes

This package only installs ModSecurity itself.

To use ModSecurity with Nginx, Nginx must be built with the ModSecurity-nginx connector.

When building Nginx, make sure the build can find ModSecurity under:

```text
/opt/modsecurity
```

For example:

```bash
export PKG_CONFIG_PATH=/opt/modsecurity/lib64/pkgconfig
```

## ModSecurity Rule Engine

Before enabling blocking mode in production, it is recommended to run ModSecurity in detection-only mode and review logs carefully.

Example:

```apache
SecRuleEngine DetectionOnly
```

After sufficient verification, blocking mode can be enabled if appropriate.

```apache
SecRuleEngine On
```

## Target Environment

Tested target environment:

```text
AlmaLinux 8
ModSecurity v3
Nginx with ModSecurity-nginx connector
```

## Disclaimer

This repository is unofficial.

It is not provided, maintained, endorsed, or supported by AlmaLinux OS Foundation, OWASP, Trustwave, or any upstream project.

Use this repository at your own risk.

The author provides no warranty of any kind.

Please test carefully in a verification environment before using it in production.

## License

ModSecurity is licensed under the Apache License 2.0.

See the upstream ModSecurity project for details:

```text
https://github.com/owasp-modsecurity/ModSecurity
```

Packaging files in this repository are provided for RPM build and integration testing purposes.

Unless otherwise stated, packaging files in this repository are released under the Apache License 2.0.

