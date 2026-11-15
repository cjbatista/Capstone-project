# AI Web Hunter

### Building a website with AI / then hunting its vulnerabilities.

**Champlain College · Cybersecurity Capstone**
**Team:** CJ Batista ([@cjbatista](https://github.com/cjbatista)) · Connor Clune ([@connorclune](https://github.com/connorclune))

## The Idea

Use an **AI tool to build a real website**, **deploy it on our own lab server**, and then **attack it**, running vulnerability scans and a hands-on penetration test against something we built ourselves.

The question we're chasing: *when you let AI build a web app, what does it leave behind?* AI-generated code ships fast, but it also ships defaults, shortcuts, and assumptions. We want to find out what those look like from an attacker's seat.

Our professor recommended **DVWA** (Damn Vulnerable Web Application). On 29 Sept. 2026 we decided to use it as a practice target before we test our own site. Using OWASP Juice Shop as a comparison baseline is still open.

The full loop: **build → deploy → break → document → harden.**

## The Setup

- **Deploy host:** a **Dell PowerEdge R740** running **Proxmox VE 9.2.2** (node `aiwebhuntsrv`). It is offline and we reach it over one Ethernet cable from a MacBook. The website will run on its own VM. Details: [Lab setup](docs/lab-setup.md). (The Alienware desktop from our first plan is scrapped. The R740 is our only lab host.)
- **Website:** generated with an AI builder (tool TBD, see [Phase 1](docs/phase-1-research-and-planning.md) and [AI tool options](docs/ai-tool-options.md)). We favor tools that output real, self-hostable code, so the site is genuinely deployable and testable rather than locked in a hosted builder.
- **Attack box:** Kali Linux, working an OWASP-based methodology — Nmap, Nikto, ZAP/Burp, sqlmap, plus a vulnerability scanner.

## Plan

| Phase | Focus |
|-------|-------|
| **1. Research & Planning** | Scope, professor approval, choose the AI tool, research DVWA, define features & pentest methodology |
| **2. Build the Website** | Scaffold with the AI tool, build core features + real input/auth surfaces, commit the code |
| **3. Deploy on the R740** | Provision a Proxmox VM, install the stack, deploy the site, (optional) stand up DVWA, snapshot before testing |
| **4. Pentest & Vuln Assessment** | Automated scans, manual OWASP Top 10, DVWA practice, findings + CVSS scoring, remediate & re-test |
| **5. Documentation & Presentation** | Attack walkthrough, architecture & network diagrams, demo video, final presentation, repo cleanup |

Work is tracked in **[Issues](../../issues)**, grouped by the milestones above and split between CJ and Connor.

## Progress

**Where we are (15 Nov. 2026):** the lab server is up. Proxmox VE runs on the R740 and we can log in to it from a MacBook over a direct cable, with no internet on the server. Phase 1 planning is mostly written but not closed. No website has been built yet.

### Completed work

**Lab server (Phase 3 groundwork)**

- [x] Obtained a Dell PowerEdge R740 server.
- [x] Connected it to power and brought it online.
- [x] Completed the initial physical server configuration.
- [x] Installed Proxmox VE 9.2.2 (node `aiwebhuntsrv`).
- [x] Configured the network interface: Proxmox's bridge `vmbr0` uses NIC 4, address `192.168.0.121`.
- [x] Found that the server's physical network ports were disabled, which blocked every connection attempt.
- [x] Enabled the ports, which fixed the connection.
- [x] Cabled NIC 4 directly to the MacBook. No switch, no router.
- [x] Logged in to the Proxmox web UI from the MacBook with no internet on the server (14 Nov. 2026).

How we did it: [Lab setup](docs/lab-setup.md) and [Network troubleshooting](docs/network-troubleshooting.md).

**Planning and research (Phase 1)**

- [x] Professor approved the new project direction (#52).
- [x] Scope doc and full Phase 1 plan written (#51).
- [x] 12 AI build tools compared and a two-tool shortlist made (#53).
- [x] Research sources gathered in MLA 9, 11 of them peer reviewed or accepted.
- [x] Revised proposal draft with one research question.
- [x] Decided: one academic year, DVWA as a practice target, OWASP Top 10:2025, CVSS v4.0.

### Next steps

**Lab server**

- [ ] Record what is still missing from [Lab setup](docs/lab-setup.md#not-recorded-yet): hardware specs (CPU, memory, disks, RAID mode), Proxmox install choices, and where the ports were enabled.
- [ ] Decide on iDRAC: fix the login and give it a fixed address, or leave it unplugged.
- [ ] Add an internal-only Proxmox bridge for the website VM and the Kali VM, so test traffic stays off the management network.
- [ ] Plan how to copy ISOs and packages onto the offline server.
- [x] Renamed the Phase 3 milestone to "Deploy on the R740" and updated issues #51, #53, #61, #63 and #73 (15 Nov. 2026).

**Close Phase 1**

- [ ] Run the two-tool trial and record the AI tool choice in Phase 1 section 2.4 (#53).
- [ ] Decide on Juice Shop as a comparison baseline (#54).
- [ ] Finalize the website's feature set (#55).
- [ ] Confirm the test method and set up the Kali VM with its tools (#56).
- [ ] Commit the authorization statement for our own lab (Phase 1 section 1.4).
- [ ] Mark the Phase 1 exit criteria done and close #51.

**Phases 2 to 5**

- [ ] Phase 2: build the site with the chosen tool and commit its code (#57 to #60).
- [ ] Phase 3: create the website VM, install the stack, deploy, optional DVWA VM, snapshot before testing (#61 to #65).
- [ ] Phase 4: automated scans, manual OWASP Top 10 testing, findings with CVSS v4.0 scores, fix and re-test (#66 to #70).
- [ ] Phase 5: walkthrough, diagrams, demo video, final presentation, repo cleanup (#71 to #75).

## Docs

| Doc | What it is |
|-----|------------|
| [Lab setup](docs/lab-setup.md) | The R740 server: hardware, Proxmox install, network, how we connect, what is not recorded yet |
| [Network troubleshooting](docs/network-troubleshooting.md) | How we found and fixed the disabled network ports, and what we learned |
| [Scope](docs/scope.md) | Project description, success criteria, who does what, timeline by phase |
| [Phase 1: Research and Planning](docs/phase-1-research-and-planning.md) | Scope, boundaries, tool options, benchmark questions, feature set, test method, exit criteria |
| [AI tool options](docs/ai-tool-options.md) | Free AI builders compared on our selection criteria, with ups and downs (issue #53) |
| [Research sources](docs/research-sources.md) | Verified sources in MLA 9, marked peer reviewed or not |
| [Proposal (revised draft)](docs/proposal-draft.md) | Our proposal with suggested edits and open questions |
