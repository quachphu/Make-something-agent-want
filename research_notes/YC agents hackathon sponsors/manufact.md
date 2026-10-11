# Manufact (formerly mcp-use): sponsor profile for the "Best MCP Server for Agents" track

Research date: 2026-10-11. Method note: manufact.com, docs.manufact.com, docs.mcp-use.com, mcp-use.com, ycombinator.com, siliconangle.com and most third-party sites could not be fetched directly from the research sandbox (DNS/proxy blocks). Facts about those pages come from **search-engine snippets** and are marked "(snippet)". Facts marked "(primary, fetched)" were read directly: the mcp-use GitHub README, the docs source files in the `mcp-use/mcp-use` repo (`docs/*.mdx`), the npm and PyPI registries, the Anthropic engineering post, and the MCP blog post on the 2026-07-28 spec.

## 1. What is Manufact? Company, YC batch, founders, funding

### Takeaway
Confirmed: Manufact is the renamed **mcp-use**. It is a YC **S25** company that builds the open-source mcp-use MCP framework (TypeScript and Python) and a hosted "MCP cloud" for deploying MCP servers and MCP Apps (ChatGPT/Claude). It raised a **$6.3M seed led by Peak XV**, announced Feb 12, 2026. Two of the three track judges are on the core team: **Luigi Pederzani** (co-founder) and **Enrico Toniato** (CTO / core contributor). The third, **Andrew Khadder**, is a Founding Engineer.

