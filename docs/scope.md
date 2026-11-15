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

| Phase | Focus | Deliverable |
|---|---|---|
| 1. Research and Planning | Scope definition, professor approval, selection of the AI development tool, DVWA evaluation, definition of feature set and testing methodology | Approved project scope |
| 2. Website Development | Build the site using the selected tool, implement core features including input handling and authentication, commit code to the repository | Deployable website |
| 3. Deployment | Provision a Proxmox VM, install required software, deploy the website, optionally deploy DVWA, snapshot the environment prior to testing | Website running on lab infrastructure |
| 4. Assessment | Automated scanning, manual OWASP Top 10 testing, DVWA testing, documentation of findings with CVSS scores, remediation and re-testing | Completed findings report |
| 5. Documentation and Presentation | Attack walkthrough, architecture and network diagrams, demo video, final presentation, repository cleanup | Final presentation and repository |

Specific dates will be added to this table once approved by the professor and reflected as milestones in GitHub Issues.
