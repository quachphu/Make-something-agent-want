# Armature (armature.tech): sponsor profile for the "Best Agent Experience (AX)" track

Research date: 2026-10-11. Method note: armature.tech, docs.armature.tech, ycombinator.com, news.ycombinator.com and runtimewire.com could not be fetched directly from this environment (DNS failures), so facts about those pages come from search-engine summaries of them. These are flagged "(via search snippet)". Armature's public GitHub repos were cloned and read directly (READMEs, SKILL.md files, source), and that is the strongest evidence below. Armature is a different company from Armature Systems, Armature (3D/animation) and others with the name. Everything here is about **armature.tech / GitHub org `armature-tech`**.

## 1. What is Armature? (product, problem, customers, YC batch, founders, funding)

### Takeaway
Armature (YC Spring 2026, "P26") is a 3-person, Paris-based startup (some listings say SF) founded by Theodore Otzenberger (ex-Palantir FDE, founding engineer at Tsuga) and Louis Scremin (ex-Joko AI agents). Its pitch is "agents are now your users." It started as automated testing of how agents use your MCP server or CLI. It moved to product analytics plus evals for MCP sessions (Jul–Aug 2026). It now sells "get your product picked by coding agents" (agent distribution / "agent SEO"), with agent.reviews ("G2 for agents") as a public wedge (Oct 2026).

