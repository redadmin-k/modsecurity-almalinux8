# ModSecurity RPM for AlmaLinux 8

This repository provides an unofficial RPM packaging spec for ModSecurity v3 on AlmaLinux 8.

This package is intended for testing and verification of Nginx WAF integration using ModSecurity.

## Overview

This repository contains RPM packaging files for building ModSecurity v3 on AlmaLinux 8.

The package installs ModSecurity under:

```text
/opt/modsecurity
```

Example runtime library path:

```text
/opt/modsecurity/lib64/libmodsecurity.so.3
```

This package can be used together with an Nginx build that includes the ModSecurity-nginx connector.

## Disclaimer

This repository is unofficial.

It is not provided, maintained, endorsed, or supported by AlmaLinux OS Foundation, OWASP, Trustwave, or any upstream project.

Use this repository at your own risk.

The author provides no warranty of any kind.
Please test carefully in a verification environment before using it in production.

## License

ModSecurity is licensed under the Apache License 2.0.

See the upstream ModSecurity project for details:

* https://github.com/owasp-modsecurity/ModSecurity

Packaging files in this repository are provided for RPM build and integration testing purposes.

Unless otherwise stated, packaging files in this repository are released under the Apache License 2.0.

## Notes

ModSecurity rules can be strict and may block legitimate requests depending on the application behavior.

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

CentOS 7 may require additional dependency RPMs and separate verification.

