---
title: "anchore/grype: A vulnerability scanner for container images and filesystems"
source: "https://github.com/anchore/grype"
author:
published:
created: 2026-10-01
description: "A vulnerability scanner for container images and filesystems - anchore/grype"
tags:
  - "clippings"
---
[![Grype logo](https://user-images.githubusercontent.com/5199289/136855393-d0a9eef9-ccf1-4e2b-9d7c-7aad16a567e5.png)](https://user-images.githubusercontent.com/5199289/136855393-d0a9eef9-ccf1-4e2b-9d7c-7aad16a567e5.png)

## Grype

**A vulnerability scanner for container images and filesystems.**

[![grype-demo](https://user-images.githubusercontent.com/590471/90276236-9868f300-de31-11ea-8068-4268b6b68529.gif)](https://user-images.githubusercontent.com/590471/90276236-9868f300-de31-11ea-8068-4268b6b68529.gif)

## Features

- Scan **container images**, **filesystems**, and **SBOMs** for known vulnerabilities (see the docs for a full list of [supported scan targets](https://oss.anchore.com/docs/guides/vulnerability/scan-targets/))
- Supports major OS package ecosystems (Alpine, Debian, Ubuntu, RHEL, Oracle Linux, Amazon Linux, and [more](https://oss.anchore.com/docs/capabilities/all-os/))
- Supports language-specific packages (Ruby, Java, JavaScript, Python,.NET, Go, PHP, Rust, and [more](https://oss.anchore.com/docs/capabilities/all-packages/))
- Supports Docker, OCI, and [Singularity](https://github.com/sylabs/singularity) image formats
- Threat & risk prioritization with **EPSS**, **KEV**, and **risk scoring** (see [interpreting the results docs](https://oss.anchore.com/docs/guides/vulnerability/interpreting-results/))
- [OpenVEX](https://github.com/openvex) support for filtering and augmenting scan results

> [!tip] Tip
> New to Grype? Check out the [Getting Started guide](https://oss.anchore.com/docs/guides/vulnerability/getting-started/) for a walkthrough!

## Installation

The quickest way to get up and going:

```
curl -sSfL https://get.anchore.io/grype | sudo sh -s -- -b /usr/local/bin
```

> [!tip] Tip
> See [Installation docs](https://oss.anchore.com/docs/installation/grype/) for more ways to get Grype, including Homebrew, Docker, Chocolatey, MacPorts, and more!

## The basics

Scan a container image or directory for vulnerabilities:

```
# container image
grype alpine:latest

# directory
grype ./my-project
```

Scan an SBOM for even faster vulnerability detection:

```
# scan a Syft SBOM
grype sbom:./sbom.json

# pipe an SBOM into Grype
cat ./sbom.json | grype
```

> [!tip] Tip
> Check out the [Getting Started guide](https://oss.anchore.com/docs/guides/vulnerability/getting-started/) to explore all of the capabilities and features.
> 
> Want to know all of the ins-and-outs of Grype? Check out the [CLI docs](https://oss.anchore.com/docs/reference/grype/cli/) and [configuration docs](https://oss.anchore.com/docs/reference/grype/configuration/).

## Contributing

We encourage users to help make these tools better by [submitting issues](https://github.com/anchore/grype/issues) when you find a bug or want a new feature. Check out our [contributing overview](https://oss.anchore.com/docs/contributing/) and [developer-specific documentation](https://oss.anchore.com/docs/contributing/grype/) if you are interested in providing code contributions.

Grype development is sponsored by [Anchore](https://anchore.com/), and is released under the [Apache-2.0 License](https://github.com/anchore/grype?tab=Apache-2.0-1-ov-file). The [Grype logo](https://anchore.com/wp-content/uploads/2024/11/grype-logo.svg) by [Anchore](https://anchore.com/) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

For commercial support options with Syft or Grype, please [contact Anchore](https://get.anchore.com/contact/).

## Come talk to us!

The Grype Team holds regular community meetings online. All are welcome to join to bring topics for discussion.

- Check the [calendar](https://calendar.google.com/calendar/u/0/r?cid=Y182OTM4dGt0MjRtajI0NnNzOThiaGtnM29qNEBncm91cC5jYWxlbmRhci5nb29nbGUuY29t) for the next meeting date.
- Add items to the [agenda](https://docs.google.com/document/d/1ZtSAa6fj2a6KRWviTn3WoJm09edvrNUp4Iz_dOjjyY8/edit?usp=sharing) (join [this group](https://groups.google.com/g/anchore-oss-community) for write access to the [agenda](https://docs.google.com/document/d/1ZtSAa6fj2a6KRWviTn3WoJm09edvrNUp4Iz_dOjjyY8/edit?usp=sharing))
- See you there!