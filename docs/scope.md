# Scope Document (AI Web Hunter)

**Champlain College, Cybersecurity Capstone**
**Team:** CJ Batista ([@cjbatista](https://github.com/cjbatista)), Connor Clune ([@connorclune](https://github.com/connorclune))

## Project Description

We will build a website using an AI code-generation tool, deploy it on our own lab infrastructure, and conduct a penetration test against it. The goal is to evaluate the security posture of AI-generated code from an attacker's perspective and document the vulnerabilities it introduces.

## Success Criteria

This project meets its objectives when the following deliverables are complete:

1. A functional website, generated with an AI tool, deployed as a self-hosted VM on our Proxmox lab host.
2. A completed vulnerability assessment and penetration test, including automated scanning (Nmap, Nikto, ZAP/Burp, sqlmap, and a vulnerability scanner) and manual testing against the OWASP Top 10, with DVWA used as a practice target before we test our own site.
3. A findings report documenting each vulnerability identified, with CVSS scoring and analysis of how the vulnerability relates to the AI tool's output.
4. Remediation of the highest-severity findings, with re-testing to confirm the fixes are effective.
5. A final presentation package, including an attack walkthrough, architecture and network diagrams, a demo video, and a completed repository.

## Team and Responsibilities

| Team Member | Primary Responsibilities |
|---|---|
| CJ Batista | Selection and evaluation of the AI development tool, website build-out and feature implementation, code review |
| Connor Clune | Proxmox VM provisioning and deployment, attack environment setup, execution of scans and manual testing |
| Both | Project planning, DVWA evaluation, findings documentation, CVSS scoring, remediation, and final presentation |

Task-level work is tracked in GitHub Issues, organized by the project phases below and assigned to CJ and Connor as appropriate.

## Timeline by Phase

The phases follow our Methodology paper. Planning comes first.

| Phase | Focus | Deliverable |
|---|---|---|
| Planning: Research and Scope | Scope definition, professor approval, selection of the AI development tool, DVWA evaluation, definition of feature set and testing methodology | Approved project scope |
| 1. Environment Setup | The R740 server and the isolated network, and the secondary device that manages the server and runs the attacks | Lab ready for the build |
| 2. Site Generation and Deployment | Hypervisor and target VM, generate the site with Claude Code from one plain-language prompt, deploy it as generated, optionally deploy DVWA, baseline snapshot | Website running on lab infrastructure |
| 3. Site Reconnaissance | Nmap scan, walk the site's features, light denial-of-service protection check, documented attack map | Attack map |
| 4. Attack and Vulnerability Analysis | Attacks including destructive ones (rolled back from snapshots), DVWA practice, findings with CVSS scores, remediation and re-testing | Completed findings report |
| 5. Presentation of Findings | Findings and conclusions in the paper, attack walkthrough, diagrams, demo video, final presentation, repository cleanup | Final presentation and repository |

Specific dates will be added to this table once approved by the professor and reflected as milestones in GitHub Issues.