### Cited Findings
- YC company page title / one-liner: "Armature: We get your product picked by coding agents." (via search snippet) — [YC company page](https://www.ycombinator.com/companies/armature)
- Homepage title: "Armature · Get discovered and used by coding agents" (via search snippet) — [armature.tech](https://armature.tech/)
- Launch YC post title: "Armature – Making your app finally usable by AI agents." It describes the product as helping companies "monitor, analyze, and optimize how AI agents experience their products": it discovers a product through MCP and CLI, runs the workflows customers' agents perform, exposes the agents' reasoning traces, and gives analytics, benchmarks and suggested fixes for MCP and CLI interfaces. It offers a free self-serve trial (via search snippet). — [Launch YC](https://www.ycombinator.com/launches/QQc-armature-making-your-app-finally-usable-by-ai-agents)
- An earlier YC listing description: automated testing for agent workflows. You connect an MCP server, CLI or ChatGPT app, and it finds the workflows agents run and tests them across harnesses such as Claude Code and Codex (via search snippet). — [YC company page](https://ycombinator.com/companies/armature)
- The YC profile says coding agents (Claude Code, Codex, Cursor) now decide which tools get installed in a codebase. Armature runs real agents across a panel of repositories to measure whether they pick a given product. A "pick" counts only when the agent installs the product and wires it in. Agents run in sandboxes and nothing runs in the customer's codebase or accounts. Armature then proposes docs, SDK and content changes for the customer to approve (via search snippet). — [YC company page](https://www.ycombinator.com/companies/armature)
- Public "Distribution agent-choice test" fixtures on GitHub (June 2026) are synthetic repos with open-ended requirements. Example: a Next.js + Drizzle SaaS whose README says "Pick the database/provider strategy you would use and outline the changes you would make" (Neon-themed fixtures: preview branches, vector search, auth previews). Others are default Next.js, Vite React and SvelteKit fixtures. — [armature-tech/distribution-fixture-neon-preview-branches](https://github.com/armature-tech/distribution-fixture-neon-preview-branches), [armature-tech GitHub org](https://github.com/armature-tech)
- Founders: Theodore Otzenberger (LinkedIn: "Co-Founder @ Armature (YC P26)"), former FDE at Palantir and founding engineer who built observability at Tsuga (a Datadog spin-off). Louis Scremin scaled AI agents and led AI automation at Joko, a consumer app with about 6M users (via search snippets). — [LinkedIn](https://www.linkedin.com/in/theodore-otzenberger-895345131/), [armature.tech/about](https://armature.tech/about), [YC page](https://www.ycombinator.com/companies/armature)
- Team and location: 3 employees, Paris (via search snippets). Other aggregators list San Francisco. — [YC page](https://www.ycombinator.com/companies/armature); conflicting: [everydev.ai](https://www.everydev.ai/developers/armature-inc)
- Funding: one aggregator lists about $500K raised. This is unconfirmed, though it matches YC's standard deal. Founders Future (a French VC) lists Armature in its portfolio. — [Founders Future portfolio](https://www.foundersfuture.com/en/portfolio/armature), aggregator via [WebSearch summary of YC-backed lists](https://altss.com/companies/yc?page=26)
- The YC Tier List notes there is no public evidence of paying customers, revenue or named beta users. — [yctierlist.com](https://yctierlist.com/s26/armature/)
- On HN, the co-founder self-describes Armature as selling "growth services" to dev tools. The tool-choice study is "part of our broader work on how to influence coding agents choices and get products picked" (via search snippet). — [HN comment](https://news.ycombinator.com/item?id=49557233)
- Timeline (dates from search snippets and repo metadata):
  - 2026-06: `armature-tech/skills` (agent-review skill) and the Distribution fixture repos are created.
  - 2026-07-22: launch, per a trade write-up. — [runtimewire](https://runtimewire.com/article/armature-product-analytics-evals-agent-sessions-mcp)
  - 2026-07-28: Armature Analytics (Show HN). 2026-08-04: Armature Evals (both per an aggregator). — [HN Show HN](https://news.ycombinator.com/item?id=49157807)
  - 2026-09-03: tool-choice study published. — [Armature blog](https://armature.tech/blog/which-tools-coding-agents-install)
  - ~2026-10-03: agent.reviews launch; the `agent-reviews` CLI repo was created 2026-10-03. — [Show HN: Agent.reviews](https://news.ycombinator.com/item?id=49995539), [repo](https://github.com/armature-tech/agent-reviews)

### Inferences
- The company has pivoted or layered fast: testing, then analytics and evals, then distribution and agent.reviews. Judges are likely to care about two things: (a) whether agents can **find and choose** your product, and (b) whether agents **succeed** once they use it. Both should show up in a winning project.
- Likely customers are dev-tool and API companies with an MCP server, CLI or SDK. The Neon-themed fixtures hint at database and infra vendors. No customers are publicly named.

### Gaps
- No confirmed funding amount, investors (beyond the Founders Future listing) or named customers.
- Exact batch label: "P26" vs "Spring 2026" are both reported and appear to mean the same batch.
- Could not read the founders' X/Twitter posts directly.

## 2. Core technology / architecture: APIs, SDKs, CLI, MCP server, pricing

### Takeaway
Armature has four product surfaces:
1. **MCP Analytics SDKs** (open source, Apache-2.0) for TypeScript, Python, Go and PHP. They wrap your MCP server, inject an optional `telemetry` argument into every tool schema, and send per-call events to Armature.
2. **A hosted dashboard plus Evals.** Sessions, use-case clustering, issues and pass rates. A real agent plays the user and an LLM judge scores the runs.
3. **A read-only Armature MCP server** for querying your analytics from Claude Code or Cursor, plus the agent.reviews MCP and CLI.
4. **AI Traffic**, server/edge analytics for AI crawlers (private beta).

There is a "generous free tier," but no public price points were found.

### Cited Findings
- **The SDKs and the telemetry contract:**
  - Packages: `@armature-tech/mcp-analytics` (npm), `armature-mcp-analytics` (PyPI, extras `[fastmcp]` / `[mcp]`), and `github.com/armature-tech/mcp-analytics-go/armatureanalytics` (mark3labs/mcp-go, plus `/official` for the official Go SDK). There is also a PHP SDK. — [packages profile (API Evangelist)](https://github.com/api-evangelist/armature), [mcp-analytics-go](https://github.com/armature-tech/mcp-analytics-go), [mcp-analytics-php](https://github.com/armature-tech/mcp-analytics-php), [PyPI](https://pypi.org/project/armature-mcp-analytics/0.1.40/)
  - How it works:
    - The SDK adds an optional `telemetry` block to each tool's input schema, with `user_intent` and `call_purpose`.
    - The agent fills those fields.
    - The SDK strips telemetry before your handler runs.
    - It sends timing, outcome and truncated input/output previews to the dashboard.
  - "No custom event schema. No logging pipeline. No changes to your tool handlers." — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)
  - `user_intent` should be sent "only on the first call after each new user message." The instructions live in the field descriptions, and the SDK "never adds text to your tool descriptions, as Anthropic's connector directory requires." The `call_purpose` field description tells agents to omit names, identifiers, credentials and argument values. — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics), [src/schema.ts](https://github.com/armature-tech/mcp-analytics/blob/main/src/schema.ts)
  - Supported integration shapes:
    - `createMcpAnalyticsServer(factory)` for an existing McpServer factory
    - `instrumentMcpServerTools`
    - `createAnalyticsRecorder` for custom JSON-RPC dispatchers
    - `wrapMastraTools`
    - fastmcp (`/fastmcp`)
    - Vercel `mcp-handler`
    - `resolveStatelessHttpSession` for serverless
    - MCP SDK v2 (`/v2`, protocol revision 2026-07-28)
    - Python `instrument_fastmcp`

    — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics), [mcp-analytics-python README](https://github.com/armature-tech/mcp-analytics-python)
  - Session reconstruction: session IDs resolve in priority order from `gen_ai.conversation.id` in `_meta` baggage, then the `X-Armature-Session-Seed` header, then `Mcp-Session-Id`, then a stdio process-scoped ID. On stateless transports the SDK mints `mcp_<name>_v_<version>_<uuid>` IDs. An `X-Armature-Workflow-Run-Id` header also exists, apparently for eval/test runs. — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)
  - **The built-in `send_feedback` tool** (on by default; named `request_capability` before 2026-10):
    - It takes one required `capability` string.
    - Its exact description is: "Use this when the user asks for something these tools can't do. It records the request so the developers of this server can add it. It changes no data and contacts no one."
    - Annotations: `readOnlyHint: false`, `destructiveHint: false`, `openWorldHint: false`, `idempotentHint: false`.
    - It feeds "unmet-demand signals."

    — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)
  - Delivery and reliability:
    - `delivery: "background"` (default) or `"await"` (for serverless).
    - 5 s timeout, at most 2 attempts with 100 ms between them. It retries only network errors, 429 and 5xx.
    - Other 4xx errors come back once as a structured `IngestDeliveryError` (`code`, `status`, `retryable`, `attempts`) through `onError`. Fail-open by default.
    - Built-in secret redaction is on by default, with `redact` / `redactEvent` hooks.

    — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics), [SKILL.md](https://github.com/armature-tech/mcp-analytics/blob/main/SKILL.md)
  - Env vars: `ANALYTICS_INGEST_API_KEY` and `ANALYTICS_INGEST_URL` (US `https://app.armature.tech/api/mcp-analytics/ingest`, EU `https://eu.armature.tech/api/mcp-analytics/ingest`). Keys are prefixed `ami_us_` / `ami_eu_`. The SDK silently no-ops without a key. — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)
- **CLI — `doctor`:** `npx @armature-tech/mcp-analytics doctor --url http://localhost:3000/mcp` (or `--command node --arg dist/server.js` for stdio). It:
  - performs the MCP handshake and lists the tools
  - verifies that every tool exposes the telemetry contract
  - authenticates the key with an empty batch
  - compares key, ingest and MCP regions before sending anything

  Flags: `--skip-ingest` for an offline check, `--json` for a "support-ready machine-readable report." — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)
- **Dashboard:**
  - Captures every session on your MCP server, Claude Connector or ChatGPT App (via search snippet). — [docs.armature.tech](https://docs.armature.tech/)
  - Shows reconstructed sessions, use-case ranking from session clustering, and frequent agent issues. Setup is about "three lines of code" (via search snippet). — [Show HN](https://news.ycombinator.com/item?id=49157807)
- **Evals:** you write eval cases, "a real agent plays the user, and a judge scores every run against your criteria." With analytics on, Armature drafts the cases from real use cases and issues (via search snippet). — [docs.armature.tech](https://docs.armature.tech/), [runtimewire](https://runtimewire.com/article/armature-product-analytics-evals-agent-sessions-mcp)
- A third-party profile says Armature compares the same workflow across Claude Code, Codex, Claude, ChatGPT, Cursor, OpenClaw, OpenCode and Gemini CLI. The profile is hedged and less authoritative. — [zeitgeist.bot](https://www.zeitgeist.bot/company/armature)
- **Armature MCP server (read-only):**
  - The docs say "Armature is also an MCP server. Connect it to Claude Code, Cursor, or any MCP client" (via search snippet). — [docs.armature.tech](https://docs.armature.tech/)
  - URLs: `https://app.armature.tech/api/mcp` (US) and `https://eu.armature.tech/api/mcp` (EU). — [doctor tests](https://github.com/armature-tech/mcp-analytics)
  - Tools (from docs.armature.tech/armature-mcp/tools): `list_mcp_servers`, `list_sessions`, `get_session`, `list_use_cases`, `list_issues`, `get_issue`.
  - Entities: MCPServer, Session, UseCase (cluster with volume, pass rate and share), Issue ("grouped by root cause and ranked by blast radius"), and ToolCall.

  — [API Evangelist data model](https://github.com/api-evangelist/armature)
- **OAuth:** mcp.armature.tech and app.armature.tech serve RFC 8414 / RFC 9728 OAuth discovery metadata and support dynamic client registration. API Evangelist's 2026-10-03 "Agent Readiness" score for Armature is 30.9. It credits the verified MCP server, agent skills and protected-resource metadata, and marks idempotency, error semantics, dry-run, OpenAPI and rate-limit signals as absent. A published OpenAPI spec "was retired to an empty stub." — [API Evangelist profile](https://github.com/api-evangelist/armature)
- **agent.reviews:**
  - Agents check reviews before picking a tool and post reviews after using one. The site claims 100,000+ reviews of 6,000+ tools. Reviews pass deterministic secret/PII filters, a leak classifier and a small LLM check. Reading and posting are free, and posting requires sign-in (via search snippet). — [Show HN: Agent.reviews](https://news.ycombinator.com/item?id=49995539), [Digg](https://digg.com/ai/o3wuk1e7)
  - The CLI is `npx @armature-tech/agent-reviews` with `login | check | submit | lookup <tool> | compare <a> <b> | search | category | last | automatic`. All output is JSON. Agents never see the token, which is stored in `~/.armature/agent-review.json`. — [agent-reviews README](https://github.com/armature-tech/agent-reviews)
  - The MCP is `claude mcp add --transport http review https://mcp.armature.tech/mcp/agent-review`, with tool `submit_agent_review`. The HTTP fallback is `POST https://app.armature.tech/api/agent-review`. — [armature-tech/skills](https://github.com/armature-tech/skills)
- **AI Traffic** (`@armature-tech/ai-traffic`) records AI crawler requests at the server or edge (Next.js 16 proxy, Cloudflare, Hono, Express). It is in private beta. Its README leads with "Install with an AI agent" and gives a copy-paste prompt. — [ai-traffic README](https://github.com/armature-tech/ai-traffic)
- **Pricing:** "self-serve, setup <5 min, generous free tier" (via search snippet). The docs have a Pricing page, but its contents could not be retrieved. — [Show HN](https://news.ycombinator.com/item?id=49157807), [docs](https://docs.armature.tech/)

### Inferences
- The `telemetry.user_intent` / `call_purpose` trick is the core technical insight. A server only sees tool calls, so Armature asks the agent to self-report intent through an optional schema field and reconstructs the session from that.
- Hackathon credits ($1,000 / $500 / $300 Armature credits) will most likely be usable on analytics, evals or distribution tests. This is an inference; the credit details are unknown.

### Gaps
- Actual pricing tiers and the credit-to-usage mapping.
- No public REST API or OpenAPI. The MCP server is the programmatic read interface.
- Full docs.armature.tech content (quickstarts, evals config format) could not be fetched.

## 3. Documentation, quickstarts, code examples, GitHub

### Takeaway
The docs live at docs.armature.tech (Mintlify-style: Introduction, SDKs, Armature MCP tools, dashboard pages, Pricing, AI Traffic agent-install guide). The real substance is in the GitHub READMEs. Each SDK ships a `SKILL.md` "Agent install" so a coding agent can do the integration itself. This "agent-installable product" pattern is something the judges clearly value.

### Cited Findings
- Docs page paths seen in the wild:
  - docs.armature.tech/ (Introduction) — [docs](https://docs.armature.tech/)
  - /armature-mcp/tools, /sdks/*, /dashboard/{sessions,use-cases,issues,overview} — [API Evangelist](https://github.com/api-evangelist/armature)
  - /ai-traffic/agent-install — [ai-traffic README](https://github.com/armature-tech/ai-traffic)
- GitHub org `armature-tech` has 22 public repos: mcp-analytics (TS), mcp-analytics-python, mcp-analytics-go, mcp-analytics-php, skills, agent-reviews, ai-traffic and about 14 `distribution-fixture-*` repos. The SDK repos say "Sync from armature-tech/mcp-tester" (a private monorepo). — [GitHub org](https://github.com/armature-tech)
- TypeScript quickstart (verbatim):
  ```ts
  // npm install @armature-tech/mcp-analytics @modelcontextprotocol/sdk@^1.29.0 zod
  import { createMcpAnalyticsServer } from "@armature-tech/mcp-analytics";
  import { createMyMcpServer } from "./server.js";
  const server = createMcpAnalyticsServer(createMyMcpServer);
  ```
  "Make one tool call, open Armature, and the session is already there." — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)
- Python minimal example (verbatim, abridged):
  ```python
  from armature_mcp_analytics import instrument_fastmcp
  from fastmcp import FastMCP
  mcp = FastMCP("armature-minimal-python")
  instrument_fastmcp(mcp, {"armature": {"delivery": "await"}})
  @mcp.tool
  def echo(text: str) -> str:
      """Echo the supplied text."""
      return f"echo: {text}"
  ```
  — [mcp-analytics-python examples/minimal/server.py](https://github.com/armature-tech/mcp-analytics-python)
- Example payload the agent sends:
  `{"telemetry": {"user_intent": "Check whether the customer's last payment succeeded", "call_purpose": "The payment lookup tool provides the requested status"}}` — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)
- How the `SKILL.md` "install-mcp-analytics" skill instructs agents:
  - Classify the repo into one of 4 integration shapes (Mastra / drop-in / registry / dispatcher) "from the code and announce your choice in one line before editing."
  - Match the package manager.
  - Never commit real secrets.
  - Pick `delivery` based on the runtime.
  - Verify the wiring with a test call.

  — [SKILL.md](https://github.com/armature-tech/mcp-analytics/blob/main/SKILL.md)
- Skills install: `npx skills add armature-tech/skills --all` (uses the vercel-labs/skills installer). — [armature-tech/skills](https://github.com/armature-tech/skills)

### Inferences
- A strong hackathon entry should copy Armature's own pattern:
  - a README section addressed to agents
  - a `SKILL.md`
  - a copy-paste "install with your agent" prompt
  - a `doctor`/verify command with `--json`
  - an MCP server for the product's own data

### Gaps
- Could not view rendered docs pages, the changelog or blog index beyond titles.

## 4. Armature's point of view on Agent Experience (AX)

### Takeaway
Armature's view is empirical and behavior-based. AX is measured by what real agents (Claude Code, Codex, Cursor) actually do:
- whether they **discover and pick** your tool
- whether they **complete the workflow** (pass rate, retries, dead ends)
- what they **report** (friction tags).

Their own artifacts show the qualities they reward:
- token-light JSON outputs
- self-verifying setup (`doctor`)
- agent-installable skills
- privacy-safe telemetry
- annotations required by app directories
- a feedback channel for unmet needs
- clear, structured errors.

### Cited Findings
- Tool-choice study (2026-09-03): Armature ran 16,893 sessions across 75 repositories (10 languages, 1,163 prompt variations).
  - The three agents picked the same tool in only 42% of cases.
  - Codex searches the web in about 94% of sessions, Cursor in about two-thirds, and Claude Code in about 30%. Claude Code relies more on prior knowledge.
  - Critics note the headline figures come from a 5,292-session validated subset, and Armature has a commercial interest in the result.

  — [Armature blog](https://armature.tech/blog/which-tools-coding-agents-install), [ai-tldr](https://ai-tldr.dev/releases/armature-coding-agent-tool-choice/), [cursorworkshop critique](https://www.cursorworkshop.com/research/17k-runs-of-claude-codex-and-cursor)
- Otzenberger, quoted in The New Stack: "Twenty years of brand building simply froze in time." The point is that agents default to tools they already know, which bypasses newer brands (via search snippet). — [The New Stack](https://thenewstack.io/coding-agents-tool-choice/)
- Armature publishes per-product pages such as "Do coding agents recommend Docling?" — [armature.tech/library](https://armature.tech/library/do-coding-agents-recommend-docling)
- The agent-review rubric defines Armature's AX dimensions:
  - Scores (1–5): usefulness, ease, reliability.
  - Outcome: `completed | partial | blocked`.
  - The review covers the whole flow "install, authentication, configuration, use, error recovery, and verification."
  - Friction tags: `auth, docs, missing_capability, missing_tool, unclear_error, rate_limit, timeout, install, configuration, permissions, destructive_risk, poor_output, too_slow, flaky, version_conflict, context_required, other`.

  — [agent-review SKILL.md](https://github.com/armature-tech/skills)
- Founder framing for agent.reviews: humans have G2 and Trustpilot, but agents have nowhere to share their experience (via search snippet). — [Show HN: Agent.reviews](https://news.ycombinator.com/item?id=49995539)
- Origin story: the founders built Armature as a testing tool and "had no visibility into how people used its MCP." That led to analytics (via search snippet). — [Show HN](https://news.ycombinator.com/item?id=49157807)
- Design choices visible in Armature's own CLI (agent-reviews):
  - Every command prints JSON.
  - A non-blocking login flow for agents without a terminal ("prints the link and returns… `check` saves the sign-in once you approve").
  - The token is never exposed to agents.
  - A `skill_update` hint is embedded in responses.
  - It respects a human's "no" to automatic reviews (`automatic declined`).

  — [agent-reviews README](https://github.com/armature-tech/agent-reviews)
- Design choices in the SDK:
  - It never pollutes tool descriptions.
  - Field-level instructions.
  - Directory-required annotations (readOnly, destructive, openWorld hints).
  - A `send_feedback` tool for unmet demand.
  - Fail-open telemetry.
  - Structured, payload-free errors (`code`, `status`, `retryable`).

  — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)

### Inferences
- Judges will likely reward evidence: "we ran Claude Code / Codex against our MCP or CLI N times and the pass rate went from X to Y." Instrumenting your project with Armature analytics and showing the sessions dashboard, or an agent.reviews score, would align directly with their worldview.
- Discoverability matters to them as much as usability: llms.txt, skills, an agent-readable README, and being the tool an agent picks unprompted.

### Gaps
- No long-form AX manifesto or blog post by Otzenberger or Scremin was found beyond the study and HN posts. Their tweets were not accessible.

## 5. General AX best practices judges are likely to reward

### Takeaway
The canonical sources are Netlify's AX framing (Access, Context, Tools, Orchestration, plus the AXIS measurement framework) and Anthropic's "Writing effective tools for agents" (choose tools carefully, namespace, return meaningful context, be token-efficient, prompt-engineer descriptions, run evals). Combine these with Armature's friction taxonomy as a checklist.

### Cited Findings
- Netlify CEO Mathias Biilmann coined "Agent Experience" in January 2025: "the holistic experience AI agents will have as the user of a product or platform." His four pillars are Access, Context, Tools and Orchestration. Netlify open-sourced **AXIS** to measure how well a product works for agents. — [Netlify AX](https://www.netlify.com/agent-experience/), [Biilmann on X](https://x.com/biilmann/status/2069818292748140804), [CIO](https://www.cio.com/article/4135922/what-ax-can-do-to-deliver-cohesion-and-uniformity-to-ai-agents.html)
- Anthropic (2025-09-11): "agents are only as effective as the tools we give them." Principles: build prototypes and evals; choose the right tools (not one per API endpoint); namespace them; return meaningful, high-signal context; optimize for token efficiency (pagination, filtering, truncation, concise vs detailed modes); prompt-engineer tool descriptions; use Claude Code to improve tools from eval transcripts. — [Anthropic engineering](https://www.anthropic.com/engineering/writing-tools-for-agents)
- Speakeasy's practical AX guide is another reference for agent-facing API and MCP design. — [Speakeasy](https://www.speakeasy.com/blog/agent-experience-introduction)
- The Agent-Readiness dimensions API Evangelist scores are a useful external checklist: spec presence, MCP server, auth clarity, idempotency, error semantics, OpenAPI examples, rate-limit signals, agent skills, well-known catalog, dry-run mode, delegated identity, protected-resource metadata, dynamic client registration, reversibility documented. — [API Evangelist Kin score](https://github.com/api-evangelist/armature)

### Inferences (checklist synthesized from the sources above)
- **Discoverability:** llms.txt / llms-full.txt, Markdown docs, `SKILL.md` + `npx skills add`, an MCP registry listing, `.well-known` OAuth metadata, and a one-line "install with your agent" prompt.
- **Tool design:**
  - a few workflow-level tools rather than endpoint mirrors
  - consistent namespacing and verb_noun names
  - field-level descriptions with examples
  - MCP annotations (readOnly, destructive, idempotent, openWorld hints)
  - a `send_feedback` / capability-request tool
- **Outputs:** compact JSON by default, a `--json` flag for CLIs, pagination and `limit`, a concise/detailed mode, stable IDs, and next-step hints in responses.
- **Errors:** a structured `{code, message, retryable, hint/fix}`. Keep it actionable ("run `x login`"); never just a stack trace. These map to Armature's `unclear_error` friction tag.
- **Safety:**
  - idempotency keys
  - `--dry-run` / plan-then-apply
  - explicit confirmation for destructive ops
  - scoped tokens that agents never see

  These map to the `destructive_risk` and `permissions` friction tags.
- **Auth for agents:** device-code / link-approval flows that don't block a terminal (Armature's own `login` / `check` pattern), plus OAuth with dynamic client registration for remote MCP.
- **Self-verification:** a `doctor` / `whoami` / `status` command that checks config and returns machine-readable diagnostics.
- **Measurement:** run evals with Claude Code, Codex and Cursor; report pass rate, tool calls per task, tokens and time; instrument with Armature analytics.

### Gaps
- No published judging rubric for the AX track beyond the one-line description, so the criteria above are inferred.

## 6. Project ideas that would score well, and how to integrate Armature

### Takeaway
The best entries will (1) ship a dedicated agent-facing interface (MCP and/or CLI) for a real product, (2) instrument it with Armature's SDK so judges can see real agent sessions and use cases, and (3) prove the AX improved with before/after agent evals or agent.reviews feedback.

### Cited Findings
- The track definition: "Agents can use your product through a dedicated Agent-Facing Interface (MCP, CLI). Build the best experience for them!" Judges are Otzenberger and Scremin. — [YC event page](https://events.ycombinator.com/MakeSomethingAgentsWant)
- Armature can capture sessions from Claude, ChatGPT, Cursor, Codex, Gemini CLI "and the rest" if the client can reach your server (via search snippet). — [docs.armature.tech](https://docs.armature.tech/)
- Integration takes about 3 lines (TS `createMcpAnalyticsServer`, Python `instrument_fastmcp`) plus 2 env vars, with `doctor` for verification. — [mcp-analytics README](https://github.com/armature-tech/mcp-analytics)

### Inferences (idea list)
1. **"AX-first" MCP + CLI for a product.** Build the agent interface for your hackathon product with:
   - a few workflow tools and a `--json` CLI
   - `doctor` and dry-run
   - a `SKILL.md` and llms.txt
   - Armature analytics, with a dashboard demo of the sessions, use-cases and issues it captures.

   Show an iteration loop: an Armature issue (for example, repeated retries on tool X) leads to a rewritten tool description or schema, which raises the pass rate.
2. **AX linter / doctor for MCP servers and CLIs.** A CLI and MCP that scores another MCP server or CLI against the checklist above. It would check annotations, description quality, output token size, error structure and `--json` support, and auto-suggest fixes. This is complementary to Armature, not competitive with it.
3. **Agent-eval harness for CLIs.** Run Claude Code, Codex and Gemini CLI headless against a CLI on fixed tasks. Report completion rate, tool calls, tokens and Armature-style friction tags. This mirrors the Distribution fixture approach.
4. **Agent-installable onboarding.** A product whose entire setup an agent can finish: a non-blocking auth link like agent-reviews `login`/`check`, a scoped token the agent never sees, and a verification step. Demo it with a zero-touch install by Claude Code.
5. **agent.reviews integration.** Have your MCP or CLI surface `lookup`/`compare` data to agents choosing tools, or auto-submit privacy-safe compact reviews of your own product during testing, then display the friction tags.
- What to demo for the judges:
  - a live agent (Claude Code or Codex) using the interface end-to-end
  - the Armature sessions view showing `user_intent` captured
  - a before/after metric
  - the `send_feedback` tool catching an unmet need

### Gaps
- Unknown whether using Armature's product is required or just helpful for the AX track, and how credits are provisioned at the event.
- Unknown whether the judges will run their own agents against submissions.
