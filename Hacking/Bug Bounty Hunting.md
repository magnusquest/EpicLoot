Bug reports should include information on how exploitation of each vulnerability can be reproduced step-by-step.

### Bounty Boards
- [HackerOne](https://hackerone.com/opportunities/all/search?ordering=Newest+programs)
- [BugCrowd](https://www.bugcrowd.com/bug-bounty-list/)



The essential elements of a good bug report are (the element order can vary):


| `Vulnerability Title`       | Including vulnerability type, affected domain/parameter/endpoint, impact etc.                                                                                        |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `CWE & CVSS score`          | For communicating the characteristics and severity of the vulnerability.                                                                                             |
| `Vulnerability Description` | Better understanding of the vulnerability cause.                                                                                                                     |
| `Proof of Concept (POC)`    | Steps to reproduce exploiting the identified vulnerability clearly and concisely.                                                                                    |
| `Impact`                    | Elaborate more on what an attacker can achieve by fully exploiting the vulnerability. Business impact and maximum damage should be included in the impact statement. |
| `Remediation`               | Optional in bug bounty programs, but good to have.                                                                                                                   |

### CWE & CVSS
[Common Weaknesses Enumeration (CWE)](https://cwe.mitre.org/) is a community-developed list of software and hardware weakness types.

When it comes to communicating the severity of an identified vulnerability, then [Common Vulnerability Scoring System (CVSS)](https://www.first.org/cvss/) should be used, as it is a published standard used by organizations worldwide.

Use the [CVSS v3.1 Calculator](https://www.first.org/cvss/calculator/3.1) identify the severity of an identified vulnerability.

## Good Report Examples

Find below some good report examples selected by HackerOne:

- [SSRF in Exchange leads to ROOT access in all instances](https://hackerone.com/reports/341876)
- [Remote Code Execution in Slack desktop apps + bonus](https://hackerone.com/reports/783877)
- [Full name of other accounts exposed through NR API Explorer (another workaround of #476958)](https://hackerone.com/reports/520518)
- [A staff member with no permissions can edit Store Customer Email](https://hackerone.com/reports/980511)
- [XSS while logging in using Google](https://hackerone.com/reports/691611)
- [Cross-site Scripting (XSS) on HackerOne careers page](https://hackerone.com/reports/474656)

Please refer to the [Submitting Reports](https://docs.hackerone.com/hackers/submitting-reports.html) section of HackerOne's docs portal for the actual process a bug bounty hunter has to follow to submit a bug report.

If the security/triage team does not get back to you in a reasonable amount of time, then if the submission was through a bug bounty platform, you can contact [Mediation](https://docs.hackerone.com/hackers/hacker-mediation.html).