### Cited Findings
- The YC company page and job listings use the title "Manufact (formerly mcp-use)". The company describes itself as "open-source dev tools and infrastructure for MCP to help dev teams quickly build and deploy MCP Servers for AI agents & MCP Apps for ChatGPT and Claude" (snippet). — [YC: Manufact](https://www.ycombinator.com/companies/manufact); [YC job: Founding SWE](https://www.ycombinator.com/companies/manufact/jobs/x7AI7un-software-engineer-founding-team)
- YC page tagline: "Cloud infrastructure for MCP servers and Claude / ChatGPT plugins" (snippet). YC launch post title: "Manufact (mcp-use): Build and deploy MCP Servers for AI Agents & MCP Apps for ChatGPT/Claude users" (snippet). — [YC](https://www.ycombinator.com/companies/manufact); [YC Launch](https://www.ycombinator.com/launches/O2c-manufact-mcp-use-build-and-deploy-mcp-servers-for-ai-agents-mcp-apps-for-chatgpt-claude-users)
- Batch: YC S25 (snippet). — [ecosistemastartup.com](https://ecosistemastartup.com/manufact-yc-s25-6-3m-para-infraestructura-mcp/); [YC](https://ycombinator.com/companies/manufact)
- Founders: Pietro Zullo and Luigi Pederzani. mcp-use was "born on March 28, 2025" (snippet). The README credits "Built by Pietro (github.com/pietrozullo), Luigi (github.com/pederzh), Enrico (github.com/tonxxd), and the mcp-use community" (primary, fetched). — [everydev.ai](https://www.everydev.ai/developers/manufact); [GitHub README](https://github.com/mcp-use/mcp-use)
- Roles conflict across sources. Crunchbase lists Zullo as CEO and Pederzani as CTO. The seed announcement calls Pederzani co-founder/co-CEO. Tooldirectory names Enrico Toniato as a founder. A July 2026 Manufact blog post carries the byline "Enrico Toniato, CTO" (all snippets). — [Crunchbase](https://www.crunchbase.com/organization/mcp-use); [Manufact seed blog](https://manufact.com/blog/seed-announcement); [tooldirectory.ai](https://tooldirectory.ai/tools/manufact); [Manufact blog index](https://manufact.com/blog/category/all)
- Andrew Khadder has the byline "Founding Engineer" on a Manufact post about building the mcp-use **screenshot CLI**, and he wrote an MCP testing article (snippet). — [Manufact blog](https://manufact.com/blog/category/all)
- Background: Pederzani pivoted his earlier company **Orango**, which aimed to let AI agents use any software product, into mcp-use after MCP appeared. He has described mcp-use as "Vercel for MCP" (snippet). — [Product Hunt @pederzh](https://www.producthunt.com/@pederzh)
- Funding: **$6.3M seed led by Peak XV**, announced Feb 12, 2026, with participation from Liquid 2 Ventures, Ritual Capital, Pioneer Fund and Y Combinator, plus angels. Tooldirectory lists True Ventures instead of Ritual Capital, which conflicts with the other sources (snippets). — [SiliconANGLE, 2026-02-12](https://siliconangle.com/2026/02/12/manufact-raises-6-3m-help-developers-connect-ai-agents-model-context-protocol/); [Manufact blog: seed announcement](https://manufact.com/blog/seed-announcement); [Founder Lodge](https://www.founderlodge.com/round/Manufact-formerly-mcp-use-raises-6300000-Seed-2026-02-13-Pietro-Zullo-MjUzMzM); [Peak XV portfolio](https://www.peakxv.com/companies/mcp-use)
- Location and size conflict: YC lists 5 employees in Zurich, Switzerland. Founder Lodge and tryfundable list San Francisco (snippets). — [YC](https://www.ycombinator.com/companies/manufact); [tryfundable](https://www.tryfundable.ai/company/manufact)
- Traction figures vary by date and source. Reported downloads include 5M+, 6M+, 7M+ and 10M+, and reported stars range from about 9k to 10k (snippets). A Manufact blog post is titled "10,000 GitHub stars". On fetch day the GitHub repo showed **10.7k stars and 1.5k forks** (primary, fetched). — [YC](https://www.ycombinator.com/companies/manufact); [Manufact blog: 10000 stars](https://manufact.com/blog/10000-github-stars); [GitHub](https://github.com/mcp-use/mcp-use)
- In February 2026 Manufact hosted an **MCP Apps hackathon at YC HQ** (Feb 21, 2026), described as the "largest MCP apps hackathon". According to a third-party research note (unverified), it had no published rubric and judging centred on live demos. — [everydev.ai timeline](https://www.everydev.ai/developers/manufact); [third-party note on glama.ai](https://glama.ai/mcp/servers/@markster-exec/mcp-unicorn/blob/ddbb82559bb5f1a082923dc01665846ee976ecbc/research/hackathon/event-details.md)

### Inferences
- The judges built the framework, so they will recognise idiomatic mcp-use v2 code: Zod `inputSchema`/`outputSchema`, `structuredContent`, annotations, Views, Skills, and deploying to Manufact. Using their stack well, and deploying on Manufact cloud, is likely a strong signal. Enrico (GitHub `tonxxd`) appears to drive conformance work: the conformance badges are hosted on his gist.
- Khadder built the screenshot CLI and wrote about MCP testing. A submission that shows **testing and evals** of its tools, such as headless CLI calls or an eval transcript, may resonate with him.

### Gaps
- No exact rebrand date was found. The rebrand happened before or around the Feb 2026 seed, because the announcement already uses the Manufact name.
- The YC page, LinkedIn and X could not be fetched to confirm current titles. No public talks or posts by Khadder or Toniato on MCP judging criteria were found.
- No published judging rubric was found for this hackathon or for the February 2026 Manufact hackathon.
- The "Make Something Agents Want" October 17-18, 2026 event page was not found in search. One result used the phrase as commentary on YC W26 Demo Day ([pingwest](https://www.pingwest.com/a/312424)).

## 2. Products, pricing, and what the credits buy

### Takeaway
There are two layers. (1) **mcp-use**, an open-source MIT framework: server, client, agent, Inspector, tunnel and scaffolder in TS, plus a Python package. (2) **Manufact Cloud**: Git-based hosting for MCP servers with observability, analytics, evals, preview environments, logs and env vars, billed as plans plus usage on a dollar-denominated credit pool (1 credit = $0.01). Prize credits most likely pay for hosting and usage on Manufact Cloud.

### Cited Findings
- README positioning (primary, fetched): "The TypeScript framework for MCP: Build, test, and ship MCP servers, ChatGPT plugins, Claude connectors. Fully Typed, native Views and MCP Apps support, built-in Inspector and first class Agent experience." — [GitHub README](https://github.com/mcp-use/mcp-use)
- Package ecosystem (primary, fetched):
  - `mcp-use`: TS v2 server framework, React views and CLI.
  - `@mcp-use/client`: connects to MCP servers from Node, browsers, React and sandboxes.
  - `@mcp-use/agent`: model-powered agents built on MCP clients.
  - `@mcp-use/inspector`.
  - `@mcp-use/tunnel`: managed relay for local servers.
  - `create-mcp-use-app`: scaffolder.
  - `mcp-use` on PyPI: Python servers, clients and agents.

  — [GitHub README](https://github.com/mcp-use/mcp-use)
- Versions (primary, fetched): npm `mcp-use` **2.8.2**, "MCP framework and CLI built on the official v2 SDK", modified 2026-10-09. The first npm publish was 2025-04-20. PyPI `mcp-use` **1.7.1**, "Full Stack MCP framework for python, build MCP agents, clients, and servers", uploaded 2026-09-10. — [npm](https://www.npmjs.com/package/mcp-use); [PyPI](https://pypi.org/project/mcp-use/)
- Vendor comparison table in the README (vendor-authored, not independent): mcp-use v2 runs at 10,982 ops/s, versus FastMCP TS 6,628, Official SDK v2 8,050, xmcp 6,585, Skybridge 8,116 and mcp-handler 6,324. Its MCP App dev stack is 74.4 MiB with 51 packages. It claims "Native Views on MCP 2026", "One-line OAuth adapters", MCP 2026 protocol support, a View screenshot CLI, built-in tunneling and a built-in Inspector. — [GitHub README](https://github.com/mcp-use/mcp-use); [benchmark.md](https://github.com/mcp-use/mcp-use/blob/main/benchmark.md)
- Cloud features (primary, fetched): "Ship to Manufact and get observability, analytics, evals, submission readiness, and Git-based preview environments for free." — [GitHub README](https://github.com/mcp-use/mcp-use)
- How deployment works (primary, fetched docs):
  - It is **GitHub-backed only**. You install the Manufact GitHub App, then run `npx mcp-use login` and `npx mcp-use deploy --name my-server`.
  - Follow the build with `npx mcp-use deployments logs <ID> --build --follow`. `servers env set` manages environment variables.
  - Flags include `--region`, `--env`, `--env-file`, `--dockerfile`, `--root-dir` (for monorepos) and `--json`.
  - The CLI does not upload local source. The hosted MCP URL comes from the dashboard; demo URLs look like `*.run.mcp-use.com/mcp`.

  — [docs/v2/typescript/server/deployment/mcp-use.mdx](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/server/deployment/mcp-use.mdx)
- Pricing has two conflicting versions (snippets):
  - `manufact.com/pricing.md`: Free $0 with $5/month in credits and no overage; Hobby $30/month; Startup $300/month; overage at $0.01 per credit. All usage draws on a single dollar-denominated credit pool (1 credit = $0.01).
  - Live pricing page: Hobby $25/month and Startup $250/month, each "plus usage", sized by requests (Hobby about 300k requests/month, Startup about 3M).
  - Both: Enterprise is custom, with SSO and self-hosting. Projects: Free 1, Hobby 2, Startup 20. Analytics retention: 7 days on Free, up to 1 year on Startup. Startup adds region pinning.

  — [Manufact pricing.md](https://manufact.com/pricing.md); [Manufact pricing](https://manufact.com/pricing)
- Other features in the v2 docs navigation (primary, fetched docs.json):
  - Auth: OAuth providers (Auth0, Better Auth, Clerk, Convex, Keycloak, Supabase, WorkOS, Scalekit, custom DCR) and mixed auth.
  - Server: proxy, **OpenAPI-to-MCP**, Next.js drop-in, middleware, elicitation, subscriptions, notifications, **Skills over MCP**.
  - MCP Apps: quickstart, ChatGPT extensions, generative UI, interactivity, model context, CSP.
  - Client: sampling, elicitation, auth.
  - Inspector: debugging ChatGPT apps.

  — [docs/docs.json](https://github.com/mcp-use/mcp-use/blob/main/docs/docs.json)
- The hosted Inspector is at inspector.mcp-use.com. In dev mode the Inspector is served at `/mcp/inspector`. — [GitHub README](https://github.com/mcp-use/mcp-use)
- Manufact publishes a comparison page, "Why mcp-use & Manufact — comparison vs alternatives" (snippet, contents not retrieved). — [manufact.com/compare](https://manufact.com/compare)

### Inferences
- The 1st-prize "$6,000 Manufact credits" plausibly equals 600,000 credits at $0.01 each, or about 20 months of the Startup plan. This assumes the credit model in pricing.md, which may not be current.
- The ChatGPT/Claude "MCP Apps" product line, with UI Views, is a central Manufact focus. This track, however, is "built for agents as the primary customer", so headless tool quality matters more than UI. Views are optional polish and probably should not be the core of the entry.

### Gaps
- Pricing could not be verified live because the two versions conflict. I found no explicit terms for the prize credits (expiry, which plan).
- No gateway product appears by name in the docs. A "proxy" doc exists (`v2/typescript/server/proxy`), but I did not read its contents.
- I did not retrieve docs.manufact.com (dashboard docs: servers, deployments, build runtimes, env vars, logs, connect-clients) or details on its evals and analytics features.

## 3. Docs, quickstart, code, repos

### Takeaway
The fastest path is `npx -y create-mcp-use-app@latest`, then `npm run dev` (Inspector at `http://localhost:3000/mcp/inspector`), then `npm run deploy` (Manufact). The v2 API is `new MCPServer({...})` with `server.tool({name, description, inputSchema, outputSchema, annotations, view?}, handler)` returning raw `CallToolResult` with `structuredContent`. v2 requires Node >= 22.22.2 and ESM.

### Cited Findings
- Docs: TS v2 at https://docs.mcp-use.com/v2/typescript/getting-started/welcome. Python at https://mcp-use.com/docs/python. Agent-driven start: give your coding agent "Build an MCP server: https://mcp-use.com/prompt.md" (primary, fetched). — [GitHub README](https://github.com/mcp-use/mcp-use)
- Quickstart commands (primary, fetched):
  ```
  npx -y create-mcp-use-app@latest
  npm run dev            # http://localhost:3000/mcp  (+ /mcp/inspector)
  mcp-use dev --tunnel   # public URL to test in ChatGPT / Claude
  npx mcp-use client connect local http://localhost:3000/mcp
  npx mcp-use client local tools list
  npx mcp-use client local tools call get-weather city=Tokyo
  npx mcp-use screenshot --server local --tool get-weather city=Tokyo --output weather-card.png
  npm run build && npm run deploy
  ```
  — [GitHub README](https://github.com/mcp-use/mcp-use)
- Minimal v2 tool pattern (primary, fetched, from the README):
  ```ts
  import { MCPServer } from "mcp-use"; import { z } from "zod";
  const server = new MCPServer({ name: "weather-app", title: "Weather App", version: "1.0.0" });
  export const getWeather = server.tool({
    name: "get-weather", title: "Get weather", description: "Get the current weather for a city",
    inputSchema: z.object({ city: z.string().describe("City to look up") }),
    outputSchema: z.object({ city: z.string(), temperature: z.number(), conditions: z.string() }),
    view: { name: "weather-card" },  // optional React View at views/weather-card/view.tsx
    annotations: { readOnlyHint: true, destructiveHint: false, openWorldHint: true },
  }, async ({ city }) => ({ content: [{ type: "text", text: `...` }], structuredContent: { city, temperature: 22, conditions: "Sunny" } }));
  export default server;
  ```
  — [GitHub README](https://github.com/mcp-use/mcp-use)
- v2 rules (primary, fetched migration doc):
  - Node >= 22.22.2 and ESM; default-export the server; export every static tool as a `ToolRef`.
  - A tool with `outputSchema` must return matching `structuredContent`. Errors return `isError: true`. Include a text fallback in `content`.
  - The legacy helpers `text()`/`object()`/`error()` are deprecated shims.
  - Sessions are gone: "Session stores, active-session registries, stream managers, session recovery, and session affinity are not part of v2… Do not key business state to an MCP transport session."
  - Edge/Fetch runtimes use `server.fetch`. Node uses `toNodeHandler()`.

  — [docs/v2/typescript/server/migration.mdx](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/server/migration.mdx)
- OAuth (primary, fetched): pass a provider, for example `oauth: oauthAuth0Provider({ domain })` imported from `mcp-use/oauth/auth0`. The server publishes protected-resource metadata and verifies bearer tokens. Tools then read `ctx.auth.user`, `ctx.auth.scopes` and `ctx.auth.permissions`. Providers must support DCR. — [docs/v2/typescript/server/authentication/index.mdx](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/server/authentication/index.mdx)
- **Skills over MCP** (primary, fetched):
  - Place a `skills/<name>/SKILL.md` directory next to the server and it is auto-published under the `io.modelcontextprotocol/skills` extension (`skills/list`, `skills/get`, `resources/read`, `resources/directory/read`).
  - It follows the **draft SEP-2640**; "wire contract may change".

  — [docs/v2/typescript/server/skills.mdx](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/server/skills.mdx)
- MCP Apps (primary, fetched): a View-bound tool must declare `outputSchema`. Views live in `views/<name>/view.tsx` and use the `mcp-use/react` hooks `useToolContext` and `useCallTool`. Vite builds them. — [docs/v2/typescript/mcp-apps.mdx](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/mcp-apps.mdx)
- Example apps you can remix and deploy: [mcp-chart-builder](https://github.com/mcp-use/mcp-chart-builder), [mcp-diagram-builder](https://github.com/mcp-use/mcp-diagram-builder), [mcp-maps-explorer](https://github.com/mcp-use/mcp-maps-explorer). More examples live in `libraries/typescript/packages/server/examples`. Discord: https://discord.gg/XkNkSkMz3V. — [GitHub README](https://github.com/mcp-use/mcp-use)
- Conformance CI runs for the Python and TS server and client. — [GitHub README](https://github.com/mcp-use/mcp-use)

### Inferences
- Hackathon tip: use `npx mcp-use client ... tools call` in a scripted eval loop to show agents using the tools correctly. Ship a `skills/` folder as the server's "operating manual" for agents. Deploy early with `npm run deploy`, which needs the repo pushed to GitHub first.

### Gaps
- I could not confirm whether Python mcp-use v1.7.1 matches TS v2 features such as Views and stateless operation. The Python docs list sessions, sampling, roots and auth/bearer.
- Stars for the other mcp-use org repos were not retrievable because the org-level API was blocked.

## 4. State of the MCP spec (Oct 2026) and what makes a server excellent for agents

### Takeaway
The current spec is **2026-07-28**. It makes the core **stateless**: no `initialize` handshake and no `Mcp-Session-Id`. Version and capabilities travel in `_meta`, with `server/discover` for discovery. Streamable HTTP gains `Mcp-Method`/`Mcp-Name` headers, multi-round-trip requests replace held streams, and list results carry ttl caching. MCP Apps and Tasks become formal extensions. Sampling, roots and logging are deprecated. Tool schemas use full JSON Schema 2020-12. Anthropic's tool-design guidance is the de facto rubric for "agent-first" servers: few consolidated workflow tools, search over list, concise/detailed response modes, pagination and truncation, actionable errors, and namespacing.

### Cited Findings
- The 2026-07-28 RC post was published May 21, 2026, with the final spec scheduled for July 28, 2026 (primary, fetched). Other sources (Aug 2026) describe it as final. — [MCP blog: RC](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/); [technspire: "spec is final"](https://technspire.com/en/blog/mcp-goes-stateless-migrating-your-enterprise-mcp-servers-to); [Equixly, 2026-08-05](https://equixly.com/blog/2026/08/05/stateless-mcp/)
- Stateless core (primary, fetched):
  - `initialize`/`initialized` is removed (SEP-2575).
  - `Mcp-Session-Id` and protocol sessions are removed (SEP-2567).
  - Streamable HTTP requires `Mcp-Method` and `Mcp-Name` headers (SEP-2243).
  - `ttlMs` and `cacheScope` enable caching (SEP-2549).
  - W3C trace context goes in `_meta` (SEP-414).
  - State lives in handles that tools return (for example `basket_id`) and the model passes back.

  — [MCP blog: RC](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/)
- MRTR (SEP-2322): the server returns an input-required result and the client re-issues the call with answers. Server-to-client requests are allowed only while handling a client request (SEP-2260). — [MCP blog: RC](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/)
- Extensions framework (SEP-2133) uses reverse-DNS IDs. **MCP Apps (SEP-1865)** provides interactive HTML UIs in sandboxed iframes, with templates declared up front. **Tasks** moves to an extension (`tasks/get`, `tasks/update`, `tasks/cancel`; `tasks/list` removed). — [MCP blog: RC](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/)
- Deprecations (SEP-2577): Roots (use tool params or URIs instead), **Sampling** (use direct LLM provider integration), Logging (use stderr or OpenTelemetry). Removal requires at least 12 months. — [MCP blog: RC](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/)
- Schemas: full JSON Schema 2020-12 for `inputSchema`/`outputSchema` (SEP-2106). `structuredContent` may be any JSON value. The missing-resource error code is now `-32602` (SEP-2164). — [MCP blog: RC](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/)
- Auth: clients must validate `iss` (SEP-2468 / RFC 9207). DCR gains `application_type` (SEP-837), plus clarifications on refresh tokens and step-up scopes. Secondary sources say **DCR is deprecated in favour of Client ID Metadata Documents (CIMD)**, but the RC post I fetched does not say this, so treat it as unconfirmed. — [MCP blog: RC](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/); [search summary of AAIF / Stacktree](https://aaif.io/blog/mcp-2026-07-28-whats-changing-and-how-to-migrate)
- Skills over MCP is a draft extension (SEP-2640) with a working group. mcp-use already implements it. — [mcp-use skills doc](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/server/skills.mdx)
- Anthropic, "Writing effective tools for agents" (Sep 11, 2025), primary, fetched:
  - Consolidate multi-step workflows, for example `schedule_event` instead of list-users + list-events + create.
  - Prefer `search_contacts` over `list_contacts`. Build fewer, purposeful tools.
  - Namespace tools, for example `asana_search` and `jira_search`.
  - Return names rather than UUIDs, but keep IDs when needed for chained calls.
  - Offer a `response_format` enum with `DETAILED` and `CONCISE` values. In the article's example, concise used about one-third of the tokens.
  - Use pagination, filtering and truncation with sane defaults; Claude Code caps tool responses at 25k tokens.
  - When truncating, tell the agent how to narrow the query.
  - Write actionable errors that show a correct input example.
  - Write descriptions like onboarding a new hire, with unambiguous param names (`user_id`).
  - Use annotations for destructive and open-world tools.
  - Evaluate with realistic multi-call tasks and read the transcripts.

  — [Anthropic Engineering](https://www.anthropic.com/engineering/writing-tools-for-agents)
- Docker's MCP best practices: design around use cases rather than one tool per API endpoint (snippet). — [Docker blog](https://www.docker.com/blog/mcp-server-best-practices/)

### Inferences
Checklist for an "agents as primary customer" server that this jury (spec-aware framework authors) would likely reward:
- **Stateless, 2026-07-28-native** design, with explicit handles instead of sessions. This matches mcp-use v2.
- About **3-8 high-level, intent-shaped tools**: search, act and verify.
- `outputSchema` + `structuredContent` on every tool.
- `readOnlyHint`/`destructiveHint` annotations.
- `response_format` concise/detailed.
- Cursor pagination with truncation hints.
- Errors that teach the fix.
- A bundled `skills/SKILL.md` playbook.
- OAuth via a one-line provider if user data is involved.
- Tasks or MRTR for long or confirm-required operations.
- Deployment on Manufact with a public URL.
- A **measured eval**: tool-call count, tokens and success rate versus a naive API wrapper.

### Gaps
- I did not verify the CIMD/DCR change or the status of the official MCP Registry in October 2026.
- I could not confirm whether elicitation "URL mode" (from the 2025-11-25 spec) changed in 2026-07-28.

## 5. Judges' public views and project ideas

### Takeaway
I found no public post or talk by Pederzani, Toniato or Khadder that states what they value in an MCP server. The company's own product choices reveal their priorities:
- "agent-first and headless" workflows ("Scaffold, invoke, inspect, screenshot, and deploy through your agent")
- testing and evals
- typed structured output
- statelessness and performance
- Skills
- production deployment

### Cited Findings
- README value props: "Agent-first and headless… through your agent"; "Fully typed… Zod schemas flow from tools to structured results"; built-in Inspector; screenshot verification (primary, fetched). — [GitHub README](https://github.com/mcp-use/mcp-use)
- Manufact blog post titles include "mcp-use v2: The age of stateless MCP" and "We Made MCP Testing Less Painful" (Pietro Zullo). The teaser for the testing post cites slow install loops, behaviour that differs across clients, and no good way to confirm agents call tools correctly. Other posts cover a deploy-to-production guide (Toniato) and building the screenshot CLI (Khadder) (snippets). — [Manufact blog: mcp-use v2](https://manufact.com/blog/mcp-use-v2); [Manufact blog index](https://manufact.com/blog?view=cloud)
- Toniato spoke at an AI Tinkerers Zurich event, introducing himself as CTO (snippet; talk content unknown). — [AI Tinkerers Zurich](https://zurich.aitinkerers.org/talks/rsvp_yY7TrFFu3wo)

### Inferences (project ideas, not sourced)
- **Agent-native "API gateway" for a messy domain**, such as government data, SEC filings, or shipping/customs. It would offer 4-6 consolidated tools with concise/detailed modes, cursor pagination and a `skills/` playbook, plus a benchmark showing fewer tokens and tool calls than a raw OpenAPI-to-MCP wrapper. mcp-use ships OpenAPI-to-MCP, so the baseline comparison is easy to build.
- **Agent sandbox/verification server**: tools that let agents test their own work, for example run a web app and return a structured accessibility/DOM diff with screenshots. This draws on mcp-use's screenshot CLI theme.
- **Agent-to-agent commerce or procurement server**: quote, compare and purchase, with explicit handles (`cart_id`), Tasks for long jobs, MRTR/elicitation for human confirmation, OAuth scopes and destructive annotations.
- **Memory/knowledge server for coding agents**: search over an org's docs and decisions, returning cited snippets with token budgets.
- **MCP-server evaluator served as MCP**: a server agents call to lint and evaluate other MCP servers (description quality, schema strictness, token cost per call). It is meta, but squarely in the judges' domain (testing, conformance).
- Whatever you build, demo it with a real agent (Claude Code, ChatGPT, or `@mcp-use/agent`) completing a multi-step task live, then show the Manufact-hosted URL and an eval table.

### Gaps
- No judging rubric or weights were found for this track.
- No talks or posts from Khadder or Toniato on MCP design preferences were found.
