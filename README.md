# AI Web Hunter

### Building a website with AI / then hunting its vulnerabilities.

**Champlain College · Cybersecurity Capstone**
**Team:** CJ Batista ([@cjbatista](https://github.com/cjbatista)) · Connor Clune ([@connorclune](https://github.com/connorclune))

## The Idea

Use an **AI tool to build a real website**, **deploy it on our Alienware lab machine**, and then **attack it**, running vulnerability scans and a hands-on penetration test against something we built ourselves.

The question we're chasing: *when you let AI build a web app, what does it leave behind?* AI-generated code ships fast, but it also ships defaults, shortcuts, and assumptions. We want to find out what those look like from an attacker's seat.

Our professor recommended **DVWA** (Damn Vulnerable Web Application); evaluating exactly how it fits practice target, benchmark, or a model for what to look for, is one of our first research tasks.

The full loop: **build → deploy → break → document → harden.**

## The Setup

- **Deploy host:** an old Alienware desktop running **Proxmox VE 9.2** (`cj.server`). The website runs on its own VM.
- **Website:** generated with an AI builder (tool TBD see Phase 1). We favor tools that output real, self-hostable code, so the site is genuinely deployable and testable rather than locked in a hosted builder.
- **Attack box:** Kali Linux, working an OWASP-based methodology — Nmap, Nikto, ZAP/Burp, sqlmap, plus a vulnerability scanner.

## Plan

| Phase | Focus |
|-------|-------|
| **1. Research & Planning** | Scope, professor approval, choose the AI tool, research DVWA, define features & pentest methodology |
| **2. Build the Website** | Scaffold with the AI tool, build core features + real input/auth surfaces, commit the code |
| **3. Deploy on Alienware** | Provision a Proxmox VM, install the stack, deploy the site, (optional) stand up DVWA, snapshot before testing |
| **4. Pentest & Vuln Assessment** | Automated scans, manual OWASP Top 10, DVWA practice, findings + CVSS scoring, remediate & re-test |
| **5. Documentation & Presentation** | Attack walkthrough, architecture & network diagrams, demo video, final presentation, repo cleanup |

Work is tracked in **[Issues](../../issues)**, grouped by the milestones above and split between CJ and Connor.
