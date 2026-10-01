---
title: Overview of Anchore Open Source tools
source: https://oss.anchore.com/docs/projects/
author:
published:
created: 2026-10-01
description: Overview of Anchore Open Source tools
tags:
  - clippings
---
We maintain three popular command-line tools, some libraries, and supporting utilities. Most are written in Go, with a few in Python. They are all released under the Apache-2.0 license. For the full list, see our [GitHub org](https://github.com/orgs/anchore/repositories).

Anchore’s tools follow a simple workflow: search and raise up evidence in the form of a Software Bill of Materials (SBOM) using **Syft**, then analyze that SBOM with **Grype** for security vulnerabilities and **Grant** for open source license compliance.

![[Anchore tools flow.png]]

This modular approach lets you generate the SBOM once with Syft, then use Grype and Grant independently to scan for different types of risk.

#### ![Syft logo](https://oss.anchore.com/images/logos/syft/apple-touch-icon-60x60.png) Syft[](https://oss.anchore.com/docs/projects/#syft)

##### SBOM Generator and library

**Syft** (pronounced like _sift_) is an open-source command-line tool and Go library. Its primary function is to scan container images, file systems, and archives to automatically generate a Software Bill of Materials, making it easier to understand the composition of software.  

[GitHub Repo](https://github.com/anchore/syft) | [Installing](https://oss.anchore.com/docs/installation/syft) | [SBOM Generation Guide](https://oss.anchore.com/docs/guides/sbom/getting-started)

#### ![Grype logo](https://oss.anchore.com/images/logos/grype/apple-touch-icon-60x60.png) Grype[](https://oss.anchore.com/docs/projects/#grype)

##### Vulnerability Scanner

**Grype** (rhymes with _hype_) is an open-source vulnerability scanner specifically designed to analyze container images and filesystems. It works by comparing the software components it finds against a database of known vulnerabilities, providing a report of potential risks so they can be addressed.

[GitHub Repo](https://github.com/anchore/grype) | [Installing](https://oss.anchore.com/docs/installation/grype) | [Vulnerability Scanning Guide](https://oss.anchore.com/docs/guides/vulnerability/getting-started)

#### ![Grant logo](https://oss.anchore.com/images/logos/grant/apple-touch-icon-60x60.png) Grant[](https://oss.anchore.com/docs/projects/#grant)

##### License Scanner

**Grant** is an open-source command-line tool designed to discover and report on the software licenses present in container images, SBOM documents, or filesystems. It helps users understand the licenses of their software dependencies and can check them against user-defined policies to ensure compliance.

[GitHub Repo](https://github.com/anchore/grant) | [Installing](https://oss.anchore.com/docs/installation/grant) | [License Scanning Guide](https://oss.anchore.com/docs/guides/license/getting-started)

Last modified September 29, 2026
