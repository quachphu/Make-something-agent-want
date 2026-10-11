# InsForge (and InstaCloud): Sponsor Profile for the "Agent-Native Cloud" Track

Research date: 2026-10-11. Method note: insforge.dev, docs.insforge.dev, dev.to, HN mirrors and the press sites did not load directly from this environment (DNS/proxy failures). GitHub pages loaded directly and are primary sources. Everything else comes from search-engine extracts of the cited URLs, so treat exact wording as close paraphrase, not verified quotation.

**Important for participants:** the two track judges, **Hang Huang (co-founder/CEO)** and **Tony Chang (co-founder)**, are InsForge's founders. So the judges are the people who designed the product, and they will know straight away whether a project really uses the platform.

## 1. What is InsForge? Company, founders, YC, funding, traction

### Takeaway
The brief's description is correct but out of date. InsForge is an Apache-2.0, open-source "backend platform for agentic coding": Postgres, auth, storage, model gateway, edge functions, realtime, site hosting and compute, all operated by coding agents through MCP and a CLI plus Skills. On 2026-09-29 the company announced an $8M seed round and a new hosted product, **InstaCloud**, pitched as "the agent-native serverless cloud". That launch is almost certainly why the track is called "Agent-Native Cloud". InsForge is in YC's Spring 2026 batch (P26/X26 naming varies).

