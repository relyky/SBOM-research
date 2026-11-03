---
title: "What is VEX?"
source: "https://sbom.se/en/vulnerabilities/what-is-vex"
author:
  - "[[Bitfront AB]]"
published: 2025-02-07
created: 2026-11-03
description: "A vulnerability scan against an SBOM often returns findings that cannot be exploited in the product at hand. With VEX the supplier states a status for each vulnerability, so that the recipient can prioritise correctly."
tags:
  - "clippings"
---
VEX (Vulnerability Exploitability eXchange) states whether a product is affected by a specific vulnerability

VEX (Vulnerability Exploitability eXchange) is a machine-readable statement from a supplier about whether a product is affected by a specific vulnerability.

## The problem VEX solves

When an SBOM is compared against a vulnerability database, the result is a list of all known vulnerabilities in the components. Many of them cannot be exploited in that particular product. The vulnerable function may never be called, or the supplier may already have added a protection.

The recipient of an SBOM can rarely decide that alone. The supplier can. VEX is the format for giving that answer.

## Status

A VEX statement gives one of four statuses for a vulnerability in a product:

| Status | Meaning |
| --- | --- |
| Not Affected | The product is not affected. No action is required. |
| Affected | The product is affected. Action is recommended. |
| Fixed | This version of the product contains a fix. |
| Under Investigation | It is not yet known whether the product is affected. An update will follow. |

The status Not Affected must be justified. The usual justifications are:

- the component is not present in the product
- the vulnerable code is not present
- the vulnerable code is never executed
- the vulnerable code cannot be controlled by an attacker
- protections already in the product prevent exploitation

The status Affected must come with a recommended action, for example updating to a specific version.

## VEX and SBOM

The SBOM answers which components the product contains. VEX answers which of the vulnerabilities in those components matter.

The two documents have different lifetimes. The SBOM for a version does not change. VEX is updated when new vulnerabilities become known and when assessments change. That is why they are usually shared as separate documents.

## VEX and VDR

A [VDR (Vulnerability Disclosure Report)](https://sbom.se/en/vulnerabilities/what-is-vdr) lists all known vulnerabilities in a product together with the supplier's analysis. VEX is mainly used to state which vulnerabilities do not affect the product. A VDR can contain VEX information.

## Formats

Three formats for VEX are in general use:

- **CSAF.** The OASIS standard Common Security Advisory Framework has a profile for VEX.
- **CycloneDX.** VEX can be in the same document as the SBOM or in a separate document that points to it. CycloneDX uses its own names for the statuses, such as `not_affected`, `exploitable`, `resolved` and `in_triage`.
- **OpenVEX.** A standalone, minimal format from OpenSSF [^1].

CISA has published minimum requirements for VEX that all three formats can meet. The document is listed under References.

[^1]: [OpenVEX](https://openssf.org/projects/openvex/), a project within the Open Source Security Foundation (OpenSSF).