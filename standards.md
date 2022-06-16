# General architecture standards

Production server should not expose stack traces logs to end users (OWASP, Security Misconfiguration).

## Versioning

- [Semantic Versioning](https://github.com/semver/semver/blob/master/semver.md)

Semver prefixes: use non-standard `v1.0.0` only when needed to differentiate _versioning tag from other tags_ in VCS,
otherwise use semver compliant `1.0.0`.

## Conventional Commits

- [Specification](https://www.conventionalcommits.org/en/v1.0.0/#specification)
- [Angular specification](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#type)
- [commitlint config](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)
- [conventional-changelog](https://github.com/conventional-changelog/conventional-changelog)