### Cited Findings
- Main repo description: "The all-in-one, open-source backend platform for agentic coding". It gives a coding agent database, auth, storage, compute, hosting and an AI gateway to ship full-stack apps end to end. **13.1k stars, 1.2k forks, about 5,575 commits, Apache-2.0** (fetched 2026-10-11). Topics include ai-agents, postgresql, pgvector, realtime and websockets. — [GitHub InsForge/InsForge](https://github.com/InsForge/InsForge)
- Star history from third parties: about 10.7k in May 2026 and about 12.3k later. — [pasqualepillitteri.it (via search)](https://pasqualepillitteri.it/en/news/3573/insforge-2-8x-token-claude-code-backend-agent-native-2026-en)
- Founders: **Hang Huang**, co-founder and CEO, formerly a senior technical PM at Amazon, Yale MBA. **Tony Chang**, co-founder, built networking infrastructure at Databricks after working at Meta and Amazon. The team joined YC's Spring 2026 batch. — [Dealroom (via search)](https://dealroom.co/news/158042-insforge-raises-8m-seed-to-build-cloud-infrastructure-for-ai-agents/)
- YC profile reportedly lists the company as "InsForge (InstaCloud)" in the Spring 2026 batch. — [progressiverobot.com (via search)](https://www.progressiverobot.com/2026/09/29/instacloud-agent-native-serverless-cloud-coding-agents/)
- Hang Huang on X, 2026-09-29: "We just raised an $8M seed round to kill AWS, GCP, and Azure. Introducing [link], the agent-native serverless cloud. Your team is shipping code like never before. But you're getting caught up in manual, tedious DevOps work trying to deploy it…" Y Combinator's account retweeted it. — [X @hanghuang_](https://x.com/hanghuang_/status/2104949571789148416); [X @ycombinator RT](https://x.com/ycombinator/status/2104955815967027406)
- The seed announcement named no investors and gave no valuation. Runtimewire notes the earlier public financing was a $1.5M pre-seed. — [Runtimewire (via search)](https://runtimewire.com/article/instacloud-8m-seed-agent-cloud)
- Pre-seed (2025) led by MindWorks Capital, with Baidu Ventures also named and Vision Capital as financial advisor. Dealroom gives US$970.6K, which conflicts with Runtimewire's $1.5M and VCBacked's "$1.5M total". — [TechLeap](https://finder.techleap.nl/news/feed/insforge-secures-multi-million-usd-funding); [VCBacked](https://www.vcbacked.co/company/insforge); [Fast AI Jobs ($8.97M total disclosed)](https://www.fastaijobs.com/companies/insforge)
- Location: most sources say San Francisco. Preqin says founded in 2025 in Seattle. — [Preqin](https://www.preqin.com/data/profile/asset/insforge-ai--inc-/778681)
- Original launch blog post is dated 2025-11-18. — [InsForge Launch blog](https://insforge.dev/blog/insforge-launch)
- InsForge 2.0 launched 2026-03-09. The company said "almost 99% of all operations and requests now come from agents instead of humans", which is why it made agent experience the core of the product. — [InsForge V2 blog](https://insforge.dev/blog/insforge-launch-v2); [Hang Huang LinkedIn](https://www.linkedin.com/posts/hang-huang-oliver_introducing-insforge-20-the-backend-for-activity-7436792293686198272-ky5F)
- Show HN, "InsForge – Open-source Heroku for coding agents", posted by co-founder Hang: "a backend platform designed for coding agents to deploy, operate, and debug end-to-end". It lists frontend hosting, backend servers (microVM-based), DB, auth, storage, LLM model router, cron jobs, realtime, edge functions and vector. The headline feature is **backend branching**: the agent works on a copy of the whole backend and a human reviews diffs before merging. 62 points when indexed. Gigazine covered it on 2026-06-14. — [HN mirror](https://hn.svelte.dev/item/48181342); [Gigazine](https://www.gigazine.net/gsc_news/en/20260614-insforge)
- A third-party article (around mid-2026) describes the team as "five people, six months old" with a small plugin ecosystem. — [pasqualepillitteri.it](https://pasqualepillitteri.it/en/news/3573/insforge-2-8x-token-claude-code-backend-agent-native-2026-en)
- Partnerships and distribution: Zeabur partnership ("Agent-Native Backend"). One-click deploys on Railway, Zeabur, Sealos, RepoCloud and ZopDay. Hostinger VPS template. Vercel OSS Program badge. — [Zeabur blog](https://zeabur.com/blogs/zeabur-insforge-partnerships); [GitHub README](https://github.com/InsForge/InsForge); [Hostinger](https://www.hostinger.com/vps/docker/insforge)

### Inferences
- Product timeline: open-source backend-as-a-service (Nov 2025), then 2.0 with CLI, Skills and remote MCP (Mar 2026), then compute, branching and Show HN (around Jun 2026), then InstaCloud, a hosted agent-native serverless cloud (Sep 2026). The October hackathon is about two to three weeks after the InstaCloud launch, so the founders will most likely want projects that showcase InstaCloud and cloud features: deploys, compute, branching, guardrails.
- The fair framing is "agent-operated Supabase/Heroku/Vercel in one". Calling it only a Supabase alternative understates the compute, hosting and branching side.

### Gaps
- The InstaCloud product URL could not be confirmed. The tweet uses a t.co link and no official InstaCloud page or press release was reachable. Check whether it is a separate domain or a rebrand of insforge.dev cloud before the event.
- Seed investors, valuation and revenue or user counts are undisclosed.
- No Product Hunt data was retrieved.

## 2. Core architecture, MCP server, CLI/Skills, SDK, self-hosting, pricing

### Takeaway
Agents use InsForge through three layers: **Skills** (static knowledge loaded into the agent's context), the **CLI** (`@insforge/cli`, deterministic execution with `--json` output; the recommended path on cloud), and the **MCP server** (`@insforge/mcp`, live inspection of backend state, especially `get-backend-metadata`). Apps call the backend through the TypeScript SDK `@insforge/sdk`, which has a Supabase-like API, or through REST/PostgREST. Self-hosting is Docker Compose on port 7130. Cloud has a free tier and Pro at about $20–25/mo.

### Cited Findings
**Services and products** — [GitHub README](https://github.com/InsForge/InsForge)
- Authentication (users, sessions, OAuth for Google and GitHub). Database (Postgres, with PostgREST in the stack). Storage (S3-compatible). Model Gateway (OpenAI-compatible API across LLM providers). Edge Functions (Deno). Compute (private preview, long-running containers). Site Deployment (build and host).
- The Show HN post adds cron jobs/schedules, realtime, vector (pgvector) and microVM backend servers. — [HN mirror](https://hn.svelte.dev/item/48181342)
- Agent interfaces: an **MCP Server** (self-hosted and cloud) and **CLI + Skills** (cloud only, per the README). — [GitHub README](https://github.com/InsForge/InsForge)
- Third-party summary of the three layers: Skills for static knowledge, CLI for deterministic execution, MCP for live state. — [pasqualepillitteri.it (via search)](https://pasqualepillitteri.it/en/news/3573/insforge-2-8x-token-claude-code-backend-agent-native-2026-en)

**MCP server** — [GitHub InsForge/insforge-mcp](https://github.com/InsForge/insforge-mcp)
- npm `@insforge/mcp`, installer `@insforge/install`. Supported clients include claude-code, cursor, windsurf, cline, roocode and trae.
```bash
npx @insforge/install --client claude-code --env API_KEY=your_api_key --env API_BASE_URL=http://localhost:7130
```
```json
{
  "mcpServers": {
    "insforge": {
      "command": "npx",
      "args": ["-y", "@insforge/mcp@latest"],
      "env": { "API_KEY": "your_api_key", "API_BASE_URL": "http://localhost:7130" }
    }
  }
}
```
- Known tools: `fetch-docs` (docType such as "instructions", which should be called first, plus "db-sdk", "storage-sdk", "functions-sdk"); `get-backend-metadata` (returns the whole backend's metadata as text: tables, buckets, functions and so on); `run-raw-sql` (admin, can modify data); `create-bucket` (public or private). — [Glama tool index](https://glama.ai/mcp/servers/InsForge/insforge-mcp/tools/get-backend-metadata); [Glama fetch-docs](https://glama.ai/mcp/servers/InsForge/insforge-mcp/tools/fetch-docs); [Smithery](https://smithery.ai/server/devel/insforge)
- The README's verification prompt: "I'm using InsForge as my backend platform, call InsForge MCP's fetch-docs tool to learn about InsForge instructions." — [GitHub README](https://github.com/InsForge/InsForge)
- InsForge 2.0 added **remote MCP servers hosted by InsForge with OAuth** and a VS Code extension. — [InsForge V2 blog (via search)](https://insforge.dev/blog/insforge-launch-v2)

**CLI** (`@insforge/cli`; "the recommended way for agents to use InsForge") — [GitHub InsForge/CLI](https://github.com/InsForge/CLI); [InsForge V2 blog](https://insforge.dev/blog/insforge-launch-v2)
- Command groups: login/whoami; create/link/metadata/logs/docs; `local start|stop|status`; **`branch list|create|switch|merge|reset|delete`**; `db query|tables|policies|migrations|rpc|export|import`; `functions deploy|invoke`; `storage create-bucket|upload`; `deployments deploy|status|env`; `domains` (Cloudflare buy and attach); `payments stripe|razorpay`; `secrets`; `schedules`; `compute deploy|start|stop|logs`; `diagnose advisor|db|logs|metrics|incident`; `config export|plan|apply`; `ai setup`; plus PostHog and Apify integrations. Most commands accept `--json` and `-y`.
```sh
npx @insforge/cli login
npx @insforge/cli link
npx @insforge/cli db query "SELECT * FROM users LIMIT 10"
npx @insforge/cli functions deploy my-function --file ./handler.ts
npx @insforge/cli storage create-bucket images
npx @insforge/cli deployments deploy ./dist --json
```

**Agent Skills** — [GitHub InsForge/insforge-skills](https://github.com/InsForge/insforge-skills); [Skills+CLI blog](https://insforge.dev/blog/insforge-skills-cli)
- Install: `npx -y skills add insforge/insforge-skills`. In Claude Code: `/install-skills insforge/insforge-skills`. In Codex: `codex plugin marketplace add InsForge/insforge-skills` then `codex plugin add insforge@insforge`.
- Four skills: `insforge` (full-stack building: DB, auth, storage, functions, AI, realtime, payments, deploys), `insforge-cli`, `insforge-debug`, and `insforge-integrations` (Auth0, Clerk, Kinde, Stytch, WorkOS, Better Auth, OKX x402 payments).
- Skills install into `.agents/skills/insforge/` and cover 9 modules. InsForge's stated rationale is that skills "encode common workflows and CLI patterns so agents don't spend tokens discovering MCP tools".

**TypeScript SDK** (`@insforge/sdk`) — [GitHub InsForge/insforge-sdk-js](https://github.com/InsForge/insforge-sdk-js)
```ts
import { createClient } from '@insforge/sdk';
const insforge = createClient({ baseUrl: 'http://localhost:7130', anonKey: 'your-anon-key' });
await insforge.auth.signUp({ email, password, name });
await insforge.auth.signInWithOAuth('google', { redirectTo: 'http://localhost:3000/dashboard' });
await insforge.database.from('posts').insert([{ title: 'My First Post', content: 'Hello World!' }]);
await insforge.database.from('posts').select('*').eq('author_id', userId);
await insforge.storage.from('avatars').upload(file);
await insforge.functions.invoke('my-function', { body: { key: 'value' } });
const c = await insforge.ai.chat.completions.create({ model: 'anthropic/claude-3.5-haiku', messages: [...] });
const img = await insforge.ai.images.generate({ model: 'google/gemini-3-pro-image-preview', prompt: '...' });
```
- AI methods return the response directly and throw on error. Other methods return `{ data, error }`. `@insforge/sdk/ssr` exists for SSR session sharing.

**Self-hosting** — [GitHub README](https://github.com/InsForge/InsForge)
```bash
curl -fsSL https://raw.githubusercontent.com/InsForge/InsForge/main/deploy/setup.sh | sh -s ~/insforge
cd ~/insforge && docker compose up -d   # dashboard at http://localhost:7130
```
- Optional MinIO or RustFS storage overlays. Key env vars: `JWT_SECRET`, `ACCESS_API_KEY`, `ACCESS_ANON_KEY`, `API_BASE_URL`. Ports are configurable: POSTGRES, POSTGREST, APP, AUTH, DENO.

**Pricing** (conflicting; verify on the day)
- Feb 2026: two tiers. Free is $0 with 2 projects on dedicated instances. Pro is $25/mo plus pay-as-you-go. — [Pricing update blog](https://insforge.dev/blog/insforge-pricing-update)
- Jun 2026 free tier expansion, per free project per month: 600 build minutes, 120 hours of standard compute, 100k edge function calls. — [Bigger Free Tier blog](https://insforge.dev/blog/bigger-free-tier)
- Docs FAQ: Free includes $1 of AI credits. Pro is $25/mo with $10 of AI credits. Enterprise is custom. — [docs pricing](https://docs.insforge.dev/pricing.md)
- Third-party listings say Pro is $20/mo billed yearly. — [modern-datatools](https://www.modern-datatools.com/tools/insforge/pricing)
- InstaCloud: Huang's post reportedly offers $10/mo of free compute. Runtimewire reports a free tier and a $20/mo minimum for Pro. — [Runtimewire (via search)](https://runtimewire.com/article/instacloud-8m-seed-agent-cloud)

### Inferences
- How agents get "context": `get-backend-metadata` (MCP) or `insforge metadata` (CLI) dumps the whole backend state (schema, buckets, functions, auth config) in one call. Docs come via `fetch-docs` or `insforge docs`, and Skills preload the usage patterns. This is the "context-first" design their benchmark posts credit.
- For a 24–36 hour hackathon, the fastest path is a cloud project, then `npx skills add insforge/insforge-skills` plus `npx @insforge/cli login && link` inside Claude Code, Codex or Cursor. Add MCP if you also want live introspection. Self-hosting is a fallback in case of Wi-Fi or cloud quota problems.
- The $1,000 in cloud credits prizes are probably InsForge/InstaCloud credits.

### Gaps
- No full current MCP tool list beyond the four confirmed tools. Newer versions likely expose more (functions, deployments, logs); check `docs.insforge.dev/mcp-setup.md`.
- No realtime SDK code was verified. Check the docs or SDK-REFERENCE.md.
- InstaCloud's exact API for guardrails and approvals is unverified (see section 3).

## 3. What "agent-native cloud" means to InsForge, plus its benchmarks and launch posts

### Takeaway
To InsForge, "agent-native" means the agent, not the human, is the main operator. The backend is exposed as a context-efficient toolset (Skills + CLI + MCP) rather than a dashboard. Agents can read the full backend state, act deterministically, debug with logs and diagnostics, and work on **branches** of the whole backend while humans approve risky changes. InstaCloud carries this to compute: scale-to-zero serverless, Postgres branches in seconds, and guardrails that route sensitive infrastructure changes to human approval. Their main evidence is self-run **MCPMark** results against Supabase MCP.

### Cited Findings
- InstaCloud gives agents (Claude Code, Codex, Cursor) serverless compute that scales to zero, Postgres DBs that "branch in seconds", and guardrails that decide which infrastructure changes need human approval. — [progressiverobot.com, 2026-09-29 (via search)](https://www.progressiverobot.com/2026/09/29/instacloud-agent-native-serverless-cloud-coding-agents/)
- Dealroom: InstaCloud lets agents provision DBs, storage and compute, and sensitive operations require human approval. — [Dealroom (via search)](https://dealroom.co/news/158042-insforge-raises-8m-seed-to-build-cloud-infrastructure-for-ai-agents/)
- Wall St Engine: "if an agent builds an app, it can deploy directly to InstaCloud without developers" manually provisioning infrastructure. — [X @wallstengine](https://x.com/wallstengine/status/2104963160511766649)
- The Nov 2025 launch roadmap listed "backend branching and versioning: staging/sandbox environments with human approval" as future work. By the Show HN and CLI docs it had shipped (`branch create|switch|merge|reset`). — [Launch blog (via search)](https://insforge.dev/blog/insforge-launch); [GitHub CLI](https://github.com/InsForge/CLI)
- **MCPMark v1 (Sonnet 4.5)**, 21-task Postgres suite: InsForge Pass^4 47.6%, Postgres MCP 38.1%, Supabase MCP 28.6%. Tokens: 8.2M, 10.4M and 11.6M respectively. Headline: "1.6x faster, 30% fewer tokens, up to 70% higher Pass^4 accuracy" than Supabase. — [InsForge blog: MCPMark results](https://insforge.dev/blog/mcpmark-benchmark-results)
- **MCPMark v2 (Sonnet 4.6)**: InsForge Pass^4 42.86% vs Supabase 33.33%. Pass@1 58.33% vs 47.62%. Pass@4 76.19% vs 66.67%. Tokens 7.3M vs 17.9M (2.4x fewer). About 1.3x faster per task. — [InsForge blog: MCPMark v2](https://insforge.dev/blog/mcpmark-benchmark-results-v2); [dev.to mirror](https://dev.to/carmen_dou/mcpmark-v2-insforge-on-sonnet-46-304j)
- Their explanation, a "context-first MCP design" (agents get structured backend context up front), reduces failures on backend tasks. — [Context-first MCP blog](https://insforge.dev/blog/context-first-mcp-design-reduces-agent-failures); [Structured backend stack blog](https://insforge.dev/blog/building-structured-backend-stack-for-ai-coding-agents)
- A third-party headline claims InsForge "cuts Claude Code token usage by 2.8x". — [pasqualepillitteri.it](https://pasqualepillitteri.it/en/news/3573/insforge-2-8x-token-claude-code-backend-agent-native-2026-en)

### Inferences
- The benchmarks are vendor-run, the sample is small (21 tasks x 4 runs) and nobody has replicated them independently. Still, they show what the judges care about: **agent reliability (pass^k) and token and context efficiency**. A demo that measures these (for example "our agent finished X with N tokens and 0 human fixes") speaks their language.
- The "agent-native cloud" values to target in a demo: (1) the agent provisions and deploys with no dashboard clicks; (2) the agent reads backend state, not guesses; (3) safe autonomy through branches, diffs and human approval for risky changes; (4) scale-to-zero, so many agent-spawned apps cost little; (5) self-debugging through logs, `diagnose` and advisors.

### Gaps
- Official InstaCloud docs and guardrail policy configuration were not found. It is unclear whether guardrails are exposed via API, CLI or dashboard.
- The full text of the MCPMark blog methodology could not be read directly (fetch blocked).

## 4. Project ideas likely to score well on the "Agent-Native Cloud" track

### Takeaway
The strongest entries will make InsForge/InstaCloud the substrate that an agent operates on its own: provisioning, branching, deploying, observing and repairing infrastructure. Using it only as a database behind a normal app will score lower. Build with the CLI + Skills + MCP in Claude Code or Codex. Show branching and human-approval guardrails. Measure reliability or token efficiency.

### Cited Findings
- The judges are the founders (per the brief), and the company's own thesis is that 99% of operations come from agents — [InsForge V2 blog](https://insforge.dev/blog/insforge-launch-v2). Branching with human diff review is the "standout feature" — [HN mirror](https://hn.svelte.dev/item/48181342). InstaCloud's pitch is removing DevOps after agents write code — [X @hanghuang_](https://x.com/hanghuang_/status/2104949571789148416).
- Primitives available to an agent: `branch create/merge/reset`, `deployments deploy`, `compute deploy`, `schedules`, `secrets`, `diagnose`, `domains buy-and-attach`, `payments stripe`, `config plan/apply`, plus the model gateway. — [GitHub CLI](https://github.com/InsForge/CLI)

### Inferences (project ideas, ranked by fit)
1. **"Prompt-to-production SaaS factory"**: an agent turns a one-line idea into a deployed app with auth, DB, Stripe payments and a custom domain, entirely through the InsForge CLI and MCP. It works on a backend branch, posts a schema and policy diff to the human for approval, then merges and deploys. Demo it live with a token and time counter. This covers every service and the branching and guardrail story.
2. **Self-healing on-call agent**: a scheduled job watches `diagnose`, logs and metrics. When something fails it opens a branch, reproduces the issue, patches the edge function or migration, runs checks, and asks for approval to merge. "Agents operating the cloud", not just building on it.
3. **Agent sandbox-per-task platform**: each user request or agent task gets an ephemeral InsForge branch or project (scale-to-zero), for example a multi-agent eval harness or a "PR preview backends for agents" tool. Uses branching as the main mechanic.
4. **Guardrail and policy layer for agent infrastructure changes**: a policy engine (cost limits, destructive-SQL detection, RLS checks) that sits on `config plan/apply` and `branch merge`, with a Slack or mobile approval UI. This extends InstaCloud's "human approval" idea and directly helps the sponsor.
5. **Backend MCP benchmark or context compiler**: extends their MCPMark story, for example by auto-generating compact backend context or skills from `get-backend-metadata` and showing pass^k and token gains. Risky as a demo but matches the judges' interests.
6. **Agent-facing app where the users are agents**: a backend whose clients are other agents (an x402-paid API via `insforge-integrations`, or an agent memory store using pgvector and the model gateway), deployed on InstaCloud. Fits the hackathon's "Make Something Agents Want" theme.
- Practical tips: start a project before the event, install the Skills, and confirm free-tier limits (2 projects; compute hours). Keep a recorded fallback demo. Name the specific InsForge features used in the pitch (branching, metadata context, scale-to-zero compute). Quantify agent autonomy: number of human interventions, tokens, time to deploy.

### Gaps
- The official judging rubric for this track was not found. These ideas are inferred from company messaging, not stated criteria.
- No examples of past InsForge hackathon winners were found.
