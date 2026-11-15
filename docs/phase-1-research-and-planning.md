# Phase 1: Research and Planning

**Champlain College, Cybersecurity Capstone**
**Team:** CJ Batista, Connor Clune

> **Updated 15 Nov. 2026 to match our Methodology paper.** Where this plan and the paper differed, the paper wins: the AI tool (section 2.4), the attack device (sections 1.4 and 5.2), destructive testing (sections 1.2 and 1.3), and the project phases (section 1.7). The paper calls this planning work the groundwork before its five phases.

Phase 1 establishes the project's scope, limitations, AI development tool options, application feature requirements, and penetration-testing methodology. The goal is to create a controlled web application using an AI-assisted development tool, deploy it within the team's Proxmox lab environment, and evaluate the security vulnerabilities introduced during the AI-assisted development process.

## 1. Project Scope

### 1.1 Project Objective

The objective of this project is to investigate the security implications of using an AI development tool to create a web application.

The team will use a selected AI development tool to assist in designing and developing a functional web application. The resulting application will be exported, deployed to a controlled virtual machine within the team's Proxmox lab environment, and subjected to penetration testing.

The project will document:

- What security controls the AI development tool implements by default.
- What vulnerabilities or insecure configurations are introduced by the generated code.
- Which vulnerabilities can be identified through automated security tools.
- Which vulnerabilities require manual testing or analysis.
- How the identified vulnerabilities can be remediated.
- Whether remediation successfully eliminates or reduces the identified vulnerabilities.

The project is focused on evaluating the security of the AI-generated application, rather than evaluating the AI model itself as a product.

### 1.2 In Scope

The following activities are within the scope of the project:

- Selecting an AI-assisted development tool capable of producing exportable application code.
- Using the selected tool to develop a web application.
- Implementing a defined set of application features that provide realistic security testing surfaces.
- Reviewing the generated source code for security weaknesses.
- Deploying the application within the team's isolated Proxmox lab environment.
- Performing reconnaissance against the team's application.
- Testing the application against relevant categories of the OWASP Top 10:2025.
- Using automated security tools to identify potential vulnerabilities.
- Performing manual validation of automated findings.
- Assigning CVSS v4.0 scores to confirmed vulnerabilities.
- Documenting vulnerabilities introduced by the AI-generated implementation.
- Remediating selected vulnerabilities.
- Re-testing the application after remediation.
- Destructive testing, such as crashing services or making permanent changes to server configurations, rolled back from snapshots afterward.
- Comparing automated findings with manually identified vulnerabilities.
- Documenting limitations and lessons learned from the AI-assisted development process.

### 1.3 Out of Scope

The following activities are outside the scope of this project:

- Attacking systems belonging to Champlain College, other students, faculty, or third parties.
- Testing the AI development company's production infrastructure.
- Attempting to compromise the AI provider, its APIs, or its underlying systems.
- Testing the security of Proxmox itself beyond what is necessary to securely host the project.
- Denial-of-service testing through traffic flooding. A light check for denial-of-service protection, such as refreshing the site a handful of times to see whether a module like Apache's Mod Evasive responds, is part of reconnaissance (section 5.4).
- Performing attacks against public-facing infrastructure outside the team's controlled lab.
- Obtaining or testing against real users' sensitive personal information.
- Deploying intentionally vulnerable software to an uncontrolled or publicly accessible environment.
- Evaluating the AI model's intelligence, reasoning ability, or overall quality except where it directly relates to application security.
- Treating the AI-generated application as evidence that all applications created by the selected AI tool contain the same vulnerabilities.

### 1.4 Testing Boundaries

All penetration testing will be performed against infrastructure owned or controlled by the project team and explicitly designated for testing.

The primary target will be the team's deployed web application and its supporting components that are necessary for the application to function.

Testing will be performed within the team's authorized lab network. The application will not be exposed to the public internet at any stage of the project.

The application will be deployed to a dedicated virtual machine on the team's Proxmox host. The project uses two devices: the R740, and a secondary device that manages it and is also the device the attacks come from. Which device that is has not been recorded yet ([#81](https://github.com/cjbatista/Capstone-project/issues/81)).

A virtual machine snapshot will be taken prior to the start of testing and prior to each remediation cycle, so that the environment can be restored to a known state and testing can be repeated consistently.

If any third-party service is required for the application to function, that service is excluded from testing. Only components hosted on the team's infrastructure are valid targets.

An authorization statement confirming team ownership of the target environment will be committed to the project repository prior to the start of Phase 4.

### 1.5 Project Constraints

The project must be completed within one academic year across the five defined phases. Phases 1 through 3 are preparatory, and schedule pressure must not be allowed to reduce the time available for Phase 4 testing.

