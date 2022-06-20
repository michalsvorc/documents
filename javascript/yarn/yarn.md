# Yarn 

This documentation is related to Yarn v2.

## PnP

Yarn PnP mode is not compatible with ES modules, when transpiling use commonjs.

## Production install

Using both `--production` and `--frozen-lockfile` v1 flags was an [antipattern](https://github.com/yarnpkg/berry/issues/2253#issuecomment-748439061).

## Mono-repository

Examples:

- [nsiebenaller/yarn-workspace-template](https://github.com/nsiebenaller/yarn-workspace-template)
- [plus-/yarn-commitlint-sample](https://github.com/plus-/yarn-commitlint-sample)
- [facebook/jest](https://github.com/facebook/jest)
