---
title: "Software Identification (SWID) Tagging"
source: "https://csrc.nist.gov/projects/software-identification-swid"
author:
published:
created: 2026-10-01
description: "Software is vital to our economy and way of life as part of the critical infrastructure for the modern world. Too often cost and complexity make it difficult to manage software effectively, leaving the software open for attack. To properly manage software,..."
tags:
  - "clippings"
---
## Software Identification (SWID) Tagging SWID

### Overview

Software is vital to our economy and way of life as part of the critical infrastructure for the modern world. Too often cost and complexity make it difficult to manage software effectively, leaving the software open for attack. To properly manage software, enterprises need to maintain accurate software inventories of their managed devices in support of higher-level business, information technology, and cybersecurity functions. Accurate software inventories help an enterprise to:

- **Manage compliance with software license agreements.** Knowing what software is installed and used can help an enterprise to avoid paying for unneeded licenses.
- **Ensure that all software assets in use conform to organizational policy.** Reducing and controlling an organization’s software footprint can reduce the surface area of attack.
- **Verify that all deployed software assets are updated and free of known exploitable weaknesses.** Ensuring all software is patched and updated is an effective way to counter cyber threats.
- **Support assessing that all deployed software assets are configured according to their organizations’ security policies.** Configuring defensive mechanisms, reducing services exposed, and restricting features used within software can also further reduce attack surface, and can harden systems against attacks. Accurate software inventories identify critical software assets so that assessments can be targeted and tracked.
- **Plan software investments and resources needed to support upgrades to and replacement of legacy systems.** Knowledge of what commercial and custom software the enterprise uses can assist with budgeting for IT investments.

While some vendors provide tools to manage licenses, updates, patches, and configurations for their products, organizations need to monitor and use many such tools to address the range of products their enterprises deploy. This multiplicity of tools creates an environment where human error and a lack of resources can limit an enterprise’s ability to support the active management of software, preventing timely patching, and allowing configurations to drift and software licenses to be inefficiently utilized. Instead, a single mechanism is needed that can help organizations to understand the state of all software across their enterprise regardless of vendor.

Software Identification (SWID) Tags, defined by the ISO/IEC 19770-2:2015 standard, promise to be an important step towards such a goal. SWID Tags provide a transparent way for organizations to track the software installed on their managed devices. SWID Tag files contain descriptive information about a specific release of a software product. The SWID standard defines a [lifecycle](https://csrc.nist.gov/projects/software-identification-swid/lifecycle) where a SWID Tag is added to an endpoint as part of the software product’s installation process and deleted by the product’s uninstall process. When this lifecycle is followed, the presence of a given SWID Tag corresponds directly to the presence of the software product that the Tag describes. The National Institute of Standards and Technology recommends adoption of the SWID Tag standard by software producers, and multiple standards bodies, including the Trusted Computing Group (TCG) and the Internet Engineering Task Force (IETF) utilize SWID Tags in their standards.

NIST plans to continue to promote the incorporation of the SWID Tag standard and [associated guidelines](https://csrc.nist.gov/projects/software-identification-swid/guidelines) in other international consensus standards (such as IETF and TCG efforts), the broad adoption of SWID tagging within the software community, and the use of SWID Tag information in the creation of cybersecurity reference data and [security automation](https://csrc.nist.gov/topics/security-and-privacy/security-programs-and-operations/security-automation) content. Additionally, NIST is working to incorporate SWID Tag data into the vulnerability dataset provided by [National Vulnerability Database](https://csrc.nist.gov/projects/national-vulnerability-database) (NVD), and has incorporated use of SWID Tag data into [Security Content Automation Protocol](https://csrc.nist.gov/projects/security-content-automation-protocol) (SCAP) version 1.3. These efforts are part of the Software Identification (SWID) Tagging project, which is an initiative of the Computer Security Division’s Security Automation Program (SAP). The SAP is focused on standardizing the exchange of security posture information supporting the management of software, vulnerabilities, patches, and secure configurations for computing devices.

#### Contacts

#### Group

[Software Security Group](https://csrc.nist.gov/Groups/Computer-Security-Division/Software-Security-Group)

Created, Updated April 13, 2026