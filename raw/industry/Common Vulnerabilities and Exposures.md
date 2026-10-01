---
title: "Common Vulnerabilities and Exposures"
source: "https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures"
author:
  - "[[Wikipedia]]"
published: 2006-02-09
created: 2026-10-01
description:
tags:
  - "clippings"
---
![](https://thumb.wikimedia.org/wikipedia/commons/thumb/a/a7/Common_Vulnerabilities_and_Exposures_logo.svg/250px-Common_Vulnerabilities_and_Exposures_logo.svg.png?utm_source=en.wikipedia.org&utm_campaign=parser&utm_content=thumbnail)

Logo

The **Common Vulnerabilities and Exposures** (**CVE**) system, originally **Common Vulnerability Enumeration**,[^1] provides a reference method for publicly known [information-security](https://en.wikipedia.org/wiki/Information_security "Information security") [vulnerabilities](https://en.wikipedia.org/wiki/Vulnerability_\(computing\) "Vulnerability (computing)") and exposures.[^2] The United States' Homeland Security Systems Engineering and Development Institute FFRDC, operated by [The MITRE Corporation](https://en.wikipedia.org/wiki/The_MITRE_Corporation "The MITRE Corporation"), maintains the system, with funding from the US [National Cyber Security Division](https://en.wikipedia.org/wiki/National_Cyber_Security_Division "National Cyber Security Division") of the [US Department of Homeland Security](https://en.wikipedia.org/wiki/US_Department_of_Homeland_Security "US Department of Homeland Security").[^3] The system was officially launched for the public in September 1999.[^4]

The [Security Content Automation Protocol](https://en.wikipedia.org/wiki/Security_Content_Automation_Protocol "Security Content Automation Protocol") uses CVE, and CVE IDs are listed on MITRE's system as well as the basis for the US [National Vulnerability Database](https://en.wikipedia.org/wiki/National_Vulnerability_Database "National Vulnerability Database").[^5]

## CVE identifiers

MITRE Corporation's documentation defines CVE Identifiers (also called "CVE names", "CVE numbers", "CVE-IDs", and "CVEs") as unique, common identifiers for publicly known information-security vulnerabilities in publicly released software packages. Historically, CVE identifiers originally had a status of "candidate" ("CAN-") and could then be promoted to entries ("CVE-"), but this practice was ended in 2005 [^6] [^7] and all identifiers are now assigned as CVEs. The assignment of a CVE number is not a guarantee that it will become an official CVE entry (e.g., a CVE may be improperly assigned to an issue which is not a security vulnerability, or which duplicates an existing entry). If found not to meet criteria, MITRE or a CVE Numbering Authority (CNA) can summarily place the entry into REJECTED status.

CVEs are assigned by a CVE Numbering Authority (CNA).[^8] While some vendors acted as a CNA before, the name and designation was not created until 1 February 2005.[^9] There are four primary types of CVE number assignments:

1. The [MITRE Corporation](https://en.wikipedia.org/wiki/MITRE_Corporation "MITRE Corporation") functions as Editor and Primary CNA
2. Various CNAs assign CVE numbers for their own products (e.g., Microsoft, Oracle, HP, Red Hat)
3. A third-party coordinator such as [CERT Coordination Center](https://en.wikipedia.org/wiki/CERT_Coordination_Center "CERT Coordination Center") may assign CVE numbers for products not covered by other CNAs
4. Researchers, in one case, have been granted the CNA role.[^10]

When investigating a vulnerability or potential vulnerability it helps to acquire a CVE number early on. CVE numbers may not appear in the MITRE or NVD databases for some time (days, weeks, months or potentially years) due to issues that are embargoed (the CVE number has been assigned but the issue has not been made public), or historically in cases where the entry is not researched and written up by MITRE due to resource issues. The benefit of early CVE candidacy is that all future correspondence and coordination can refer to the CVE number to ensure all parties are referring to the same vulnerability. Information on getting CVE identifiers for issues with open source projects is available from [Red Hat](https://en.wikipedia.org/wiki/Red_Hat "Red Hat") [^11] and [GitHub](https://en.wikipedia.org/wiki/GitHub "GitHub").[^12]

CVEs are for software that has been publicly released; this can include betas and other pre-release versions if they are widely used. [Commercial software](https://en.wikipedia.org/wiki/Commercial_software "Commercial software") is included in the "publicly released" category, but custom-built software that is not distributed would historically not be given a CVE. For the first two decades of the program, services (e.g., a Web-based email provider) are not assigned CVEs for vulnerabilities found in the service (e.g., an XSS vulnerability) unless the issue exists in an underlying software product that is publicly distributed. Official rules have not been published regarding this change but some CNAs including MITRE have begun assigning CVEs to service-based vulnerabilities as far back as 2000.[^13]

## CVE data fields

The CVE database contains several fields:

### Description

This is a standardized text description of the issue(s). One common entry is:

> \*\* RESERVED \*\* This candidate has been reserved by an organization or individual that will use it when announcing a new security problem. When the candidate has been publicized, the details for this candidate will be provided.

This means that the entry number has been reserved by Mitre for an issue or a CNA has reserved the number. So when a CNA requests a block of CVE numbers in advance (e.g., Red Hat currently requests CVEs in blocks of 500), the CVE number will be marked as reserved even though the CVE itself may not be assigned by the CNA for some time. Until the CVE is assigned, Mitre is made aware of it (i.e., the embargo passes and the issue is made public), and Mitre has researched the issue and written a description of it, entries will show up as "\*\* RESERVED \*\*".

### Creation date

This is the date the entry was created. For CVEs assigned directly by Mitre, this is the date Mitre created the CVE entry. For CVEs assigned by CNAs (e.g., Microsoft, Oracle, HP, Red Hat) this is also the date that was created by Mitre, not by the CNA. When a CNA requests a block of CVE numbers in advance, the entry date is when the block was assigned to the CNA.

### Obsolete fields

The following fields were previously used in CVE records, but are no longer used.

- Phase: The phase the CVE is in (e.g., CAN, CVE).
- Votes: Previously board members would vote yea or nay on whether or not the CAN should be accepted and turned into a CVE.
- Comments: Comments on the issue.
- Proposed: When the issue was first proposed.

## Changes to syntax

In order to support CVE IDs beyond CVE-YEAR-9999 (an issue known as the 'CVE10k problem' [^14]) a change was made to the CVE syntax in 2014 and took effect on 13 January 2015.[^15]

The new CVE-ID syntax is variable length and includes:

CVE prefix + Year + Arbitrary Digits

The variable-length arbitrary digits begin at four fixed digits and expand with arbitrary digits only when needed in a calendar year; for example, CVE-YYYY-NNNN and if needed CVE-YYYY-NNNNN, CVE-YYYY-NNNNNN, and so on. The schema is compatible with previously assigned CVE-IDs, which all include a minimum of four digits.

## Search CVE identifiers

The Mitre CVE database can be searched at the [CVE List Search](https://cve.mitre.org/cve/search_cve_list.html), and the NVD CVE database can be searched at [Search CVE and CCE Vulnerability Database](https://web.nvd.nist.gov/view/vuln/search).

## CVE usage

CVE identifiers are intended for use with respect to identifying vulnerabilities:

> Common Vulnerabilities and Exposures (CVE) is a dictionary of common names (i.e., CVE Identifiers) for publicly known information security vulnerabilities. CVE's common identifiers make it easier to share data across separate network security databases and tools, and provide a baseline for evaluating the coverage of an organization's security tools. If a report from one of your security tools incorporates CVE Identifiers, you may then quickly and accurately access fix information in one or more separate CVE-compatible databases to remediate the problem.[^16]

Users who have been assigned a CVE identifier for a vulnerability are encouraged to ensure that they place the identifier in any related security reports, web pages, emails, and so on.

## CVE assignment issues

Per section 7 of the CNA Rules, a vendor which received a report about a [security vulnerability](https://en.wikipedia.org/wiki/Security_vulnerability "Security vulnerability") has full discretion in regards to it.[^17] This can lead to a [conflict of interest](https://en.wikipedia.org/wiki/Conflict_of_interest "Conflict of interest") as a vendor may attempt to leave flaws unpatched by denying a CVE assignment at first place – a decision which Mitre can't reverse. The "!CVE" (not CVE) project, announced in 2023, aims to collect vulnerabilities that are denied by vendors, so long as they are considered valid by a panel of experts from the project.[^18]

CVE identifiers have been awarded for bogus issues and issues without security consequences.[^19] In response, a number of open-source projects have themselves applied to become the CVE Numbering Authority (CNA) of their own project.[^20]

## 2025 funding issues

On 15 April 2025, it was reported that the contract between MITRE and the US government, set to expire the day after,[^21] would be allowed to expire. Reports stated that the expiration of the contract would bring an end to the operational arm of the CVE program, including assigning new CVEs, while the database would remain accessible via [GitHub](https://en.wikipedia.org/wiki/GitHub "GitHub").[^22]

Just prior to its expiration, the contract was extended for 11 months, averting the shutdown of the program.[^23]

Following the risk of funding expiration on March 16, 2026, the acting director of CISA Nick Andersen stated that the program is now being fully funded. Pete Allor, the co-founder of CVE Foundation, reported that the CVE programs funding had been restructured from a discretionary item to being one of the core programs to be funded.[^24]

[^1]: ["CVE - Towards a Common Enumeration of Vulnerabilities"](https://web.archive.org/web/20250418034843/https://cve.mitre.org/docs/docs-2000/cerias.html). 18 April 2025. Archived from [the original](https://cve.mitre.org/docs/docs-2000/cerias.html) on 18 April 2025. Retrieved 29 April 2025.

[^2]: Wu, Xiaoxue; Zheng, Wei; Chen, Xiang; Wang, Fang; Mu, Dejun (2020). ["CVE-assisted large-scale security bug report dataset construction method"](https://linkinghub.elsevier.com/retrieve/pii/S0164121219302304). *Journal of Systems and Software*. **160** 110456. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1016/j.jss.2019.110456](https://doi.org/10.1016%2Fj.jss.2019.110456). [S2CID](https://en.wikipedia.org/wiki/S2CID_\(identifier\) "S2CID (identifier)") [209056007](https://api.semanticscholar.org/CorpusID:209056007). Retrieved 24 October 2022.

[^3]: ["CVE – Common Vulnerabilities and Exposures"](https://cve.mitre.org/). [Mitre Corporation](https://en.wikipedia.org/wiki/Mitre_Corporation "Mitre Corporation"). 3 July 2007. [Archived](https://web.archive.org/web/20201219060633/https://cve.mitre.org/) from the original on 19 December 2020. Retrieved 18 June 2009. CVE is sponsored by the National Cyber Security Division of the U.S. Department of Homeland Security.

[^4]: ["CVE - History"](https://cve.mitre.org/about/history.html). *cve.mitre.org*. [Archived](https://web.archive.org/web/20200108035610/https://cve.mitre.org/about/history.html) from the original on 8 January 2020. Retrieved 25 March 2020.

[^5]: ["CVE - Common Vulnerabilities and Exposures (CVE)"](https://cve.mitre.org/). *cve.mitre.org*. [Archived](https://web.archive.org/web/20130407115613/https://cve.mitre.org/) from the original on 7 April 2013. Retrieved 8 April 2013.

[^6]: ["CVE - Frequently Asked Questions"](https://cve.mitre.org/about/faqs.html#cve_list_retire_term_cve). *cve.mitre.org*. [Archived](https://web.archive.org/web/20180410002016/http://cve.mitre.org/about/faqs.html#cve_list_retire_term_cve) from the original on 10 April 2018. Retrieved 1 September 2021.

[^7]: Kouns, Jake (13 August 2009). ["Reviewing(4) CVE"](https://vulndb.wordpress.com/2009/08/16/reviewing4-cve/). *OSVDB: Everything is Vulnerable*. [Archived](https://web.archive.org/web/20210901151014/https://vulndb.wordpress.com/2009/08/16/reviewing4-cve/) from the original on 1 September 2021. Retrieved 1 September 2021.

[^8]: ["CVE - CVE Numbering Authorities"](https://www.cve.org/PartnerInformation/ListofPartners). [MITRE Corporation](https://en.wikipedia.org/wiki/MITRE_Corporation "MITRE Corporation"). 1 February 2015. Retrieved 5 March 2024.

[^9]: ["CVE - CVE Blog "Our CVE Story: Ancient History of the CVE Program – Did the Microsoft Security Response Center have Precognition?" (guest author)"](https://cve.mitre.org/blog/September222020_Our_CVE_Story_Ancient_History_of_the_CVE_Program_-_Did_the_Microsoft_Security_Response_Center_have_Precognition.html). *cve.mitre.org*. Retrieved 17 September 2021.

[^10]: ["CVE - CVE Blog "My CVE Story: How I Became the CVE Program's First Vulnerability Researcher CNA" (guest author)"](https://web.archive.org/web/20210315211105/https://cve.mitre.org/blog/March152021_My_CVE_Story_How_I_Became_the_CVE_Programs_First_Vulnerability_Researcher_CNA.html). 15 March 2021. Archived from [the original](https://cve.mitre.org/blog/March152021_My_CVE_Story_How_I_Became_the_CVE_Programs_First_Vulnerability_Researcher_CNA.html) on 15 March 2021. Retrieved 29 April 2025.

[^11]: ["CVE OpenSource Request HOWTO"](https://github.com/RedHatProductSecurity/CVE-HOWTO). [Red Hat Inc.](https://en.wikipedia.org/wiki/Red_Hat_Inc. "Red Hat Inc.") 14 November 2016. Retrieved 29 May 2019. There are several ways to make a request depending on what your requirements are:

[^12]: ["About GitHub Security Advisories"](https://docs.github.com/en/code-security/security-advisories/about-github-security-advisories#cve-identification-numbers). [GitHub](https://en.wikipedia.org/wiki/GitHub "GitHub"). [Archived](https://web.archive.org/web/20211223082247/https://docs.github.com/en/code-security/security-advisories/about-github-security-advisories#cve-identification-numbers) from the original on 23 December 2021. Retrieved 23 December 2021. GitHub Security Advisories builds upon the foundation of the Common Vulnerabilities and Exposures (CVE) list

[^13]: ["CVE - CVE-2000-0081"](https://web.archive.org/web/20211204064603/https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2000-0081). 4 December 2021. Archived from [the original](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2000-0081) on 4 December 2021. Retrieved 29 April 2025.

[^14]: Christey, Steven M. (12 January 2007). ["CVE - The CVE-10K Problem"](https://cve.mitre.org/data/board/archives/2007-01/msg00000.html). *cve.mitre.org*. The [MITRE Corporation](https://en.wikipedia.org/wiki/MITRE_Corporation "MITRE Corporation"). Retrieved 25 November 2023.

[^15]: ["CVE - CVE ID Syntax Change"](https://cve.mitre.org/cve/identifiers/syntaxchange.html). *cve.mitre.org*. 13 September 2016.

[^16]: ["CVE - About CVE"](https://cve.mitre.org/about/). *cve.mitre.org*. Retrieved 28 July 2015.

[^17]: ["CVE Numbering Authority Rules - Assignment Rules"](https://www.cve.org/Resources/Roles/Cnas/CNA_Rules_v3.0.pdf) (PDF). The MITRE Corporation. 1 February 2020. pp. 13–15. [Archived](https://web.archive.org/web/20231207180342/https://www.cve.org/Resources/Roles/Cnas/CNA_Rules_v3.0.pdf) (PDF) from the original on 7 December 2023. Retrieved 6 December 2023.

[^18]: Edge, Jake (5 December 2023). ["Supplementing CVEs with!CVEs"](https://lwn.net/Articles/953738/). *lwn.net*. [Archived](https://web.archive.org/web/20240221004340/https://lwn.net/Articles/953738/) from the original on 21 February 2024. Retrieved 21 February 2024.

[^19]: Edge, Jake (13 September 2023). ["The bogus CVE problem"](https://lwn.net/Articles/944209/). *lwn.net*.

[^20]: ["A turning point for CVE numbers"](https://lwn.net/Articles/961978/). *LWN.net*. 14 February 2024. [Archived](https://web.archive.org/web/20240222175503/https://lwn.net/Articles/961978/) from the original on 22 February 2024. Retrieved 21 February 2024.

[^21]: ["CONTRACT to THE MITRE CORPORATION"](https://www.usaspending.gov/award/CONT_AWD_70RCSJ24FR0000018_7001_70RSAT20D00000001_7001). *www.usaspending.gov*. Retrieved 16 April 2025.

[^22]: Bradley, Tony (15 April 2025). ["Cybersecurity World On Edge As CVE Program Prepares To Go Dark"](https://www.forbes.com/sites/tonybradley/2025/04/15/cybersecurity-world-on-edge-as-cve-program-prepares-to-go-dark/?ctpv=searchpage). *Forbes*. [Archived](https://web.archive.org/web/20250717103742/https://www.forbes.com/sites/tonybradley/2025/04/15/cybersecurity-world-on-edge-as-cve-program-prepares-to-go-dark/?ctpv=searchpage) from the original on 17 July 2025. Retrieved 16 April 2025.

[^23]: Brunfield, Cynthia (16 April 2025). ["CVE program averts swift end after CISA executes 11-month contract extension"](https://www.csoonline.com/article/3963190/cve-program-faces-swift-end-after-dhs-fails-to-renew-contract-leaving-security-flaw-tracking-in-limbo.html). *CSO Online*. [Archived](https://web.archive.org/web/20250415234419/https://www.csoonline.com/article/3963190/cve-program-faces-swift-end-after-dhs-fails-to-renew-contract-leaving-security-flaw-tracking-in-limbo.html) from the original on 15 April 2025. Retrieved 16 April 2025.

[^24]: Brunfield, Cynthia (9 March 2026). ["CVE program funding secured, easing fears of repeat crisis"](https://www.csoonline.com/article/4142600/cve-program-funding-secured-easing-fears-of-repeat-crisis.html). *CSO Online*. Retrieved 5 May 2026.