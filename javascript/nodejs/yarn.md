# Yarn

## Setup

- [Installation](https://yarnpkg.com/getting-started/install)
- [Updating to the latest versions](https://yarnpkg.com/getting-started/install#updating-to-the-latest-versions)

## Plugins

- [Official plugins](https://yarnpkg.com/features/plugins#official-plugins)
- [Contrib plugins](https://yarnpkg.com/features/plugins#contrib-plugins)

Recommended plugins:

- interactive-tools: interactive upgrade
- typescript: improves the TypeScript experience

## PnP

Yarn PnP mode is not compatible with ES modules, when transpiling use commonjs.

## Production install

Using both `--production` and `--frozen-lockfile` v1 flags was an [antipattern](https://github.com/yarnpkg/berry/issues/2253#issuecomment-748439061).

## Mono-repository

Examples:

- [nsiebenaller/yarn-workspace-template](https://github.com/nsiebenaller/yarn-workspace-template)
- [plus-/yarn-commitlint-sample](https://github.com/plus-/yarn-commitlint-sample)
- [facebook/jest](https://github.com/facebook/jest)
