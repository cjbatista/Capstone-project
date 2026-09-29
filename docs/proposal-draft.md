# AI Web Hunter: Proposal (Revised Draft)

**Status:** draft for CJ and Connor to review. Not submitted.

This is our proposal draft with edits. The original wording is kept wherever it worked. Each section ends with a short "What changed" note so we can see the edits and push back on any of them. Sources are in [research-sources.md](research-sources.md).

---

## Motivation

CJ and I have noticed the increase in popularity of services that offer website creation via AI model. For most of the sites we have seen firsthand, they have been remarkably similar in wording, content, and structure. Their services are often found online through sponsored media or paid advertising on browser result pages.

This matches what researchers are seeing. Pew Research Center found that more than a third of web pages published since ChatGPT launched show signs of AI authorship (Bestvater et al.). Sites built with AI builders have also already leaked real people's data. In 2025, researchers found 170 sites built with Lovable, a popular AI builder, that exposed names, emails, and payment details because the generated database access rules were missing or weak (Palmer; "CVE-2025-48757 Detail"). In 2026, a site whose founder said AI wrote all of its code exposed 1.5 million API tokens and 35,000 email addresses the same way (Nagli).

> **What changed:** kept the first paragraph as is. Added a second paragraph that backs our observation with Pew and two real incidents.

---

## Problem Statement

With the increasing prevalence of AI in our web browsing compounding with its involvement elsewhere in our daily life, more websites are being built by people with no security background, using tools that write the code for them. Research already shows that AI-written code is often insecure. In one early study, about 40% of programs written by GitHub Copilot were vulnerable (Pearce et al.). In another, people using an AI assistant wrote less secure code while feeling more confident that it was secure (Perry et al.). OWASP, the main authority on web application security, now lists "inappropriate trust in AI generated code," or vibe coding, as an emerging risk in its 2025 Top 10 ("X03:2025"). Most of this research tests small pieces of code, though. Much less is known about the security of complete applications built with AI, especially when they are built by novices (Heidaripour et al.).

We want to find out whether the people interacting with these sites can reasonably expect their privacy and security not to be compromised.

**Research question:** What security weaknesses does a website built by an AI website builder contain by default, and can an attacker use them to reach the data the site is meant to protect?

> **What changed:** the original said what we want ("ensure these sites are secure") but not what the problem is. Now it names the gap (little research on complete AI-built sites), cites OWASP's own 2025 entry on vibe coding, and ends with one research question we can answer by the end of the project.

---

## Objectives of Work

The fundamental objective at this point in time involves hosting a local web server that has been created by one of the generative AI website builders, and populating it with dummy information that acts as a stand-in for real client/server data. Following the completion of this task, the next step is to attack the site in an attempt to gather any of the dummy information from above.

We will test the site against the OWASP Top 10 using both automated scanners and manual testing. We will focus on the flaws researchers most often find in AI-generated applications: broken access control, injection, weak authentication and session handling, and insecure configuration (Deng et al.; Heidaripour et al.). This follows the approach of an earlier study that deployed AI-generated websites in a lab and attacked them (Tóth et al.). We will also capture and analyze the site's network traffic to check whether data or passwords are sent without encryption.

Once testing is done, we will fix the most severe issues and re-test the site to confirm the fixes work. All of the attacks, extracted data, methods, and fixes will be documented.

> **What changed:**
> - "Pentest the site for possible applications of malware" became testing against the OWASP Top 10. A web pentest doesn't usually look for malware, so the new wording says what we will actually test.
> - "Offensive network forensics" became "capture and analyze the site's network traffic". That's what we meant, and it isn't a standard term.
> - Added the fix and re-test step. Our README and issue #70 already include it.
> - Added Tóth et al. to show the method has a precedent.

---

## Research Limitations and Scope

Our early research relied mostly on non-peer-reviewed, "unofficial" work. Since then we have found peer-reviewed studies on the security of AI-generated code and web applications (Tóth et al.; Heidaripour et al.; Vero et al.). Some of the most relevant work is still very new, including 2026 preprints (Deng et al.), and much of what is known about specific AI builders comes from security researchers' disclosures rather than academic papers. We will note which kind of source supports each claim.

Due to the relatively constricted time-frame of one academic year, we plan to generate and host just one web server that will be probed and attacked. We do not want to perform multiple analyses of separate web servers at this time as we are unsure how long the actual analysis may take, however we are open to broadening our sample size of website generators if we find there is spare time.

Because we are testing one site built by one tool, our results will show what that tool produced for our prompt. They cannot prove that every site built by AI, or by that tool, has the same weaknesses.

All testing will stay on our own Proxmox lab, on a network that is not reachable from the internet, using dummy data only. We will not test the AI builder's own platform or any system we do not own. If the site depends on a hosted service we cannot run on our own server, that service is out of scope.