All virtual machines are hosted on a single Dell PowerEdge R740 running Proxmox VE 9.2.2 (see [lab-setup.md](lab-setup.md)). The Alienware desktop from the first plan is scrapped. Available memory and storage on that host limit the total number of virtual machines that can run concurrently.

The project will use free-tier and open-source tooling. Any tool that requires a paid subscription to export application code or to complete a full security scan will be identified during tool evaluation and excluded if a suitable free alternative exists.

Neither team member is primarily a web application developer. The selected AI development tool must be capable of producing a deployable application without requiring extended framework troubleshooting.

### 1.6 Assumptions

- The selected AI development tool will produce exportable application code that can be hosted on the team's own virtual machine without reliance on vendor hosting.
- The generated application will contain identifiable security weaknesses. If the generated application proves unexpectedly secure, that outcome will be documented as a finding in its own right, and the benchmark application described in Section 3 will take on greater importance in demonstrating testing methodology.
- The Proxmox host will remain available and operational for the duration of the project.

### 1.7 Project Phases

From our Methodology paper. This planning work comes before them.

| Phase | What happens |
|---|---|
| 1. Environment Setup | The R740 and the isolated network: the physical and network foundation |
| 2. Site Generation and Deployment | Hypervisor and target VM, generate the site with Claude Code, deploy it as generated, take a clean baseline snapshot |
| 3. Site Reconnaissance | Map the deployed site before any attack: Nmap, walking its features, a light denial-of-service protection check |
| 4. Attack and Vulnerability Analysis | Run the attacks, measure the results, score each weakness with CVSS |
| 5. Presentation of Findings | Compile the findings and conclusions into the paper and the final presentation |

## 2. AI Development Tool Options

### 2.1 Candidate Tools

**Bolt.new**

- Advantages: Builds and runs a full-stack application in the browser, allowing the team to validate functionality immediately. Exports code to any host rather than locking the project to a single platform, which supports deployment to the Proxmox environment. The free tier includes one million tokens per month, which is sufficient for substantial prototyping. Generates applications with a functional backend, providing meaningful testing surfaces.
- Disadvantages: A documented failure pattern is the exposure of secrets within the client-side bundle. Token limits may become restrictive during extended development sessions.

**Lovable**

- Advantages: Produces full-stack applications with Supabase integration and GitHub synchronization, keeping the generated code portable. Output tends to be visually polished, which makes the resulting application a more realistic testing target.
- Disadvantages: The Supabase dependency presents a significant problem for this project. If the application database is hosted in Supabase's cloud environment, a portion of the application's attack surface resides outside the team's infrastructure and is therefore out of scope. A commonly reported weakness in Lovable applications is the omission of Supabase row-level security, which the team would be unable to test under the defined scope.

**v0 (Vercel)**

- Advantages: Converts prompts into production-ready React components using modern frontend patterns. Produces clean Next.js output that is readable when documenting the root cause of a finding.
- Disadvantages: Deployment is oriented toward Vercel, so self-hosting requires manual export and deployment configuration. The tool has historically been more focused on frontend components than on full-stack applications, which risks producing a limited backend and therefore a limited assessment. Reported weaknesses include improper use of NEXT_PUBLIC_ environment variables and unguarded route handlers.

**Replit Agent**

- Advantages: Provides an integrated development environment with an AI agent, database, and hosting. Offers the lowest friction path to a working application.
- Disadvantages: The integrated hosting model conflicts with the project requirement that the application run on the team's Proxmox host. Extracting and self-hosting the application would require deliberate additional effort.

**Cursor or Claude Code (AI-assisted coding tools)**

- Advantages: Provide maximum control over the technology stack and project structure, ensuring the application can be deployed to the team's virtual machine. Free and low-cost tiers are available. Output follows standard project conventions that are straightforward to deploy.
- Disadvantages: These tools represent AI-assisted development rather than AI-generated application development, which weakens the research premise. If the team makes the majority of architectural and security decisions, resulting vulnerabilities are attributable to the team rather than to the tool. Development time is also longer.

**Open-source self-hosted builders (bolt.diy, Dyad, Open Lovable)**

- Advantages: Genuinely open source, capable of running locally with a model of the team's choosing, and free of platform lock-in. bolt.diy is a browser-based open implementation of Bolt, and Dyad runs locally on the desktop. These options align with the project's preference for free, self-hosted tooling and keep all components within the team's environment.
- Disadvantages: These tools require more setup effort and are less refined than the hosted alternatives. They also require the team to supply model access. There is a meaningful risk of consuming Phase 2 development time on builder configuration rather than application development.

### 2.2 Selection Criteria

Candidate tools will be evaluated against the following criteria:

