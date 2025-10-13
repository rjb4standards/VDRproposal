# VDRproposal
Vulnerability Disclosure Report (VDR) Proposed Standard https://github.com/ossf/wg-vulnerability-disclosures/issues/172

### Problem Statement:
Frequently, users do not know precisely which products in their ecosystems are affected by a vulnerability/CVE. i.e. Log4J - how does a user know if any of the products running in their production environments are affected by Log4J. 

End users MUST reach out to their product manufacturers to know, with certainty, if their running products are affected by a vulnerability using names they are familiar with. [Typically a CVE entry lists "Known affected products" using CPE identifiers which are very cryptic and difficult to correlate to the product names that users are familiar with](https://nvd.nist.gov/vuln/detail/CVE-2025-20363). Users need information about product vulnerabilities, particularly remediation, using product names users are familiar with, such as the products listed on an invoice or in a proposal, in order to make effective risk decisions and to use software products and services more securely.

To satisfy this user need to correlate CVE's to products running in user/customer ecosystems, product producers provide their customers/users with product Vulnerability Disclosure Reports (VDR) in a machine readable, proprietary format, as seen in these two examples:
[Cisco Product Vulnerability Disclosure Report (VDR) Generator](https://sec.cloudapps.cisco.com/security/center/softwarechecker.x)
[Actual Cisco Product VDR sample is available here - click Export Selected for machine readable VDR in CSV format](https://sec.cloudapps.cisco.com/security/center/softwarechecker.x?productSelected=ASA&selectedMethod=A&captchaPage=true&platformCode=277437&versionNamesSelected=9.16.4&allAdvisoriesSelectedByTree=N&advisoryType=0&iosBundleId=cisco-sa-20250924-bundle&isFewCheckBoxChecked1=false&isNoneCheckBoxsChecked1=true#~onStep3)
Here is an example of[ a Cisco Product VDR showing "No known vulnerabilities"](https://sec.cloudapps.cisco.com/security/center/softwarechecker.x?productSelected=ASA&selectedMethod=A&captchaPage=true&platformCode=277437&versionNamesSelected=9.16.4.85&allAdvisoriesSelectedByTree=N&advisoryType=0&iosBundleId=cisco-sa-20250924-bundle&isFewCheckBoxChecked1=false&isNoneCheckBoxsChecked1=true#~onStep3)

[Palo Alto product Vulnerability Disclosure Report (VDR)](https://security.paloaltonetworks.com/)

Each example gives a customer the ability to select a product name and version that users are familiar with to generate the VDR, which can be downloaded in a machine readable format (CSV file). Each of these CSV files contains **up to date vulnerability information** identified with a single product, which enables a software consumer to answer the question: **"What is the vulnerability status of MY product, as of right now?"**

These proprietary VDR's make it difficult for product consumers to automate their risk management and vulnerability detection processes using VDR. A standard, machine readable VDR format would give software consumers the ability to rapidly close the window of opportunity that criminals exploit when a new vulnerability is reported, as described in [this article ](https://www.energycentral.com/intelligent-utility/post/closing-the-cyber-risk-window-of-opportunity-that-criminals-exploit-DufDnCMWayEym24)

"Enterprise attack surfaces continue to expand rapidly, with more than 20,000 new vulnerabilities disclosed in the first half of 2025, straining already hard-pressed security teams." **A paradigm shift is underway as this article clearly shows;** https://www.csoonline.com/article/4065137/cisos-advised-to-rethink-vulnerability-management-as-exploits-sharply-rise.html


### Proposal

Initiate a work effort to develop a standard machine readable VDR format following the recommendations provided by the NIST SP 800-161r1 RA-5 standard data model [described in this article](https://www.energycentral.com/intelligent-utility/post/what-is-a-nist-sbom-vulnerability-disclosure-report-vdr-C1A40dhnYZxARMa) in alignment with [IEC 29147](https://www.iso.org/obp/ui/#iso:std:iso-iec:29147:ed-2:v1:en) and [FedRAMP Vulnerability Detection and Response (VDR) standards](https://github.com/FedRAMP/docs/blob/main/markdown/FRMR.VDR.vulnerability-detection-and-response.md)

Business Cyber Guardian (TM) has created an open source VDR format based on the NIST SP 800-161r1 RA-5 standard, [defined by an XML schema](https://raw.githubusercontent.com/rjb4standards/REA-Products/refs/heads/master/SAGVulnDisclosure_V214.xsd), a production example of this VDR format is [available in JSON format for an open source product](https://raw.githubusercontent.com/rjb4standards/CISASAGReader/refs/heads/main/CISASAGReader-V1_0_4-VDR.json) maintained by Business Cyber Guardian (TM). [CycloneDX SBOM standards already provide VDR support following NIST standards, using the implicit VDR model.](https://cyclonedx.org/capabilities/vdr/). The Business Cyber Guardian SAG-PM software supports both VDR formats.

This would enable the replacement of "cpe identifiers" typically listed in a CVE display, [such as CVE-2025-20363](https://nvd.nist.gov/vuln/detail/CVE-2025-20363), with direct [links to Product Manufacturer VDR data for affected products using product names familiar to end users](https://sec.cloudapps.cisco.com/security/center/softwarechecker.x?productSelected=ASA&selectedMethod=A&captchaPage=true&platformCode=277437&versionNamesSelected=9.16.4&allAdvisoriesSelectedByTree=N&advisoryType=0&iosBundleId=cisco-sa-20250924-bundle&isFewCheckBoxChecked1=false&isNoneCheckBoxsChecked1=true#~onStep3), eliminating a cpe search to find affected products. CPE identifiers contained in CVE Known Affected Software lists could be replaced with links to VDR's of affected products in a CVE Known Affected Software list using names familiar to the end users, such as this example:

- [Cisco ASA 5500-X Series Firewalls Software release 9.16.4](https://sec.cloudapps.cisco.com/security/center/softwarechecker.x?productSelected=ASA&selectedMethod=A&captchaPage=true&platformCode=277437&versionNamesSelected=9.16.4&allAdvisoriesSelectedByTree=N&advisoryType=0&iosBundleId=cisco-sa-20250924-bundle&isFewCheckBoxChecked1=false&isNoneCheckBoxsChecked1=true#~onStep3)

The creation of a well known URL for VDR's may also be worth considering using REST API syntax, i.e. https://supplier.com/VDR/productID/Version would return the current VDR for productID/version. The VDR download location (URL) could be provided in a product SBOM [as shown in this SPDX V 2.3 example](https://spdx.github.io/spdx-spec/v2.3/how-to-use/#k19-linking-to-an-sbom-vulnerability-report-for-a-software-product-per-nist-executive-order-14028) or a product Trust Registry cybersecurity label (see FDA materials for cybersecurity label information), as show in this [product Trust Registry lookup](https://softwareassuranceguardian.com/labellink/getTrustedProductLabel?ProductID=BDFD6504A6D994F1ACDBF28E863D20C7B5CB69A72113403B5DE0784A537B27C6&html=1) based on I[ETF SCITT concepts](https://www.energycentral.com/intelligent-utility/post/an-international-trust-registry-demonstration-is-a-success-ENajTxqSuVCnTrg) that were [demonstrated in an IETF SCITT Hackathon using FDA Requirements](https://wiki.ietf.org/meeting/117/hackathon#ProjectsIncludedinHackathon).

### Ownership
Business Cyber Guardian is prepared to transfer ownership of the open source VDR schema to the Linux Foundation, if this VDR standards development proposal is approved and a VDR standard initiative is launched, based on the VDR schema provided.

### Summary
In summary, a NIST Vulnerability Disclosure Report (VDR) is an attestation by a software vendor showing that the vendor has checked each component of a software product SBOM for vulnerabilities and reports on the details of any vulnerabilities reported by a NIST NVD search. The VDR is a living document which the software vendor updates as needed when new vulnerabilities have been discovered and reported to communicate the vulnerability status of their product, in accordance with[ the international standard for communicating vulnerability disclosures, IEC 29147:2018](https://www.iso.org/obp/ui/#iso:std:iso-iec:29147:ed-2:v1:en). A VDR is published whenever a software vendor issues a new or updated SBOM, including initial product release, making the  most current version of the  VDR available online, all the time, to all customers of the product described in the VDR. This gives software consumers that ability to answer the question [“What is the vulnerability status of my software product from Vendor V, as of NOW?”.](https://energycentral.com/c/pip/sbom-vulnerability-attestations-%E2%80%93-carfax-sbom%E2%80%99s) for all of the products in their digital ecosystem, using one common VDR format. 

CVE records would become more useful to consumers by replacing known affected product cpe identifiers with URLs to Manufacturer VDR materials using familiar product names and version for affected products, eliminating one or more cpe searches typically needed to identify the product that users are running in their production ecosystems. This would enable end users to operationalize and automate the processing of CVE reports to rapidly close the window of opportunity that hackers exploit when a new vulnerability is reported, as described in this article; https://www.energycentral.com/intelligent-utility/post/closing-the-cyber-risk-window-of-opportunity-that-criminals-exploit-DufDnCMWayEym24 

**NOTE: Business Cyber Guardian has committed to withdraw its VDR format, if there is broad consensus to adopt the OWASP CycloneDX VDR format.**

### VEX and VDR Differences and VEX Challenges

VEX is frequently brought up during discussions of VDR as an alternative. VEX is not an alternative to VDR, as show in the [side-by-side comparison of VEX and VDR provided by OWASP](https://owasp.org/blog/2023/02/07/vdr-vex-comparison).  A VEX record MUST contain at least one vulnerability ID, however many products have no reported vulnerabilities making it infeasible to use VEX as an alternative for VDR as there is no CVE to report on. Art Manion provides a clear explanation for why a VEX cannot be used as a VDR when there are not vulnerabilities to report for a product: https://github.com/ossf/wg-vulnerability-disclosures/issues/172#issuecomment-3391482701


[Ground truth on the extreme difficulties of implementing VEX is provided by Cassie Crossley in this video clip](https://www.youtube.com/watch?v=j9MB7oaq8aI&t=3634s).



