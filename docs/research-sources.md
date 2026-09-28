# AI Web Hunter: Research Sources

CJ Batista and Connor Clune. Compiled 28 Sept. 2026. All citations are MLA 9.

Every source below was opened on its real page (publisher, DOI, arXiv, NVD, or the author's own site) to confirm the title, authors, date, and the numbers quoted. Anything that could not be confirmed is listed in the "Do not cite" section at the end.

Labels:
- **Peer reviewed**: journal or conference proceedings
- **Accepted**: accepted to a peer-reviewed conference, final proceedings not out yet
- **Preprint**: not peer reviewed yet
- **Incident**: a real disclosed vulnerability or breach
- **Report**: industry or think-tank research
- **Standard**: methodology or scoring reference
- **Champlain library**: full text through our student login (IEEE Xplore, ACM Digital Library)

---

## How we found these sources

- **Search:** web searches for research on the security of AI-generated code and AI-built web apps, run with an AI research assistant (Claude). We started from a list of well-known papers in this area and added newer ones from 2025 and 2026.
- **Check:** every source was opened on its own page (publisher, DOI, arXiv, NVD, the researcher's site, or vendor docs). Titles, authors, dates, and page numbers were checked against Crossref (the DOI registry) and arXiv. Anything we could not confirm is in section 7.
- **Library:** on 28 Sept. 2026 we searched the databases the Champlain library gives us (IEEE Xplore, ACM Digital Library, ScienceDirect) and added 3 sources we can read in full with our student login.
- **OWASP:** on 28 Sept. 2026 we went back through the OWASP site and checked the sources OWASP itself cites. That turned up OWASP's own entry on vibe coding (section 5).
- **Our own finds:** we found Information is Beautiful (section 4) ourselves through the OWASP website.
- **Paywalls:** for paywalled papers, the details here come from the abstract or a free arXiv copy, not the paid version. Read the full text before quoting a number.

### Getting the full text

| Access | Sources |
|---|---|
| Free | Everything in sections 3, 4, and 5, including the ACM TechBrief and Information is Beautiful. The arXiv papers (Deng, Zhao, Andročec, Dora). BaxBench. |
| Champlain library, IEEE Xplore | Aydın and Bahtiyar, Hamer et al., Pearce et al., Khoury et al. |
| Champlain library, ACM Digital Library | Perry et al., Fu et al. |
| Free arXiv copy of a paywalled paper | Tóth et al. ([2404.14459](https://arxiv.org/abs/2404.14459)), Hamer et al. ([2403.15600](https://arxiv.org/abs/2403.15600)), Pearce et al. ([2108.09293](https://arxiv.org/abs/2108.09293)), Perry et al. ([2211.03622](https://arxiv.org/abs/2211.03622)), Fu et al. ([2310.02059](https://arxiv.org/abs/2310.02059)), Khoury et al. ([2304.09655](https://arxiv.org/abs/2304.09655)) |
| Not in Champlain's databases | Heidaripour et al. (Springer, no free copy). Use the library's [interlibrary loan form](https://docs.google.com/forms/d/e/1FAIpQLScg7AfJrWHMlcHQ2dQNsXuB92LnNo_VL_5b4_4yzEY-YwQmDQ/viewform). |

Library links go through `https://cobalt.champlain.edu/login?url=` followed by the article link. If we read the arXiv copy instead of the published one, we cite the arXiv copy.

---

## 1. Fixes to our current three references

**Pew study.** Cite Pew directly, not the news story about it.

Bestvater, Samuel, et al. "How Much of the Internet Is Written With AI?" *Pew Research Center*, 20 Aug. 2026, www.pewresearch.org/data-labs/2026/08/20/how-much-of-the-internet-is-written-with-ai/. Accessed 28 Sept. 2026.

- Pew checked about 490,000 English web pages with an AI text detector. More than a third of pages published since ChatGPT launched show signs of AI authorship.
- Note: this is about AI-written *text*, not AI-built *sites*. Use it in Motivation only, as "AI is already all over the web."

**OWASP Gen AI Security Project.** Swap it for OWASP's own vibe coding entry, X03:2025 (section 5). That project is about apps that *contain* an LLM (chatbots, prompt injection), not code an AI wrote. Only keep it if our site ends up with an AI feature, and then cite the specific list:

Wilson, Steve, et al. *OWASP Top 10 for LLM Applications 2026*. OWASP Foundation, Aug. 2026, genai.owasp.org/resource/owasp-genai-llm-top-10-2026/. Accessed 28 Sept. 2026.

**NIST SP 800-218A.** Keep it, but in MLA. It covers secure development of AI models, not testing code an AI produced, so use it as background, not as our testing standard.

Booth, Harold, et al. *Secure Software Development Practices for Generative AI and Dual-Use Foundation Models: An SSDF Community Profile*. NIST Special Publication 800-218A, National Institute of Standards and Technology, July 2024, https://doi.org/10.6028/NIST.SP.800-218A. Accessed 28 Sept. 2026.

---

## 2. Academic research (supports the Problem Statement)

These replace the "most of our sources are non-peer reviewed" problem. 11 of the 13 are peer reviewed or accepted.

### Closest matches to our project

**Tóth et al. (2024)**, Peer reviewed

Tóth, Rebeka, et al. "LLMs in Web Development: Evaluating LLM-Generated PHP Code Unveiling Vulnerabilities and Limitations." *Computer Safety, Reliability, and Security. SAFECOMP 2024 Workshops*, edited by Andrea Ceccarelli et al., Springer, 2024, pp. 425-37, https://doi.org/10.1007/978-3-031-68738-9_34. Lecture Notes in Computer Science 14989. Accessed 28 Sept. 2026.

- Deployed 2,500 GPT-4 generated PHP websites in Docker and attacked them with Burp Suite, static analysis, and manual review.
- 11.56% of sites could be fully compromised. 26% had at least one vulnerability exploitable through the web page. File upload code was insecure 78% of the time.
- **Use:** our methodology precedent. They did what we are doing, at scale.

**Heidaripour et al. (2026)**, Peer reviewed

Heidaripour, Mahdieh, et al. "How Secure Are Full-Stack Web Applications Generated by Large Language Models? A Multi-Language Security Study." *Availability, Reliability and Security. ARES 2026 International Workshops*, Springer, 2026, pp. 58-75, https://doi.org/10.1007/978-3-032-35576-8_4. Lecture Notes in Computer Science. Accessed 28 Sept. 2026.

- Ten full-stack apps built with GPT-4o and Claude Sonnet across five stacks (PHP, Node/Express, Spring Boot, Flask, ASP.NET), the way a novice would build them. 275 findings.
- Most common: security misconfiguration, weak login and session handling, missing security headers, no CSRF protection, insecure cookies, server info leakage.
- Their abstract says most research tests small code snippets and much less is known about complete apps built by novices. **That is our research gap.**
- **Use:** Problem Statement gap, and a checklist of what to expect.

**Deng et al. (2026)**, Preprint

Deng, Junquan, et al. "Understanding the (In)Security of Vibe-Coded Applications." *arXiv*, version 4, 14 Sept. 2026, https://doi.org/10.48550/arXiv.2606.23130. Preprint. Accessed 28 Sept. 2026.

- Collected 9,041 apps built with Claude Code and Lovable and audited 200 live ones. Found 1,186 vulnerabilities. 91.0% of audited apps had at least one, and 65.77% were Critical or High.
- Most common: broken access control, injection, authentication failures.
- Cite version 4. Earlier versions have different numbers.
- **Use:** the only academic source on a named AI app builder (Lovable).

### Supporting studies

**Aydın and Bahtiyar (2025)**, Peer reviewed, Champlain library

Aydın, Deniz, and Şerif Bahtiyar. "Security Vulnerabilities in AI-Generated JavaScript: A Comparative Study of Large Language Models." *2025 IEEE International Conference on Cyber Security and Resilience (CSR)*, IEEE, 2025, pp. 200-05, https://doi.org/10.1109/CSR64739.2025.11130176. Accessed 28 Sept. 2026.

- 275 of 600 JavaScript snippets from six models (including GPT-4o and Claude 3.5 Sonnet) had vulnerabilities. That's 602 vulnerabilities across 28 CWE types, and every model introduced some.
- Numbers are from the abstract. Read the full paper before quoting them.
- **Access:** no free copy. [Open through Champlain](https://cobalt.champlain.edu/login?url=https://ieeexplore.ieee.org/document/11130176).
- **Use:** our site will most likely be JavaScript, so this is the closest match to what we'll be testing.

**Hamer et al. (2024)**, Peer reviewed, Champlain library

Hamer, Sivana, et al. "Just Another Copy and Paste? Comparing the Security Vulnerabilities of ChatGPT Generated Code and StackOverflow Answers." *2024 IEEE Security and Privacy Workshops (SPW)*, IEEE, 2024, pp. 87-94, https://doi.org/10.1109/SPW63631.2024.00014. Accessed 28 Sept. 2026.

- ChatGPT's code had 248 vulnerabilities against 302 in human StackOverflow answers to the same 108 questions, about 20% fewer. Their conclusion is that no copied code, from AI or people, should be trusted blindly.
- **Access:** [open through Champlain](https://cobalt.champlain.edu/login?url=https://ieeexplore.ieee.org/document/10579524), or the free copy on [arXiv](https://arxiv.org/abs/2403.15600).
- **Use:** keeps us fair in Limitations. We are not claiming AI is worse than humans, only that AI-built sites still need testing.

**Vero et al. (2025), BaxBench**, Peer reviewed

Vero, Mark, et al. "BaxBench: Can LLMs Generate Correct and Secure Backends?" *Proceedings of the 42nd International Conference on Machine Learning*, edited by Aarti Singh et al., PMLR, 2025, pp. 61344-90. Proceedings of Machine Learning Research 267, proceedings.mlr.press/v267/vero25a.html. Accessed 28 Sept. 2026.

- 392 backend tasks. The best model (OpenAI o1) got 62% correct. On average, the authors could exploit around half of the correct programs.
- **Use:** "it works" does not mean "it is safe."

**Zhao et al. (2026), SusVibes**, Accepted (ICML 2026)

Zhao, Songwen, et al. "Is Vibe Coding Safe? Benchmarking Vulnerability of Agent-Generated Code in Real-World Tasks." *arXiv*, version 4, 21 Sept. 2026, https://doi.org/10.48550/arXiv.2512.03262. Accepted to the Forty-Third International Conference on Machine Learning (ICML 2026). Accessed 28 Sept. 2026.

- 186 real feature requests. SWE-Agent with Claude 4 Sonnet was 57% functionally correct but only 11.8% secure. Adding security hints to the prompt did not fix it.
- **Use:** same point as BaxBench, for AI agents (the kind of tool that builds whole sites).

**Andročec (2026)**, Accepted (CECIIS 2026)

Andročec, Darko. "Vibe Coding and Web Application Security: A Twin-Prompt Study." *arXiv*, 21 Aug. 2026, https://doi.org/10.48550/arXiv.2608.20963. Accepted to the 37th Central European Conference on Information and Intelligent Systems (CECIIS 2026). Accessed 28 Sept. 2026.

- Built six web apps twice: once with a normal prompt, once asking for security. Normal versions had 51 confirmed issues, security-prompted versions had 24 and no Critical or High.
- **Use:** an optional experiment if we have spare time (see section 6).

**Pearce et al. (2022)**, Peer reviewed

Pearce, Hammond, et al. "Asleep at the Keyboard? Assessing the Security of GitHub Copilot's Code Contributions." *2022 IEEE Symposium on Security and Privacy (SP)*, IEEE, 2022, pp. 754-68, https://doi.org/10.1109/SP46214.2022.9833571. Accessed 28 Sept. 2026.

- About 40% of 1,689 Copilot programs across 89 scenarios were vulnerable.
- **Use:** the standard background citation that started this research area.

**Perry et al. (2023)**, Peer reviewed

Perry, Neil, et al. "Do Users Write More Insecure Code with AI Assistants?" *Proceedings of the 2023 ACM SIGSAC Conference on Computer and Communications Security*, ACM, 2023, pp. 2785-99, https://doi.org/10.1145/3576915.3623157. Accessed 28 Sept. 2026.

- People using an AI assistant wrote less secure code *and* were more confident it was secure.
- **Use:** supports our point that non-experts trust these tools and don't notice the problems.

**Fu et al. (2025)**, Peer reviewed

Fu, Yujia, et al. "Security Weaknesses of Copilot-Generated Code in GitHub Projects: An Empirical Study." *ACM Transactions on Software Engineering and Methodology*, vol. 34, no. 8, 2025, pp. 1-34, https://doi.org/10.1145/3716848. Accessed 28 Sept. 2026.

- 733 AI-generated snippets from real GitHub projects. 29.5% of Python and 24.2% of JavaScript snippets had security weaknesses, across 43 CWE types including XSS.
- **Use:** shows the flaws make it into real shipped code.

**Khoury et al. (2023)**, Peer reviewed

Khoury, Raphaël, et al. "How Secure Is Code Generated by ChatGPT?" *2023 IEEE International Conference on Systems, Man, and Cybernetics (SMC)*, IEEE, 2023, pp. 2445-51, https://doi.org/10.1109/SMC53992.2023.10394237. Accessed 28 Sept. 2026.

- Only 5 of 21 ChatGPT programs were secure on the first try.
- **Use:** AI knows about security but doesn't apply it unless asked.

**Dora et al. (2025)**, Preprint (backup)

Dora, Swaroop, et al. "The Hidden Risks of LLM-Generated Web Application Code: A Security-Centric Evaluation of Code Generation Capabilities in Large Language Models." *arXiv*, 29 Apr. 2025, https://doi.org/10.48550/arXiv.2504.20612. Preprint. Accessed 28 Sept. 2026.

- Web code from five major models had gaps in login, sessions, input validation, and security headers.

---

## 3. Real incidents with AI site builders (supports Motivation)

**Lovable data exposure, CVE-2025-48757**, Incident

"CVE-2025-48757 Detail." *National Vulnerability Database*, National Institute of Standards and Technology, 30 May 2025, nvd.nist.gov/vuln/detail/CVE-2025-48757. Accessed 28 Sept. 2026.

Palmer, Matt. "Statement on CVE-2025-48757." *Matt Palmer*, 29 May 2025, mattpalmer.io/posts/statement-on-CVE-2025-48757/. Accessed 28 Sept. 2026.

- Researchers scanned 1,645 Lovable sites and found 170 (10.3%) leaking data like names, emails, payment details, and API keys, because database access rules were missing or weak.
- NVD scores it 9.3 Critical. It is marked "disputed" because Lovable says securing the data is the customer's job.
- Palmer works at Replit, a Lovable competitor. Worth one line if we cite him.
- **Use:** our best real example. It also shows the "who is responsible" gap our Problem Statement is about.

**Base44 login bypass**, Incident

Nagli, Gal. "Wiz Research Uncovers Critical Vulnerability in AI Vibe Coding Platform Base44 Allowing Unauthorized Access to Private Applications." *Wiz Blog*, Wiz, 29 July 2025, www.wiz.io/blog/critical-vulnerability-base44. Accessed 28 Sept. 2026.

- Anyone with an app's ID (visible in its URL) could register a verified account on private apps. Fixed within a day.
- **Use:** a specific test for us: can IDs found in the site's code get us into restricted areas?

**Moltbook database exposure (2026)**, Incident

Nagli, Gal. "Hacking Moltbook: The AI Social Network Any Human Can Control." *Wiz Blog*, Wiz, 2 Feb. 2026, www.wiz.io/blog/exposed-moltbook-database-reveals-millions-of-api-keys. Accessed 28 Sept. 2026.

- A database key in the site's JavaScript plus missing access rules exposed 1.5 million API tokens, 35,000 emails, and 4,060 private messages. The founder said AI wrote all the code.
- **Use:** shows the same mistake still happening in 2026.

**Lovable platform leak (2026)**, Incident

"Our Response to the April 2026 Incident." *Lovable*, 22 Apr. 2026, lovable.dev/blog/our-response-to-the-april-2026-incident. Accessed 28 Sept. 2026.

- From 3 Feb. to 20 Apr. 2026, any logged-in Lovable user could view the chat history and source code of other users' public projects. Bug bounty reports were closed without action for two months.
- **Use:** the builder platform itself can leak what users type into it. Supports the privacy side of our Problem Statement.

**Escape.tech scan of 5,600 apps**, Report

Hinniger-Foray, Nohé, et al. "Methodology: How We Discovered over 2k High-Impact Vulnerabilities in Apps Built with Vibe Coding Platforms." *Escape*, Escape Technologies, 29 Oct. 2025, escape.tech/blog/methodology-how-we-discovered-vulnerabilities-apps-built-with-vibe-coding/. Accessed 28 Sept. 2026.

- Over 5,600 public apps (mostly Lovable, plus Base44, Create.xyz, Bolt.new, and others). Over 2,000 vulnerabilities, 400+ exposed secrets, 175 cases of exposed personal data including medical records.
- **Use:** shows the problem across several builders, not just one.

**v0 used to build phishing sites**, Report

Bordjiba, Houssem Eddine, and Paula De la Hoz. "Okta Observes v0 AI Tool Used to Build Phishing Sites." *Okta*, 1 July 2025, www.okta.com/blog/threat-intelligence/okta-observes-v0-ai-tool-used-to-build-phishing-sites/. Accessed 28 Sept. 2026.

- Attackers used Vercel's v0 to clone real login pages (Microsoft 365, crypto companies).
- **Use:** supports "these sites reach regular users." Optional.

---

## 4. Industry and policy reports

**ACM TechBrief on vibe coding (2026)**, Report (policy brief), free

Garfinkel, Simson, et al. *ACM TechBrief: AI-Assisted Software Development, or Vibe Coding: Benefits and Risks of AI-Driven Software Development*. Association for Computing Machinery, 28 Apr. 2026, https://doi.org/10.1145/3807518. Accessed 28 Sept. 2026.

- A 5-page brief from the ACM. It says vibe coding lets people with little coding experience build working apps, but the platforms don't enforce normal software engineering practices. The AI can repeat security flaws from the code it learned from, and the platforms rarely test their output.
- **Access:** free on the [ACM Digital Library](https://dl.acm.org/doi/full/10.1145/3807518).
- **Use:** a major computing organization making the same point as our Problem Statement.

**Information is Beautiful: breach tracker**, Data visualization, free (found through OWASP)

McCandless, David, et al. "World's Biggest Data Breaches & Hacks." *Information is Beautiful*, informationisbeautiful.net/visualizations/worlds-biggest-data-breaches-hacks/. Accessed 28 Sept. 2026.

- A regularly updated chart of the largest data breaches and hacks, with a link to the raw data. The page credits its data to the Identity Theft Resource Center, DataBreaches.net, and news reports.
- It does not flag which breaches involved AI-built sites. It shows how big breaches get in general.
- It's a compiled chart, not peer-reviewed research. To cite a specific breach from it, cite that breach's original report too.
- **Use:** Motivation and Limitations. It backs up our draft's point that much of the evidence is about "massive data breaches" rather than GenAI itself.

**Veracode 2025**, Report

Wessling, Jens. "We Asked 100+ AI Models to Write Code. Here's How Many Failed Security Tests." *Veracode*, 30 July 2025, www.veracode.com/blog/genai-code-security-report/. Accessed 28 Sept. 2026.

- 45% of code samples from 100+ models failed security tests with OWASP Top 10 flaws. XSS defense failed 86% of the time. Bigger models were not more secure.

**Veracode 2026**, Report

Tischler, Natalie. "2026 GenAI Code Security Report: AI Is Writing More of Your Code but Security Hasn't Caught Up." *Veracode*, 28 July 2026, www.veracode.com/blog/2026-genai-code-security-report-ai-risk/. Accessed 28 Sept. 2026.

- Average security pass rate 56%, basically unchanged from the year before. XSS pass rate only 15%.
- **Use with 2025:** a year later, no real improvement.

**Georgetown CSET (2024)**, Report

Ji, Jessica, et al. *Cybersecurity Risks of AI-Generated Code*. Center for Security and Emerging Technology, Georgetown University, Nov. 2024, https://doi.org/10.51593/2023CA010. Accessed 28 Sept. 2026.

- Almost half the code from five models had bugs that could often be exploited. Argues responsibility should sit with AI companies, not only users.
- **Use:** a neutral, policy-level source for the Problem Statement.

**Wiz on common vibe-coding risks**, Report

Nagli, Gal, and Alon Schindel. "Wiz Research Discovers One in Five Organizations Exposed to Systemic Risks in Vibe-Coded Applications: Here's How to Secure Them." *Wiz Blog*, Wiz, 18 Sept. 2025, www.wiz.io/blog/common-security-risks-in-vibe-coded-apps. Accessed 28 Sept. 2026.

- Four repeat problems: login checks only in the browser, secrets in browser code, weak or missing database access rules, internal apps published with no login.
- The "1 in 5" means 1 in 5 organizations *use* these platforms, not that 1 in 5 apps are flawed. Don't misquote it.
- **Use:** a ready test checklist.

**Vercel on v0 secrets**, Report (vendor)

Sbano, Ty, et al. "v0: Vibe Coding, Securely." *Vercel*, 4 Aug. 2025, vercel.com/blog/v0-vibe-coding-securely. Accessed 28 Sept. 2026.

- Vercel blocked over 17,000 deployments in one month for exposed secrets.
- **Use:** the vendor itself admits users ship secrets in client code.

---

## 5. Standards and methodology (for issues #54 and #56)

**OWASP Top 10:2025, X03: vibe coding**, Standard (emerging risk)

"X03:2025 Inappropriate Trust in AI Generated Code ('Vibe Coding')." *OWASP Top 10:2025*, OWASP Foundation, 2025, top10.owasp.org/2025/X01_2025-Next_Steps/. Accessed 28 Sept. 2026.

- In the "Next Steps" chapter of the Top 10:2025, OWASP lists "Inappropriate Trust in AI Generated Code ('Vibe Coding')" as an emerging risk. It defines vibe coding as code written and committed almost entirely without human oversight.
- It tells developers to fully understand and review all AI code, with their own eyes and with tools like static analysis. It also says vibe coding is not recommended for complex, business-critical, or long-lived programs.
- **Checking its sources:**
  - Its only reference is the Secure Code Review Cheat Sheet (below). It maps no CWEs, since OWASP says there are no CVEs or CWEs for AI-generated code yet.
  - It says AI code "often contains more vulnerabilities" than human code, but gives no source for that. The studies are mixed. Perry et al. found people with an AI assistant wrote less secure code, but Hamer et al. found ChatGPT's code had fewer vulnerabilities than human StackOverflow answers. Cite this as OWASP's position and back it with the studies, not as a proven fact.
- **Use:** our best OWASP citation. OWASP naming vibe coding as a risk supports our Problem Statement.

**OWASP Secure Code Review Cheat Sheet**, Standard

"Secure Code Review Cheat Sheet." *OWASP Cheat Sheet Series*, OWASP Foundation, cheatsheetseries.owasp.org/cheatsheets/Secure_Code_Review_Cheat_Sheet.html. Accessed 28 Sept. 2026.

- The method X03 points to for reviewing AI code. It doesn't mention AI itself.
- **Use:** how we do the "review the generated source code" step in Phase 1 section 1.2.
- **More from OWASP's own references:** the Top 10 category pages list the guides to test each category with. For example:
  - A01 Broken Access Control: ASVS V8 Authorization, WSTG Authorization Testing, and the Authorization Cheat Sheet.
  - A07 Authentication Failures: the Authentication Cheat Sheet.

**OWASP Top 10:2025**, Standard

*OWASP Top 10:2025*. OWASP Foundation, 2025, top10.owasp.org/2025/. Accessed 28 Sept. 2026.

- A01 Broken Access Control, A02 Security Misconfiguration, A03 Software Supply Chain Failures, A04 Cryptographic Failures, A05 Injection, A06 Insecure Design, A07 Authentication Failures, A08 Software or Data Integrity Failures, A09 Security Logging and Alerting Failures, A10 Mishandling of Exceptional Conditions.
- **Use:** the categories we group every finding under.

**OWASP Web Security Testing Guide**, Standard

*OWASP Web Security Testing Guide*. Version 4.2, OWASP Foundation, 3 Dec. 2020, wstg.owasp.org/v4.2/. Accessed 28 Sept. 2026.

- **Use:** our step-by-step test plan. Each test gets a WSTG ID so the re-test is repeatable.

**NIST SP 800-115**, Standard

Scarfone, Karen, et al. *Technical Guide to Information Security Testing and Assessment*. NIST Special Publication 800-115, National Institute of Standards and Technology, Sept. 2008, https://doi.org/10.6028/NIST.SP.800-115. Accessed 28 Sept. 2026.

- **Use:** the overall phases (plan, discover, attack, report) and rules of engagement.

**CVSS v4.0**, Standard

*Common Vulnerability Scoring System Version 4.0: Specification Document*. Document version 1.2, Forum of Incident Response and Security Teams, 18 June 2024, www.first.org/cvss/v4.0/specification-document. Accessed 28 Sept. 2026.

- **Use:** score every finding with the FIRST calculator, before and after the fix.

**CWE Top 25 (2025)**, Standard

"2025 CWE Top 25 Most Dangerous Software Weaknesses." *Common Weakness Enumeration*, MITRE Corporation, Dec. 2025, cwe.mitre.org/top25/archive/2025/2025_cwe_top25.html. Accessed 28 Sept. 2026.

- Top three: XSS (CWE-79), SQL injection (CWE-89), CSRF (CWE-352).
- **Use:** tag each finding with a CWE ID and compare our list to the Top 25.

**DVWA**, Standard (practice target)

Wood, Robin. *Damn Vulnerable Web Application (DVWA)*. Version 2.5, GitHub, 29 Jan. 2025, github.com/digininja/DVWA. Accessed 28 Sept. 2026.

- A deliberately broken PHP and MariaDB site with modules for SQL injection, XSS, CSRF, file upload, command injection, and more. Four levels: Low, Medium, High, Impossible (the secure version).
- Runs with `docker compose up -d`. Its README says never put it on the internet, run it in a VM on NAT.
- **Use:** our control target. Confirm our tools catch known bugs on DVWA first, then run the same tools on our site. Impossible level is the "what secure looks like" comparison.

**OWASP ASVS 5.0**, Standard

*OWASP Application Security Verification Standard 5.0.0*. OWASP Foundation, 30 May 2025, github.com/OWASP/ASVS/tree/v5.0.0. Accessed 28 Sept. 2026.

- **Use:** pass or fail checks for the re-test after we fix things.

**NIST SP 800-218 (SSDF)**, Standard

Souppaya, Murugiah, et al. *Secure Software Development Framework (SSDF) Version 1.1: Recommendations for Mitigating the Risk of Software Vulnerabilities*. NIST Special Publication 800-218, National Institute of Standards and Technology, Feb. 2022, https://doi.org/10.6028/NIST.SP.800-218. Accessed 28 Sept. 2026.

- **Use:** backs the fix and re-test phase. Better fit than 800-218A for that part.

**PTES**, Standard (optional)

"Main Page." *The Penetration Testing Execution Standard*, 16 Aug. 2014, www.pentest-standard.org/index.php/Main_Page. Accessed 28 Sept. 2026.

- Seven pentest phases. Old and community-run, so use it next to NIST 800-115, not instead of it.

---

## 6. How these fix the proposal

- **Problem Statement:** cite OWASP's X03:2025 vibe coding entry, then add the gap from Heidaripour et al. (complete AI-built apps, especially by novices, are under-studied). Back it with Tóth et al. and Deng et al.
- **Limitations:** the line "most of the relevant resources we've found have been non-peer reviewed" is no longer true. We now have 11 peer-reviewed or accepted sources. Update or cut that paragraph.
- **Motivation:** Pew for "AI is all over the web," then the Lovable CVE and Moltbook for "and it leaks real data."
- **Methodology (new section, if the template has one):** NIST 800-115 phases, OWASP WSTG tests, OWASP Top 10 and CWE for labels, CVSS v4.0 for scores, DVWA as the control, ASVS for re-test.
- **Test checklist:** the Wiz four risks, plus Heidaripour's categories (headers, CSRF, cookies, sessions), plus Deng's (access control, injection, auth).
- **Optional, only if time:** Andročec's twin-prompt idea. Build the site twice, once with a normal prompt and once asking for security, then compare. That changes our "one site" scope, so it's a team decision.
- **For #53 (picking the builder):** Lovable has the most published research (the CVE, Escape, Deng, the April 2026 leak), which makes our results easy to compare. But its backend normally runs on hosted Supabase, so self-hosting it on the Alienware needs a plan. See [ai-tool-options.md](ai-tool-options.md). Decide in #53.

---

## 7. Do not cite

These came up in research but could not be confirmed from a primary source:

- "80% of AI-generated apps contain an exploitable flaw" credited to Stanford. No academic source found.
- "40 to 45% vulnerability rate across Lovable, Bolt, and v0." Only in vendor blogs.
- Okta's v0 phishing site built "in 30 seconds." It's in news stories, not in Okta's post.
- RedAccess "Shadow Builders" report (380,000 exposed assets). Behind a form, and secondary sources disagree.
- A Feb. 2026 Lovable case affecting 18,000+ people. Only found on aggregator blogs.
- Replit "4,000 fake users." From news coverage, not the first-hand account.
- Escape's landing page numbers (1.4K apps). They conflict with its own methodology post. Use the methodology post.

Details that are fine to cite but have a known gap:
- Heidaripour et al.: the Springer book editors and LNCS volume number were not listed. The citation works without them.
- Zhao et al. and Andročec: accepted, but final proceedings pages not out yet. Cite the arXiv version as written above.
- OWASP LLM Top 10 2026: the release page is dated 3 Aug. 2026, but OWASP's main LLM page still shows 2025. Only matters if our site has an AI feature.