1. **Exportable and self-hostable code.** This is a mandatory requirement. Hosted website builders such as Wix and Squarespace do not permit full code export and lock projects to their own platform, which excludes that entire category of tool from consideration.
2. **Functional backend rather than frontend only.** The application requires authentication, form handling, and a database hosted on the team's virtual machine. Code-first builders frequently rely on external services such as Supabase or Clerk, so each candidate must be evaluated on whether its backend components can be hosted locally.
3. **Deployable technology stack.** The generated application must run on a Proxmox virtual machine using a common stack such as Node.js, Python, or PHP with a locally hosted database.
4. **Sufficient free tier.** No paid subscription should be required to export application code or complete development.
5. **Genuine AI-driven development.** The tool should be responsible for architectural and security decisions rather than the team, as those decisions are the subject of this study.

### 2.3 Evaluation Method

Both team members will trial the two highest-scoring candidates using an identical prompt describing a comparable application, such as a site with user authentication and a page where authenticated users can post comments. The generated output will be compared on backend completeness, deployability, and the security controls each tool implements by default.

### 2.4 Tool Selection

**Decision: Claude Code**, Anthropic's command-line coding tool, as stated in our Introduction and Methodology papers ([#53](https://github.com/cjbatista/Capstone-project/issues/53)).

- The site is generated from a single prompt that describes a small business site in plain, non-technical language and makes no reference to security, encryption, or input validation. This reflects how a non-expert owner would describe what they want.
- The exact model, programming language, and framework are fixed and recorded before the build begins.
- Every prompt, the model version, and the number of generations needed to reach a working site are recorded.

The two-tool trial described in section 2.3 was not recorded.

## 3. Benchmark Application: Open Questions

The professor recommended DVWA (Damn Vulnerable Web Application). DVWA is one of several available options, and the team will make a documented decision rather than adopting it by default. The following questions must be resolved.

### 3.1 Questions Regarding Role

What function would a benchmark application serve in this project? Three distinct purposes are possible, and each leads to a different selection:

- **Calibration**, meaning the benchmark is used to verify that the team's scanning tools and methodology correctly identify known vulnerabilities before being applied to the primary target.
- **Comparison**, meaning the benchmark serves as a baseline against which the vulnerability profile of the AI-generated application is measured.
- **Skill development**, meaning the benchmark provides a practice environment for exploitation techniques prior to testing the team's own application.

Is a benchmark application necessary at all? If the AI-generated application produces sufficient findings, a second application may represent schedule cost without corresponding value. The team should define the threshold for that decision.

Will the benchmark application appear in the final report, or is it internal preparation only?

### 3.2 Questions Regarding Selection

- **DVWA.** Written in PHP, with graduated difficulty levels and source code displayed for each challenge, and straightforward Docker deployment. However, DVWA reflects an older PHP development style, while the selected AI tool will most likely generate a modern JavaScript or Python stack. Does a PHP baseline provide a valid comparison to the application under test?
- **OWASP Juice Shop.** Written in TypeScript and Node.js, covering the OWASP Top Ten along with additional real-world vulnerability classes, MIT licensed, actively maintained, and deployable via Docker. It is widely regarded as the most modern of the deliberately vulnerable applications and is a much closer match to the expected AI-generated stack. Does the improved stack alignment justify the increased difficulty?
- **OWASP WebGoat.** Written in Java and structured as guided lessons. Effective for learning, but a poor stack match for this project.
- **bWAPP and Mutillidae II.** Both written in PHP with broad vulnerability coverage. These present the same stack-alignment concern as DVWA.
- **OWASP Broken Web Applications VM.** Bundles multiple vulnerable applications into a single virtual machine. Convenient, but consumes more host resources.

### 3.3 Questions Regarding Deployment

- Should the benchmark application be deployed as a Docker container or as a separate virtual machine? A container is faster to deploy and lighter on host resources, while a separate virtual machine provides clearer network segmentation and a more accurate architecture diagram.
- Does the benchmark application's vulnerability set meaningfully overlap with the weaknesses expected from AI-generated code, such as missing authorization checks, exposed secrets, injection flaws, and insecure default configurations? Limited overlap would weaken any comparison drawn in the final report.
- Should the benchmark application influence the feature set of the team's application? A meaningful comparison may require that both applications expose similar categories of attack surface.

### 3.4 Preliminary Position

OWASP Juice Shop appears to offer the stronger technology-stack alignment, while DVWA offers an easier initial learning curve. One possible approach is to use DVWA for early skill development and Juice Shop as the comparison baseline in the final report. This approach requires deploying and maintaining two applications, and the team should determine whether that cost is justified.

**Decision (29 Sept. 2026):** DVWA will be used as a practice target (skill development) before we test our own site. Using Juice Shop as a comparison baseline is still open.