> **What changed:**
> - The first paragraph is updated. "Most of our sources are non-peer reviewed" is no longer true: we now have 11 peer-reviewed or accepted sources.
> - The second paragraph is kept as is.
> - Added a limit on what one site can prove, and a short ethics and scope paragraph that matches Phase 1 sections 1.3 and 1.4.

---

## Works Cited

Bestvater, Samuel, et al. "How Much of the Internet Is Written With AI?" *Pew Research Center*, 20 Aug. 2026, www.pewresearch.org/data-labs/2026/08/20/how-much-of-the-internet-is-written-with-ai/. Accessed 28 Sept. 2026.

"CVE-2025-48757 Detail." *National Vulnerability Database*, National Institute of Standards and Technology, 30 May 2025, nvd.nist.gov/vuln/detail/CVE-2025-48757. Accessed 28 Sept. 2026.

Deng, Junquan, et al. "Understanding the (In)Security of Vibe-Coded Applications." *arXiv*, version 4, 14 Sept. 2026, https://doi.org/10.48550/arXiv.2606.23130. Preprint. Accessed 28 Sept. 2026.

Heidaripour, Mahdieh, et al. "How Secure Are Full-Stack Web Applications Generated by Large Language Models? A Multi-Language Security Study." *Availability, Reliability and Security. ARES 2026 International Workshops*, Springer, 2026, pp. 58-75, https://doi.org/10.1007/978-3-032-35576-8_4. Lecture Notes in Computer Science. Accessed 28 Sept. 2026.

Nagli, Gal. "Hacking Moltbook: The AI Social Network Any Human Can Control." *Wiz Blog*, Wiz, 2 Feb. 2026, www.wiz.io/blog/exposed-moltbook-database-reveals-millions-of-api-keys. Accessed 28 Sept. 2026.

Palmer, Matt. "Statement on CVE-2025-48757." *Matt Palmer*, 29 May 2025, mattpalmer.io/posts/statement-on-CVE-2025-48757/. Accessed 28 Sept. 2026.

Pearce, Hammond, et al. "Asleep at the Keyboard? Assessing the Security of GitHub Copilot's Code Contributions." *2022 IEEE Symposium on Security and Privacy (SP)*, IEEE, 2022, pp. 754-68, https://doi.org/10.1109/SP46214.2022.9833571. Accessed 28 Sept. 2026.

Perry, Neil, et al. "Do Users Write More Insecure Code with AI Assistants?" *Proceedings of the 2023 ACM SIGSAC Conference on Computer and Communications Security*, ACM, 2023, pp. 2785-99, https://doi.org/10.1145/3576915.3623157. Accessed 28 Sept. 2026.

Tóth, Rebeka, et al. "LLMs in Web Development: Evaluating LLM-Generated PHP Code Unveiling Vulnerabilities and Limitations." *Computer Safety, Reliability, and Security. SAFECOMP 2024 Workshops*, edited by Andrea Ceccarelli et al., Springer, 2024, pp. 425-37, https://doi.org/10.1007/978-3-031-68738-9_34. Lecture Notes in Computer Science 14989. Accessed 28 Sept. 2026.

Vero, Mark, et al. "BaxBench: Can LLMs Generate Correct and Secure Backends?" *Proceedings of the 42nd International Conference on Machine Learning*, edited by Aarti Singh et al., PMLR, 2025, pp. 61344-90. Proceedings of Machine Learning Research 267, proceedings.mlr.press/v267/vero25a.html. Accessed 28 Sept. 2026.

"X03:2025 Inappropriate Trust in AI Generated Code ('Vibe Coding')." *OWASP Top 10:2025*, OWASP Foundation, 2025, top10.owasp.org/2025/X01_2025-Next_Steps/. Accessed 28 Sept. 2026.

> **What changed:**
> - One style (MLA 9), listing only sources that are cited in the text.
> - The Pew news article is replaced with Pew's own report.
> - The OWASP GenAI project is replaced with OWASP's own Top 10:2025 entry on vibe coding (X03:2025), which is about AI-written code. The GenAI project is about apps that use AI.
> - NIST SP 800-218A is dropped, since the text doesn't cite it anymore. Both older sources are still in [research-sources.md](research-sources.md) if we want them back.

---

## Open questions for us to settle

These conflict between our docs. Pick one answer for each and make every doc match.

1. **Timeline:** resolved 29 Sept. 2026. It's one academic year, and Phase 1 section 1.5 now says so.
2. **DVWA:** resolved 29 Sept. 2026. DVWA is a practice target, and both [scope.md](scope.md) and Phase 1 section 3.4 now say so. Juice Shop as a comparison baseline is still open.
3. **Standard versions:** resolved 29 Sept. 2026. We use OWASP Top 10:2025 and CVSS v4.0, and Phase 1 now says so.
4. **AI tool:** most likely Claude Code (29 Sept. 2026), to be confirmed in Phase 1 section 2.4. See [ai-tool-options.md](ai-tool-options.md) and issue #53.
