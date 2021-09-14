# General architecture standards

Production server should not expose stack traces logs to end users (OWASP, Security Misconfiguration).

## Versioning

* [Semantic Versioning](https://github.com/semver/semver/blob/master/semver.md)

Semver prefixes: use non-standard `v1.0.0` only when needed to differentiate versioning tag from other tags in VCS,
otherwise use semver compliant `1.0.0`.

* [Is "v1.2.3" a semantic version?](https://github.com/semver/semver/blob/master/semver.md#is-v123-a-semantic-version)