## 4. Application Feature Requirements

### 4.1 Draft Feature Set

Each proposed feature exists to establish a specific category of attack surface.

| Feature | Attack surface established |
|---|---|
| User registration and login | Authentication, credential handling, password storage |
| Session management | Session handling, cookie attributes, session fixation and hijacking |
| Form accepting and storing user input | Injection, cross-site scripting, input validation |
| Page displaying stored user data | Broken access control, insecure direct object references, data exposure |
| Administrative or privileged view | Privilege escalation, authorization enforcement |
| File upload (optional) | File handling, unrestricted upload, path traversal |

### 4.2 Open Question on Feature Specification

Two approaches are available. The team may specify the required features to the AI development tool explicitly, or may provide a general application prompt, such as a request for a community message board, and document which features the tool chooses to include on its own.

The second approach produces a stronger research result, because the tool's independent design decisions are the subject of the study. The first approach more reliably guarantees sufficient attack surface for testing. A combined approach is possible, in which a general prompt is issued first and only missing features are requested afterward, with the difference documented.

**Decision:** the general-prompt approach. One plain-language prompt describes a small business site, and we document what the tool builds on its own (section 2.4).

### 4.3 Feature Set Finalization

Per our Methodology paper, the site is expected to have the pages typical of a small business site: a landing page, registration, login, a customer account area, and a payment page. The final count is recorded once the site is generated.


Original note: to be completed following tool selection, as available features may depend on the capabilities of the selected tool.

## 5. Penetration Testing Methodology

### 5.1 Framework

Testing will follow the OWASP Top 10:2025, using the OWASP Web Security Testing Guide as the procedural reference for individual test cases.

### 5.2 Testing Platform

The secondary device that manages the R740 is also the attack platform (our Methodology paper). Which device that is has not been recorded yet ([#81](https://github.com/cjbatista/Capstone-project/issues/81)). All required tooling will be installed and verified on it before attacks begin.

### 5.3 Tooling

| Category | Tool | Purpose |
|---|---|---|
| Reconnaissance | Nmap | Host discovery, port and service enumeration |
| Web server scanning | Nikto | Server-level misconfiguration and exposure checks |
| Application scanning | OWASP ZAP | Automated web application vulnerability scanning, selected as the primary scanner because it is free and open source |
| Injection testing | sqlmap | Automated detection and exploitation of SQL injection |
| Manual testing proxy | OWASP ZAP proxy or Burp Suite Community | Request interception and manipulation for authentication, authorization, and session testing |
| Infrastructure scanning | OpenVAS / Greenbone | Vulnerability scanning of the host virtual machine rather than the application layer |

### 5.4 Testing Sequence

1. Reconnaissance and service enumeration against the target virtual machine: Nmap for ports, services, versions, the host OS, and HTTP or HTTPS; walking the site's account features; and a light denial-of-service protection check ([#82](https://github.com/cjbatista/Capstone-project/issues/82)).
2. Automated scanning using the tools identified above, with all output retained.
3. Manual testing across the applicable OWASP Top 10 categories, conducted independently of the automated results.
4. Comparison of manual findings against automated findings. Vulnerabilities identified manually but missed by automated tooling will be documented explicitly, as that gap is a reportable result of this project.
5. Validation of each candidate finding to eliminate false positives. Only confirmed vulnerabilities will be carried into the findings report.

### 5.5 Documentation of Findings

Each confirmed vulnerability will be documented with a description, the affected component, reproduction steps, supporting evidence in the form of screenshots and captured requests and responses, a CVSS v4.0 score with its vector string, and an analysis of how the vulnerability relates to the AI tool's generated output.

### 5.6 Remediation and Re-testing

Vulnerabilities will be prioritized by CVSS score. High-severity findings will be remediated, and the application will be re-scanned and re-tested to confirm that the remediation is effective. Lower-severity and informational findings will be documented with a recommendation but will not necessarily be remediated within the project timeline.

A virtual machine snapshot will be taken before testing begins and before each remediation cycle, allowing the team to restore the environment to a known state and repeat tests consistently.

## 6. Phase 1 Exit Criteria

Phase 1 is complete when the following conditions are met:

- [x] Initial project meeting held with the professor and project direction approved
- [ ] Scope, limitations, and testing boundaries reviewed and agreed by both team members
- [x] AI development tool selected, with rationale documented in Section 2.4 (Claude Code)
- [ ] Benchmark application decision made and documented, including a decision not to use one if that is the outcome
- [ ] Application feature set finalized in Section 4.3
- [ ] Testing methodology confirmed and all required tooling installed and verified on the attack device
- [ ] Authorization statement committed to the project repository
