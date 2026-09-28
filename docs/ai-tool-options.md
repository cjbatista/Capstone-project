# Free AI Tools for Building the Site

Goes with Phase 1 section 2 and issue #53. Free plans change often. Everything here was checked on each tool's own pricing page or docs on **28 Sept. 2026**. Links are at the bottom.

## Quick scorecard

Scored against our selection criteria in [Phase 1, section 2.2](phase-1-research-and-planning.md#22-selection-criteria).

| Tool | 1. Export code | 2. Backend on our VM | 3. Common stack | 4. Free plan is enough | 5. AI makes the decisions |
|---|---|---|---|---|---|
| **Lovable** | Yes (GitHub sync) | Partial (Supabase, which we can self-host) | Yes | Partial (30 credits a month) | Yes |
| **Dyad** | Yes (local files) | Partial (Supabase or Neon, optional) | Yes | Yes (needs a model) | Yes |
| **Bolt.new** | Yes (GitHub sync) | No (Bolt's hosted database by default) | Yes | Yes | Yes |
| **v0** | Yes (GitHub sync) | Partial (database through Vercel add-ons) | Yes | Partial (7 messages a day) | Yes |
| **Replit Agent** | Yes (zip or GitHub) | Partial (built around Replit's database) | Yes | Partial | Yes |
| **Google AI Studio (Build)** | Yes (zip or GitHub) | Partial (Firestore database is Google-hosted) | Yes | Yes | Yes |
| **bolt.diy** | Yes (zip) | Partial | Yes | Yes (needs a model) | Yes |
| **Gemini CLI** | Yes (local files) | Yes | Yes | Yes | Partial |
| **Google Antigravity** | Yes (local files) | Yes | Yes | Yes (weekly limits) | Partial |
| **GitHub Copilot** | Yes (local files) | Yes | Yes | Partial | Partial |
| **Cursor** | Yes (local files) | Yes | Yes | Partial (limits not published) | Partial |

**Not an option:**
- **Claude Code** is not on Claude's free plan. The cheapest plan with it is Pro, $20 a month.
- **Firebase Studio** stopped taking new sign-ups on 22 June 2026 and shuts down 22 March 2027.
- **Base44:** GitHub sync needs the paid Builder plan.
- **Anything** (formerly Create.xyz): building an app needs a paid plan.
- **Wix and Squarespace** can't export code.

## App builders (you describe the app, it builds the whole thing)

### Lovable
- **Free plan:** 5 build credits a day, up to 30 a month, plus 20 Cloud credits a month.
- **Getting the code out:** GitHub sync works on every plan, free included. The direct "Download codebase" button is paid only, so we would use GitHub.
- **Ups:**
  - Most published research to compare our results against: the CVE-2025-48757 data leak, Escape's scan of 4,000+ Lovable apps, Deng et al. (2026), and the April 2026 platform leak.
  - New apps (since 13 May 2026) use TanStack Start, which runs a Node server. The backend is Lovable Cloud, built on Supabase.
  - Lovable's own docs list self-hosted Supabase as a supported place to move the backend. If we self-host it, the row level security weakness everyone writes about becomes something we can actually test in scope.
- **Downs:**
  - 30 credits a month is tight. We would need to write a good prompt up front and not waste credits on small fixes.
  - Self-hosting Supabase adds a Phase 3 task. Supabase lists 4 GB RAM minimum (8 GB recommended), which has to fit on the Alienware next to the Kali VM.

### Dyad
- **Free plan:** free and open source (Apache 2.0, except a separate "pro" folder). Runs on our own computer. Latest release v1.16.0, 21 Sept. 2026.
- **Model:** we bring our own. It works with local models through Ollama (free) or API keys (Gemini, OpenAI, Anthropic).
- **Ups:**
  - Works like Lovable (prompt in, full app out) but everything stays on our machines.
  - Generates standard Next.js. Supabase or Neon is optional.
  - Active project.
- **Downs:**
  - Setup time, and results depend on which model we plug in.
  - We have not checked how well a local model runs on the Alienware, or the current Gemini API free limits.

### Bolt.new
- **Free plan:** 1M tokens a month, 300K a day. Includes databases and hosting.
- **Getting the code out:** syncs to GitHub.
- **Ups:** fast, builds front end and back end together, and the free plan is generous.
- **Downs:**
  - The default backend is **Bolt Database**, a Postgres database hosted on Bolt's cloud. Using Supabase instead is only on the Pro and Teams plans.
  - Bolt Database is built on Supabase. Moving it off Bolt means "claiming" it into Supabase (paid plans) or rebuilding the backend on self-hosted Supabase ourselves.
  - So Bolt has the same hosted-backend problem as Lovable, with less documentation on moving it. Our Phase 1 doc says Bolt "exports code to any host". That's true for the front end, but not for the default database.

### v0 (Vercel)
- **Free plan:** $5 of credits a month, 7 messages a day. GitHub sync is included.
- **Ups:** clean Next.js, Tailwind, and shadcn/ui code, which is easy to read when we trace a bug back to what the AI wrote.
- **Downs:**
  - 7 messages a day is very slow for building a whole site.
  - Databases come through Vercel Marketplace add-ons (Neon, Supabase, Upstash), which are hosted services.

### Replit Agent
- **Free plan (Starter):** daily Agent credits up to a monthly cap. The pricing page does not publish the numbers. 1 free published app, which expires after 30 days.
- **Getting the code out:** download as zip, or sync to GitHub.
- **Ups:** the easiest way to get a working full-stack app.
- **Downs:** it's built around Replit's own hosting and database, so moving it to our VM is extra work. The free credit amount is unclear.

### Google AI Studio (Build mode)
- **Free plan:** free to use with Google's free models. Paid models cost money.
- **Getting the code out:** download as zip, or two-way GitHub sync.
- **Ups:** builds a React front end plus a Node.js server, and it's free.
- **Downs:**
  - The database is Firebase Firestore, which Google hosts, so it's out of scope.
  - Apps it builds often call the Gemini API. That adds an AI feature, and with it a whole separate set of risks (the OWASP LLM Top 10).

### bolt.diy
- **Free plan:** free and open source (MIT). Runs on our machine with Docker, pnpm, or a desktop app. We bring the model (Ollama, Gemini, OpenRouter, and others).
- **Getting the code out:** download as zip.
- **Ups:** an open version of Bolt with no hosted database lock-in.
- **Downs:** it's slowing down. The last release was v1.0.0 in May 2025, and the last commit was 7 Feb. 2026. There's also more setup than Dyad.

## Coding agents (write code into a folder on our machine)

These all score "Partial" on criterion 5. Our Phase 1 doc worries that with these tools the team makes the decisions, not the AI.

One way around that: give the agent one plain feature prompt, accept whatever design it picks, and log every prompt. Deng et al. (2026) studied apps built with Claude Code as vibe-coded apps, so the research does count agent-built apps. That's a team call.

### Gemini CLI
- **Free plan:** free and open source (Apache 2.0). 60 requests a minute and 1,000 a day with a personal Google account.
- **Ups:** the most generous free option. It builds in whatever stack we ask for (for example Node + SQLite), so the whole backend runs on our VM with nothing hosted.
- **Downs:** a terminal tool, so building means more back and forth.

### Google Antigravity
- **Free plan:** $0 for individuals, with "basic weekly rate limits". Models include Gemini and Claude Sonnet and Opus 4.6.
- **Ups:** an agent-first code editor with strong models for free.
- **Downs:** weekly limits could stop us mid-build. We didn't dig into how its agent works day to day.

### GitHub Copilot
- **Free plan:** Copilot Free has a small monthly allowance with agent mode included. GitHub's plans page says 2,000 completions and 50 chat requests; the docs now describe it as "an allowance of GitHub AI Credits." Copilot Student is also free for verified students.
- **Ups:** we already use GitHub.
- **Downs:** the free allowance is small. On the student plan you can't pick models, only "auto". Check that your student verification is active before counting on it.

### Cursor
- **Free plan:** Hobby, "limited Agent requests". No number is published.
- **Downs:** we can't plan around a limit we don't know.

## Tip for whichever tool we pick

Put one fixed line in the first prompt:

> "The app must run self-contained on our own offline Linux server, with a local database and no third-party login or storage services."

That's a deployment rule, not a security decision, so the AI still makes the choices we are studying (criterion 5). Without it, most of these tools default to hosted services.

Also plan for installing packages. The VM has no internet access, so npm packages and any Docker images (like self-hosted Supabase) have to be pulled during setup or copied in.

## Suggested shortlist for the trial (section 2.3)

Section 2.3 says we trial the two best options with the same prompt. Based on the scorecard:

1. **Lovable with self-hosted Supabase.** The strongest research angle: the most published work to compare with, and it makes row level security testable. The risk is the 30-credit limit and the extra Supabase setup.
2. **Dyad.** Everything local and free, and still a "prompt in, app out" builder. The risk is setup time and model quality.

**Backup:** Gemini CLI, if both of those eat too much time, with the one-prompt rule above.

This is a suggestion, not the decision. The pick goes in section 2.4 once we've both tried them.

## Corrections to our Phase 1 doc (section 2.1)

Found while checking the tools. Not changed in the Phase 1 doc yet, since we should agree first.

- **Bolt.new:** the default database is Bolt's hosted Bolt Database, and the Supabase option is paid. So "exports code to any host" is only half true.
- **Lovable:** row level security *can* be in scope if we self-host Supabase. Also, the direct code download is paid only, so we would use GitHub sync.
- **Cursor or Claude Code:** Claude Code has no free plan (Pro, $20 a month). Cursor's free plan has unpublished limits.

## Sources (checked 28 Sept. 2026)

- Bolt pricing: https://bolt.new/pricing
- Bolt Database docs: https://support.bolt.new/cloud/database
- Bolt Database advanced settings: https://support.bolt.new/cloud/database/advanced
- Lovable pricing: https://lovable.dev/pricing
- Lovable GitHub sync docs: https://docs.lovable.dev/integrations/github
- Lovable hosting and ownership docs: https://docs.lovable.dev/tips-tricks/deployment-hosting-ownership
- v0 pricing: https://v0.app/pricing
- v0 docs: https://v0.app/docs/llms.txt
- Replit pricing: https://replit.com/pricing
- Replit Starter plan docs: https://docs.replit.com/billing/plans/starter-plan
- Replit projects and files docs: https://docs.replit.com/help/projects-and-files
- Google AI Studio Build mode: https://ai.google.dev/gemini-api/docs/aistudio-build-mode
- Firebase Studio sunset notice: https://firebase.google.com/docs/studio/get-started
- Dyad: https://www.dyad.sh/
- Dyad repo: https://github.com/dyad-sh/dyad
- bolt.diy repo: https://github.com/stackblitz-labs/bolt.diy
- Gemini CLI: https://github.com/google-gemini/gemini-cli
- Google Antigravity pricing: https://antigravity.google/pricing
- GitHub Copilot plans: https://docs.github.com/en/copilot/get-started/plans
- Cursor pricing: https://cursor.com/pricing
- Claude pricing: https://claude.com/pricing
- Base44 GitHub sync docs: https://docs.base44.com/developers/app-code/local-development/github
- Anything plans: https://www.anything.com/docs/account/subscriptions
- Supabase self-hosting with Docker: https://supabase.com/docs/guides/self-hosting/docker
