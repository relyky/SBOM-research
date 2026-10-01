---
title: "anchore/syft: CLI tool and library for generating a Software Bill of Materials from container images and filesystems"
source: "https://github.com/anchore/syft"
author:
published:
created: 2026-10-01
description: "CLI tool and library for generating a Software Bill of Materials from container images and filesystems - anchore/syft"
tags:
  - "clippings"
---
[![Cute pink owl syft logo](https://user-images.githubusercontent.com/5199289/136844524-1527b09f-c5cb-4aa9-be54-5aa92a6086c1.png)](https://user-images.githubusercontent.com/5199289/136844524-1527b09f-c5cb-4aa9-be54-5aa92a6086c1.png)

## Syft

**A CLI tool and Go library for generating a Software Bill of Materials (SBOM) from container images and filesystems. Exceptional for vulnerability detection when used with a scanner like [Grype](https://github.com/anchore/grype).**

[![syft-demo](https://user-images.githubusercontent.com/590471/90277200-2a253000-de33-11ea-893f-32c219eea11a.gif)](https://user-images.githubusercontent.com/590471/90277200-2a253000-de33-11ea-893f-32c219eea11a.gif)

## Features

- Generates SBOMs for **container images**, **filesystems**, **archives** (see the docs for a full list of [supported scan targets](https://oss.anchore.com/docs/guides/sbom/scan-targets/))
- Supports dozens of packaging ecosystems (e.g. Alpine (apk), Debian (dpkg), RPM, Go, Python, Java, JavaScript, Ruby, Rust, PHP,.NET, and [many more](https://oss.anchore.com/docs/capabilities/all-packages/))
- Supports OCI, Docker, [Singularity](https://github.com/sylabs/singularity), and [more image formats](https://oss.anchore.com/docs/guides/sbom/scan-targets/)
- Works seamlessly with [Grype](https://github.com/anchore/grype) for vulnerability scanning
- Multiple output formats (**CycloneDX**, **SPDX**, **Syft JSON**, and [more](https://oss.anchore.com/docs/guides/sbom/formats/)) including the ability to [convert between SBOM formats](https://oss.anchore.com/docs/guides/sbom/conversion/)
- Create signed SBOM attestations using the [in-toto specification](https://github.com/in-toto/attestation/blob/main/spec/README.md)

> [!tip] Tip
> **New to Syft? Check out the [Getting Started guide](https://oss.anchore.com/docs/guides/sbom/getting-started/) for a walkthrough!**

## Installation

The quickest way to get up and going:

```
curl -sSfL https://get.anchore.io/syft | sudo sh -s -- -b /usr/local/bin
```

> [!tip] Tip
> **See [Installation docs](https://oss.anchore.com/docs/installation/syft/) for more ways to get Syft, including Homebrew, Docker, Scoop, Chocolatey, Nix, and more!**

## The basics

See the packages within a container image or directory:

```
# container image
syft alpine:latest

# directory
syft ./my-project
```

To get an SBOM, specify one or more output formats:

```
# SBOM to stdout
syft <image> -o cyclonedx-json

# Multiple SBOMs to files
syft <image> -o spdx-json=./spdx.json -o cyclonedx-json=./cdx.json
```

> [!tip] Tip
> **Check out the [Getting Started guide](https://oss.anchore.com/docs/guides/sbom/getting-started/)** to explore all of the capabilities and features.
> 
> **Want to know all of the ins-and-outs of Syft?** Check out the [CLI docs](https://oss.anchore.com/docs/reference/syft/cli/), [configuration docs](https://oss.anchore.com/docs/reference/syft/configuration/), and [JSON schema](https://oss.anchore.com/docs/reference/syft/json/latest/).

## Contributing

We encourage users to help make these tools better by [submitting issues](https://github.com/anchore/syft/issues) when you find a bug or want a new feature. Check out our [contributing overview](https://oss.anchore.com/docs/contributing/) and [developer-specific documentation](https://oss.anchore.com/docs/contributing/syft/) if you are interested in providing code contributions.

Syft development is sponsored by [Anchore](https://anchore.com/), and is released under the [Apache-2.0 License](https://github.com/anchore/syft?tab=Apache-2.0-1-ov-file). The [Syft logo](https://anchore.com/wp-content/uploads/2024/11/syft-logo.svg) by [Anchore](https://anchore.com/) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

For commercial support options with Syft or Grype, please [contact Anchore](https://get.anchore.com/contact/).

## Come talk to us!

The Syft Team holds regular community meetings online. All are welcome to join to bring topics for discussion.

- Check the [calendar](https://calendar.google.com/calendar/u/0/r?cid=Y182OTM4dGt0MjRtajI0NnNzOThiaGtnM29qNEBncm91cC5jYWxlbmRhci5nb29nbGUuY29t) for the next meeting date.
- Add items to the [agenda](https://docs.google.com/document/d/1ZtSAa6fj2a6KRWviTn3WoJm09edvrNUp4Iz_dOjjyY8/edit?usp=sharing) (join [this group](https://groups.google.com/g/anchore-oss-community) for write access to the [agenda](https://docs.google.com/document/d/1ZtSAa6fj2a6KRWviTn3WoJm09edvrNUp4Iz_dOjjyY8/edit?usp=sharing))
- See you there!