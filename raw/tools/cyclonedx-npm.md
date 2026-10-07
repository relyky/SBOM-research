---
title: "@cyclonedx/cyclonedx-npm"
source: https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm
author:
published: 2026-08-11
created: 2026-10-07
description: "Create CycloneDX Software Bill of Materials (SBOM) from NPM projects.. Latest version: 6.0.1, last published: 2 months ago. Start using @cyclonedx/cyclonedx-npm in your project by running `npm i @cyclonedx/cyclonedx-npm`. There are 5 other projects in the npm registry using @cyclonedx/cyclonedx-npm."
tags:
  - clippings
---
# CycloneDX SBOM for _npm_

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#cyclonedx-sbom-for-npm)

[![shield_npm-version](https://camo.githubusercontent.com/9e3226c1ff1e9598ba7cffc5d0e8c6a0b7339909b16a78c122c25ca1e45e6456/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f762f2534306379636c6f6e6564782532666379636c6f6e6564782d6e706d2f6c61746573743f6c6162656c3d6e706d266c6f676f3d6e706d266c6f676f436f6c6f723d7768697465 "npm")](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm) [![shield_gh-workflow-test](https://camo.githubusercontent.com/ac75664ac631a4d57d2d7cfaa5784dd981fb34408878a280d3fe10d22540c3dc/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f616374696f6e732f776f726b666c6f772f7374617475732f4379636c6f6e6544582f6379636c6f6e6564782d6e6f64652d6e706d2f6e6f64656a732e796d6c3f6272616e63683d6d61696e266c6f676f3d476974487562266c6f676f436f6c6f723d7768697465 "tests")](https://github.com/CycloneDX/cyclonedx-node-npm/actions/workflows/nodejs.yml?query=branch%3Amain) [![shield_coverage](https://camo.githubusercontent.com/80ad3d01388269c50c2e9c10f393624fea837403b8d414760b1f87ff26ef6281/68747470733a2f2f696d672e736869656c64732e696f2f636f646163792f636f7665726167652f31366230333465353436333534333030386531636330653261336564373030353f6c6f676f3d436f64616379266c6f676f436f6c6f723d7768697465 "test coverage")](https://app.codacy.com/gh/CycloneDX/cyclonedx-node-npm/dashboard) [![shield_ossf-best-practices](https://camo.githubusercontent.com/02fd0af7f73c28a79d39efcede8f2b1ea3705d1d4d6045a6e773583690106678/68747470733a2f2f696d672e736869656c64732e696f2f6369692f6c6576656c2f363631343f6c6162656c3d4f70656e53534625323062657374253230707261637469636573 "OpenSSF best practices")](https://www.bestpractices.dev/projects/6614) [![shield_license](https://camo.githubusercontent.com/692c18f46716c06ebfc59b0a56e04718a7b2d48dced691328861879b210dccf7/68747470733a2f2f696d672e736869656c64732e696f2f6769746875622f6c6963656e73652f4379636c6f6e6544582f6379636c6f6e6564782d6e6f64652d6e706d3f6c6f676f3d6f70656e253230736f75726365253230696e6974696174697665266c6f676f436f6c6f723d7768697465 "license")](https://github.com/CycloneDX/cyclonedx-node-npm/blob/main/LICENSE)  
[![shield_website](https://camo.githubusercontent.com/9905fa5ea81557b29cc02ac0400c299db5288cf953546628b6fa51a3668f234c/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f68747470733a2f2f2d6379636c6f6e6564782e6f72672d626c75652e737667 "homepage")](https://cyclonedx.org/) [![shield_slack](https://camo.githubusercontent.com/29cd2597d61476e11f9bd9cd6f3603f8b78404f39706fc83c9c4a77d7c2322c5/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f736c61636b2d6a6f696e2d626c75653f6c6f676f3d536c61636b266c6f676f436f6c6f723d7768697465 "slack join")](https://cyclonedx.org/slack/invite) [![shield_groups](https://camo.githubusercontent.com/76fae4f6b8172052f9331d39e5d0a47e4efa0e9c1e3480d79ccbfb70b4bf2808/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f64697363757373696f6e2d67726f7570732e696f2d626c75652e737667 "groups discussion")](https://groups.io/g/CycloneDX) [![shield_twitter-follow](https://camo.githubusercontent.com/011306690785b8ba83a328009cb8a5144db3e718ae7c6bb4955d01edde82c00a/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f547769747465722d666f6c6c6f772d626c75653f6c6f676f3d54776974746572266c6f676f436f6c6f723d7768697465 "twitter follow")](https://twitter.com/CycloneDX_Spec)

---

Create [CycloneDX](https://cyclonedx.org/) Software Bill of Materials (SBOM) from _[npm](http://www.npmjs.com/)_ projects.  
This is probably the most accurate, complete SBOM generator for npm-based projects.

Based on [OWASP Software Component Verification Standard for Software Bill of Materials](https://scvs.owasp.org/scvs/v2-software-bill-of-materials/)'s criteria, this tool is capable of producing SBOM documents almost passing Level-2 (only signing needs to be done externally).

The resulting SBOM documents follow [official specifications and standards](https://github.com/CycloneDX/specification), and might have properties following [`cdx:npm` Namespace Taxonomy](https://cyclonedx.github.io/cyclonedx-property-taxonomy/cdx/npm.html) and [`cdx` Namespace Taxonomy](https://cyclonedx.github.io/cyclonedx-property-taxonomy/cdx.html) .

## Requirements

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#requirements)

- `node >= 20.18.0`
- `npm >= 9`

However, there are older versions of this tool that support

- Node.js v14 or later
- NPM v6 or later

## Installation

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#installation)

There are multiple methods for installing this tool:

- As a global tool ala `npm`:
    
    ```shell
    npm install --global @cyclonedx/cyclonedx-npm
    ```
    
- As a global tool ala `npx`:
    
    ```shell
    npx --package @cyclonedx/cyclonedx-npm --call exit
    ```
    
- As a development dependency of the current project:
    
    ```shell
    npm install --save-dev @cyclonedx/cyclonedx-npm
    ```
    

## Usage

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#usage)

Depending on the installation method, the following describes the proper usage:

- If installed as a global tool ala `npm`:
    
    ```shell
    cyclonedx-npm --help
    ```
    
- If installed as a global tool ala `npx`:  
    — or —  
    If installed as a development dependency of the current projects:
    
    ```shell
    npx @cyclonedx/cyclonedx-npm --help
    ```
    

The help page:

```
Usage: cyclonedx-npm [options] [--] [<package-manifest>]

Create CycloneDX Software Bill of Materials (SBOM) from Node.js NPM projects.

Arguments:
  <package-manifest>              Path to project's manifest file.
                                  (default: "package.json" file in current working directory)

Options:
  --ignore-npm-errors             Whether to ignore errors of NPM.
                                  This might be used, if "npm install" was run with "--force" or "--legacy-peer-deps".
                                  (default: false)
  --package-lock-only             Whether to only use the lock file, ignoring "node_modules".
                                  This means the output will be based only on the few details in and the tree described by the "npm-shrinkwrap.json" or "package-lock.json", rather than the contents of "node_modules" directory.
                                  (default: false)
  --omit <type...>                Dependency types to omit from the installation tree.
                                  (can be set multiple times)
                                  (choices: "dev", "optional", "peer", default: "dev" if the NODE_ENV environment variable is set to "production", otherwise empty)
  -w, --workspace <workspace...>  Only include dependencies for specific workspaces.
                                  (can be set multiple times)
                                  This feature is experimental.
                                  (default: empty)
  --no-workspaces                 Do not include dependencies for workspaces.
                                  Default behaviour is to include dependencies for all configured workspaces.
                                  This cannot be used if workspaces have been explicitly defined using `--workspace`.
                                  This feature is experimental.
  --include-workspace-root        Include workspace root dependencies along with explicitly defined workspaces' dependencies. This can only be used if you have explicitly defined workspaces using `--workspace`.
                                  Default behaviour is to not include the workspace root when workspaces are explicitly defined using `--workspace`.
                                  This feature is experimental.
  --no-include-workspace-root     Do not include workspace root dependencies. This only has an effect if you have one or more workspaces configured in your project.
                                  This is useful if you want to include all dependencies for all workspaces without explicitly defining them with `--workspace` (default behaviour) but you do not want the workspace root dependencies included.
                                  This feature is experimental.
  --gather-license-texts          Search for license files in components and include them as license evidence.
                                  This feature is experimental.
                                  (default: false)
  --flatten-components            Whether to flatten the components.
                                  This means the actual nesting of node packages is not represented in the SBOM result.
                                  (default: false)
  --short-PURLs                   Omit all qualifiers from PackageURLs.
                                  This causes information loss in trade-off shorter PURLs, which might improve ingesting these strings.
                                  (default: false)
  --sv, --spec-version <version>  Which version of CycloneDX spec to use.
                                  (choices: "1.2", "1.3", "1.4", "1.5", "1.6", default: "1.6")
  --output-reproducible           Whether to go the extra mile and make the output reproducible.
                                  This requires more resources, and might result in loss of time- and random-based-values.
                                  (env: BOM_REPRODUCIBLE)
  --of, --output-format <format>  Which output format to use.
                                  (choices: "JSON", "XML", default: "JSON")
  -o, --output-file <file>        Path to the output file.
                                  Set to "-" to write to STDOUT.
                                  (default: write to STDOUT)
  --validate                      Validate resulting BOM before outputting.
                                  Validation is skipped, if requirements not met. See the README.
  --no-validate                   Disable validation of resulting BOM.
  --mc-type <type>                Type of the main component.
                                  (choices: "application", "firmware", "library", default: "application")
  -v, --verbose                   Increase the verbosity of messages.
                                  Use multiple times to increase the verbosity even more.
  -V, --version                   output the version number
  -h, --help                      display help for command
```

## Demo

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#demo)

For a demo of _cyclonedx-npm_ see the [demo projects](https://github.com/CycloneDX/cyclonedx-node-npm/blob/main/demo/README.md).

## How it works

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#how-it-works)

This tool utilizes _[npm](http://www.npmjs.com/)_ to collect evidences of installed packages/modules. Read more in the [dedicated docs](https://github.com/CycloneDX/cyclonedx-node-npm/tree/main/docs/how.md).

The appropriate _npm_ executable is detected automatically, yet can be overridden with the environment variable `npm_execpath`.  
Autodetect: If called from `npm`/`npx` context, then the current _npm_ executable is utilized, otherwise it is managed by SHELL and PATH.

This tool does not do artificial deduplication. Therefore, if a component is installed multiple times, it appears multiple times in the SBOM result. Read more on the topic in the [dedicated docs "Component Deduplication"](https://github.com/CycloneDX/cyclonedx-node-npm/tree/main/docs/component_deduplication.md).

## Internals

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#internals)

This tool utilizes the [CycloneDX library](https://www.npmjs.com/package/@cyclonedx/cyclonedx-library) to generate the actual data structures, and serialize and validate them.  
Validation requires [transitive optional dependencies](https://github.com/CycloneDX/cyclonedx-javascript-library/blob/main/README.md#optional-dependencies).

This tool does **not** expose any additional _public_ API or classes - all code is intended to be internal and might change without any notice during version upgrades. However, the CLI is stable - you may call it programmatically like:

```js
const { execFileSync } = require('child_process')
const { constants: { MAX_LENGTH: BUFFER_MAX_LENGTH } } = require('buffer')
const sbom = JSON.parse(execFileSync(process.execPath, [
    '../path/to/this/package/bin/cyclonedx-npm-cli.js',
    '--output-format', 'JSON',
    '--output-file', '-'
    // additional CLI args
], { stdio: ['ignore', 'pipe', 'ignore'], encoding: 'buffer', maxBuffer: BUFFER_MAX_LENGTH }))
```

## Contributing

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#contributing)

Feel free to open issues, bugreports or pull requests.  
See the [CONTRIBUTING](https://github.com/CycloneDX/cyclonedx-node-npm/blob/main/CONTRIBUTING.md) file for details.

## License

[](https://www.npmjs.com/package/@cyclonedx/cyclonedx-npm#license)

Permission to modify and redistribute is granted under the terms of the Apache 2.0 license.  
See the [LICENSE](https://github.com/CycloneDX/cyclonedx-node-npm/blob/main/LICENSE) file for the full license.

### Keywords

- [CycloneDX](https://www.npmjs.com/search?q=keywords:CycloneDX)
- [SBOM](https://www.npmjs.com/search?q=keywords:SBOM)
- [BOM](https://www.npmjs.com/search?q=keywords:BOM)
- [inventory](https://www.npmjs.com/search?q=keywords:inventory)
- [bill-of-materials](https://www.npmjs.com/search?q=keywords:bill-of-materials)
- [software-bill-of-materials](https://www.npmjs.com/search?q=keywords:software-bill-of-materials)
- [component](https://www.npmjs.com/search?q=keywords:component)
- [dependency](https://www.npmjs.com/search?q=keywords:dependency)
- [package-url](https://www.npmjs.com/search?q=keywords:package-url)
- [PURL](https://www.npmjs.com/search?q=keywords:PURL)
- [spdx](https://www.npmjs.com/search?q=keywords:spdx)
- [node](https://www.npmjs.com/search?q=keywords:node)
- [npm](https://www.npmjs.com/search?q=keywords:npm)