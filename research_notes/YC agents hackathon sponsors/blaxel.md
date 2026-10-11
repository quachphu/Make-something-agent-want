# Blaxel: technical and business profile for the YC "Make Something Agents Want" hackathon (Oct 17-18, 2026)

> Research date: 2026-10-11. **Method note:** this sandbox's egress proxy blocked direct fetches of blaxel.ai, docs.blaxel.ai, baseten.co and events.ycombinator.com. The docs content below comes from Blaxel's public docs source repo ([github.com/blaxel-ai/docs](https://github.com/blaxel-ai/docs), cloned at a commit dated 2026-10-09), which is what docs.blaxel.ai publishes. Citations point to the matching docs.blaxel.ai page URL. Package versions come straight from the npm and PyPI registries. Business facts come from web-search snippets of the cited articles, and I could not open those articles in full.

## 1. What is Blaxel? Product, customers, YC batch, founders, funding, and the Baseten acquisition

### Takeaway
Blaxel calls itself "infrastructure for autonomous agents," a cloud "where AI agents themselves are the primary users." Its main product is "perpetual" microVM sandboxes that sit on standby and resume in about 25ms. Around them it offers Agents Hosting, MCP Servers Hosting, Batch Jobs, a Model Gateway, storage (Volumes and Agent Drive) and observability. It is a YC Spring 2025 (X25) company and raised a $7.3M seed led by First Round. **Big recent news: Baseten acquired Blaxel on Sept 10, 2026.** Blaxel says the product keeps running as before.

### Cited Findings
**Positioning**
- Tagline: "Blaxel is the **infrastructure for autonomous agents**. Our platform lets you keep infinite, secure sandboxes on automatic standby while co-hosting your agents for near instant latency." — [Blaxel docs: Overview](https://docs.blaxel.ai/Overview)
- "Blaxel is a cloud where **AI agents themselves are the primary users**. All products are accessible through MCP servers, allowing agents to create and manage resources via tool calls… Sandboxes give them their own dedicated personal computer(s)… Batch Jobs enable them to schedule background tasks at scale." — [Blaxel docs: Overview](https://docs.blaxel.ai/Overview). This fits the hackathon theme very closely.
- Homepage title: "Blaxel: Infrastructure for autonomous agents." — [blaxel.ai (search result title)](https://blaxel.ai/). Sandbox page title: "Sandboxes that persist forever, with 25ms resumes." — [blaxel.ai/sandbox](https://blaxel.ai/sandbox)
- The YC event page describes Blaxel as "the perpetual sandbox platform for AI agents that need to run code fast," with sandboxes that "automatically scale to zero after 1s of inactivity and resume in under 25ms with full memory state preserved." — [YC event page (via search snippet)](https://events.ycombinator.com/MakeSomethingAgentsWant)

**Product components** (all from [Blaxel docs: Overview](https://docs.blaxel.ai/Overview))
- **Sandboxes** (flagship): microVMs with full filesystem, process and log access. They resume from standby in under 25ms, support Zero Data Retention (ZDR), and offer preview URLs on custom domains.
- **Agents Hosting**: serverless, auto-scaling HTTP endpoints. "Completely framework agnostic: just bring your code, Blaxel builds it and runs it for you." Sync mode allows up to 100s, async mode up to 10 min.
- **Batch Jobs**: parallel background tasks, up to 24h each, with about 30s boot.
- **MCP Servers Hosting** (historically called "Functions" in the docs and API): about 25ms boot, up to 10 min per request.
- **Model Gateway**: "Intelligent routing layer to LLM providers with built-in telemetry, token cost control, and fallback capabilities."
- **Volumes** (durable block storage, one sandbox at a time) and **Agent Drive** (a shared distributed POSIX filesystem with an S3-compatible endpoint, mountable by many sandboxes and agents at once).
- **Observability** (logs, traces, metrics) and Governance (policies, environments).
- **Applications** (private preview): long-running public services, deployable from source, an image, or a *forked sandbox*. The stated design idea: "agents… will build ad hoc user-facing software to expose as micro-apps to end-users — whether humans-in-the-loop, or other agents." — [Blaxel docs: Applications](https://docs.blaxel.ai/Applications/Overview)

**Company**
- YC batch X25 (Spring 2025); $7.3M seed led by First Round Capital — [YC jobs page via search](https://www.ycombinator.com/companies/blaxel/jobs); the round also included Y Combinator, Liquid2 and Transpose — [Blaxel blog: seed announcement](https://blaxel.ai/blog/blaxel-raises-7-3m-seed-round-led-by-first-round-to-build-cloud-infrastructure-for-the-ai-agent-eco-23247e47b1ea8067b923d998364e3ced). One aggregator lists the batch as "P25". The source conflicts on this and is low quality — [altss.com](https://altss.com/companies/yc/blaxel)
- Seed timing: July 2025, about one month after graduating YC. Other sources give total funding as $7.0M or $7.8M — [StartupHub.ai](https://www.startuphub.ai/ai-news/funding-round/2025/blaxel-raises-7-3m-seed-for-ai-agent-cloud-infrastructure); [Crunchbase](https://www.crunchbase.com/organization/https-blaxel-ai)
- Founders (six): Paul Sinaï (CEO), Thomas Crochet, Charles Drappier, Mathis Joffre, Nicolas Lecomte and Christophe Ploujoux. They previously worked together at ForePaaS, which OVHcloud acquired in 2022 — [rywalker.com research](https://rywalker.com/research/blaxel); [Pulse2 interview with Charles Drappier](https://pulse2.com/blaxel-profile-charles-drappier-interview/). Sources differ slightly on the founder list.
- The company was formerly **Beamlit**. Its GitHub org still has repos such as `bl-controller` ("A Kubernetes controller for managing Beamlit resources"), `homebrew-beamlit` and `bl-action` ("Github action for beamlit") — [github.com/blaxel-ai](https://github.com/blaxel-ai)
- Customers: Webflow is the anchor customer, using Blaxel sandboxes for real-time previews in its AI coding agent. Other names cited include Shortwave, Strapi, Sapiom, Vybe, Casco, Polsia, Delty, Build0 and Mendral, though lists vary by source — [rywalker.com](https://rywalker.com/research/blaxel); [Blaxel 2025 year-end round-up](https://blaxel.ai/blog/2025-blaxel-our-year-end-round-up)
- At the time of the seed, one report cited "7.5M+ agent requests per day across 16 regions" — [Menlo Times](https://www.menlotimes.com/post/blaxel-ai-secures-7-3-million-to-build-cloud-infrastructure-for-ai-agent-economy). This is unverified and conflicts with the 4 self-service regions listed today.

**Baseten acquisition (Sept 10, 2026)**
- "Blaxel is joining Baseten to build the future of agentic infrastructure." Terms were undisclosed — [Baseten blog](https://www.baseten.co/blog/blaxel-is-joining-baseten-to-build-the-future-of-agentic-cloud/); [Axios Pro, 2026-09-10](https://www.axios.com/pro/enterprise-software-deals/2026/09/10/baseten-agentic-infrastructure-blaxel); [The Next Web](https://thenextweb.com/news/baseten-acquires-blaxel-ai-agent-sandboxes)
- Baseten CEO Tuhin Srivastava: "As AI moves from single models to millions of agents, we need a new infrastructure stack… a platform where execution, inference, and training run on one system." — [X post](https://x.com/tuhinone/status/2098091259386823048)
- Blaxel told customers it "continues as a product and platform. Your sandboxes, storage, networking, API keys, credits, and support contacts stay the same." — [Blaxel about page (via search)](https://blaxel.ai/company/about)
- This is Baseten's second acquisition since it raised $1.5B at a $13B valuation in June 2026. Coverage repeats the claim that Blaxel sandboxes start and resume "up to 5x faster" than competitors — [VKTR](https://www.vktr.com/ai-market/blaxel-is-joining-baseten-to-build-the-future-of-agentic-infrastructure/); [Dealroom](https://app.dealroom.co/news/feed/baseten-acquires-blaxel-to-power-ai-agents-with-5x-faster-sandbox-infrastructure)
- The docs now include "Baseten managed workspaces": a "Continue with Baseten" login that maps each Baseten org to one Blaxel workspace — [Blaxel docs: Baseten managed workspaces](https://docs.blaxel.ai/Security/Baseten-managed-workspaces)
- Baseten blog post on NVIDIA OpenShell running on Blaxel sandboxes ("Carbon") — [Baseten blog](https://www.baseten.co/blog/announcing-carbon/); the PoC repo is `openshell-blaxel` ("Run NVIDIA OpenShell sandboxes as Blaxel microVMs") — [GitHub](https://github.com/blaxel-ai/openshell-blaxel)
- A critical take: Blaxel's "keeps running" pledge has no end date, and its standard terms allow assignment, repricing and deletion of data 90 days after termination — [beri.net](https://www.beri.net/article/baseten-blaxel-acquisition-agent-sandbox-continuity-migration-notice-portability)

### Inferences
- The judges are likely Blaxel engineers or founders, now part of Baseten. They will reward projects that use **sandboxes as an agent's own computer** and that use the stack natively (sandbox MCP, Agent Drive, forking, Jobs). Agent-to-agent use, rather than human UIs, fits their stated philosophy.
- Because of the Baseten deal, pairing Blaxel compute with Baseten-hosted open models for inference may also appeal to the judges. This is speculative.

### Gaps
- I could not open the YC company page (ycombinator.com/companies/blaxel) to confirm the founder list and batch label.
- Current headcount, revenue, and the acquisition price were not found.

## 2. Core technology and architecture, regions, pricing and free tier

### Takeaway
Sandboxes are microVMs (infrastructure generation "Mark 3.0"; "Carbon"/Mark 3.1 is in private preview). The filesystem is an EROFS read-only image plus an in-RAM tmpfs layer. On idle, the full memory, process and filesystem state is snapshotted, and the sandbox resumes in under 25ms. You pay for memory only while active; standby costs only snapshot storage. Four self-service regions are listed (Oregon, N. Virginia, London, Frankfurt). Pricing is usage-based, about $0.04/GB-hour of memory per third-party sources, and the free plan reportedly includes up to $200 in credits.

### Cited Findings
**Sandbox lifecycle** ([Blaxel docs: Sandboxes](https://docs.blaxel.ai/Sandboxes/Overview))
- "Sandboxes resume from standby in under 25 milliseconds and automatically scale to zero after a few seconds of inactivity… Memory state is maintained even after scaling down, including the running processes and entire filesystem."
- **Active mode**: billed for allocated memory plus storage. CPU is not billed separately and scales with memory: "8 GB memory is allocated 4 CPU cores… 16 GB… 6 CPU cores."
- **Standby**: entered when there is no active connection, "in approximately 15 seconds." An idle WebSocket/TCP connection times out after 15 minutes. A snapshot is taken automatically. "You are not charged for memory while a sandbox is in standby mode", only for snapshot or volume storage. External network connections (DB connections, HTTP pools) do not survive standby.
- **Conflicting idle timeouts**: the YC page says 1s, the Overview and Get-started docs say "Automatic scale-to-zero after 5s inactivity, resume from standby under 25ms even after weeks" ([Overview](https://docs.blaxel.ai/Overview)), and the Sandboxes doc says about 15s. Treat the timeout as "seconds" and the resume time (25ms) as the consistent claim.
- **Archived mode**: stores the filesystem diff and shuts the sandbox down without keeping memory. Unarchiving restarts processes with new PIDs.
- **Deletion and TTLs**: expiration policies are supported. "Starter quotas enforce time-to-live limits (TTLs), while higher quota tiers unlock sandboxes with unlimited persistence."
- Re-creating a deleted sandbox from Volumes or Agent Drive takes "~2–4 seconds" — [Overview](https://docs.blaxel.ai/Overview)
- **Filesystem internals**: an EROFS read-only base image, a writable tmpfs layer in RAM, and OverlayFS on top. About 50% of memory is reserved for tmpfs — [Sandboxes](https://docs.blaxel.ai/Sandboxes/Overview)
- Reserved ports are 80, 443 and 8080. Other ports can be exposed at creation or opened dynamically through preview URLs — [Sandboxes](https://docs.blaxel.ai/Sandboxes/Overview)
- **Every sandbox exposes a built-in MCP server** at `https://<SANDBOX_BASE_URL>/mcp` (streamable HTTP, Bearer API key) with tools for files, processes, ports and previews — [Sandbox MCP server](https://docs.blaxel.ai/Sandboxes/MCP)
- **Codegen tools**: "fast apply" of LLM-suggested edits at 2000+ tokens/s, powered by Morph or Relace (bring your own key) — [Codegen tools](https://docs.blaxel.ai/Sandboxes/Codegen-tools)
- **Snapshots and forking** (private preview, launched 2026-07-24): capture filesystem, processes and memory; roll back; fork into new sandboxes or into a live Application — [Snapshots & forking](https://docs.blaxel.ai/Sandboxes/Fork); [Changelog](https://docs.blaxel.ai/changelog)
- **Proxy routing with secrets injection** (public preview): outbound HTTPS from the sandbox is intercepted and secrets or headers are injected server-side, "so code never sees raw API keys". Dynamic value injection (UUIDs, nonces, idempotency keys) was added 2026-08-13. Domain, method and path egress filtering was added 2026-08-14, with network-level enforcement on 2026-09-25 — [Proxy secrets injection](https://docs.blaxel.ai/Sandboxes/Proxy-secrets-injection); [Changelog](https://docs.blaxel.ai/changelog)
- Other sandbox features: schedules (cron, future date, or delay), external IDs for indexed lookup by user or session, sessions, log streaming, and non-root users. Snapshots became workspace-level resources on 2026-09-04 — [Changelog](https://docs.blaxel.ai/changelog)

**Infrastructure generations** ([Infrastructure generations](https://docs.blaxel.ai/Infrastructure/Gens))
- Mark 1 used Knative on Kubernetes and was decommissioned Jan 2025. Mark 2 used containers with 2-10s cold starts, was deprecated Q4 2025 and decommissioned Q2 2026. **Mark 3.0 (the default) uses microVMs** for sandboxes, agents, MCP servers and jobs. **Carbon (Mark 3.1)** is in private preview since 2026-07-13 and adds manual snapshot and fork. It does not yet support Agent Drive, firewalling or dedicated egress IPs.
- The "Global Agentics Network" is a distributed backbone that decouples the execution layer from a federated data layer for multi-region deployments — [Overview](https://docs.blaxel.ai/Overview)

**Regions** ([Regions](https://docs.blaxel.ai/Infrastructure/Regions))
- `us-pdx-1` (Oregon), `us-was-1` (N. Virginia), `eu-lon-1` (London), `eu-fra-1` (Frankfurt), plus `auto`. Not all regions are self-service. Agents, MCP servers and jobs are deployed globally; sandboxes are regional. `BL_REGION` sets the default, and `region` "will become mandatory in future versions of the SDK."

**Pricing and free tier**
- Billing is per second for allocated memory while active, with no separate CPU charge — [Sandboxes docs](https://docs.blaxel.ai/Sandboxes/Overview); "per-second with no base subscription" — [Upstash comparison 2026](https://upstash.com/blog/ai-agent-sandbox-providers-compared-2026)
- About $0.0000115 per GB-second, or roughly $0.0414/GB-hour. A 2GB sandbox runs about $0.08/hr and an 8GB one about $0.33/hr — [AgentDeals](https://agentdeals.dev/best/free-agent-sandbox); [Upstash comparison](https://upstash.com/blog/ai-agent-sandbox-providers-compared-2026). These are third-party figures; the official pricing page is [blaxel.ai/pricing](https://blaxel.ai/pricing), which I could not fetch.
- "Free plan including $200 in credits at signup, no credit card required". Credits reportedly expire one year after issue — [AgentDeals](https://agentdeals.dev/best/free-agent-sandbox) (third-party).
- Quota tiers depend on 30-day **top-up volume**. Promotional credits do not unlock tiers. Higher tiers raise limits on standby and concurrent sandboxes, jobs, volume sizes and TTLs, and unlock custom domains and dedicated IPs. "Accounts on the free plan are not eligible for quota upgrades." — [Usage and quotas](https://docs.blaxel.ai/Security/Quotas)

### Inferences
- For a 24-hour hackathon, the free plan and its $200 in credits should easily cover development, since standby is close to free. The real constraint is free-tier quotas (concurrent sandboxes, TTLs). Teams should ask Blaxel staff on-site for hackathon credits or a quota bump.
- Fork and snapshot and Applications are in private preview and may need to be enabled for your workspace. Ask the Blaxel team early if you plan to rely on them.

### Gaps
- I could not read the official pricing page or exact free-tier quotas (max concurrent sandboxes, max memory, default TTL).
- No independent benchmark of the 25ms resume claim was found.

## 3. Documentation, SDKs, CLI, MCP, GitHub, and the real API surface

### Takeaway
The docs are at docs.blaxel.ai (source: github.com/blaxel-ai/docs). They include an `llms-full.txt`, a docs MCP server and an AI assistant. The SDKs are TypeScript (`@blaxel/core`, currently 0.3.25), Python (`blaxel`, currently 0.4.13) and Go. The CLI is `bl`. Blaxel also ships agent skills and a Claude Code / Codex / Cursor plugin, so a coding agent can provision Blaxel resources itself. Auth uses the `BL_WORKSPACE` and `BL_API_KEY` env vars, or `bl login`.

### Cited Findings
**Packages and repos**
- npm `@blaxel/core` 0.3.25, last modified 2026-10-11. Framework adapters `@blaxel/langgraph`, `@blaxel/vercel`, `@blaxel/mastra`, `@blaxel/llamaindex` and `@blaxel/telemetry` are all at 0.3.25. `@blaxel/sdk` (0.1.16) is the older package — [npm registry](https://registry.npmjs.org/@blaxel/core)
- PyPI `blaxel` 0.4.13, "Blaxel - AI development platform SDK" — [PyPI](https://pypi.org/project/blaxel/)
- Key GitHub repos — [github.com/blaxel-ai](https://github.com/blaxel-ai):
  - `sandbox`: the in-VM sandbox API, written in Go (28 stars)
  - `sdk-python`, `sdk-typescript`, `sdk-go`
  - `toolkit`: the `bl` CLI, written in Go
  - `mcp-hub` and `blaxel-mcp-server`
  - `agent-skills` and `agent-migration-skills` (migrate from E2B, Daytona, Modal)
  - `cma-blaxel-sandbox`: "Self-host Claude Managed Agents tool execution on Blaxel sandboxes"
  - `blaxel-openai-agents-api-cookbook`, `openclaw-blaxel`, `deepseek-harness-blaxel-sandbox`, `herdr-blaxel-sandbox-plugin`, `openshell-blaxel`
  - `blaxel-sandbox-code-generation-cookbook`, `blaxel-agent-drive-lifecycle-cookbook`, `demo-sandbox`

**Install, CLI and auth** ([Get started](https://docs.blaxel.ai/Get-started))
```bash
curl -fsSL https://blaxel.ai/install.sh | sh     # or: brew install blaxel-ai/blaxel/blaxel
bl login                                          # or export BL_WORKSPACE / BL_API_KEY
bl new agent | bl new mcp | bl new job | bl new sandbox <name>   # scaffold
bl serve --hotreload                              # run locally (agent at http://localhost:1338)
bl deploy                                         # build + deploy (uses blaxel.toml)
bl get sandboxes -o json                          # list resources
bl setup / bl skills install                      # install skills + MCP servers into coding agents
```
- The SDK "does not accept credentials as constructor arguments". Credentials come from env vars, a `.env` file or a CLI login session. On Blaxel itself, auth is automatic — [Sandboxes](https://docs.blaxel.ai/Sandboxes/Overview)
- Locally, agents take `POST {"inputs": "..."}` on port 1338, and jobs take `POST {"tasks":[{...}]}` — [Get started](https://docs.blaxel.ai/Get-started)

**Create a sandbox** ([Sandboxes](https://docs.blaxel.ai/Sandboxes/Overview))
```typescript
import { SandboxInstance } from "@blaxel/core";
const sandbox = await SandboxInstance.createIfNotExists({
  name: "my-sandbox",
  image: "blaxel/base-image:latest",   // also blaxel/nextjs:latest, blaxel/py-app:latest, custom
  memory: 4096,                        // MB
  ports: [{ target: 3000, protocol: "HTTP" }],
  labels: { env: "dev" },
  externalId: "session-abc-123",       // optional indexed lookup key
  region: "us-pdx-1",
});
// later: await SandboxInstance.get("my-sandbox") / SandboxInstance.getByExternalId("session-abc-123")
```
```python
from blaxel.core import SandboxInstance
sandbox = await SandboxInstance.create_if_not_exists({
  "name": "my-sandbox", "image": "blaxel/base-image:latest",
  "memory": 4096, "ports": [{"target": 3000}], "region": "us-pdx-1"})
```

**Run processes** ([Process execution](https://docs.blaxel.ai/Sandboxes/Processes))
```typescript
const result = await sandbox.process.exec({ command: "ls /", workingDir: "/app", waitForCompletion: true });
console.log(result.exitCode, result.stdout, result.stderr);
// long-running server that keeps the VM awake: exec({ command, keepAlive: true, timeout })
```
- `exec` returns right away unless `waitForCompletion` is set. A non-zero exit sets `status: failed` and does not throw. `keepAlive: true` blocks auto-standby while the process runs.

**Filesystem, previews, drives, snapshots**
```typescript
await sandbox.fs.write("/blaxel/app/config.json", "{}");          // Filesystem docs
const content = await sandbox.fs.read("/blaxel/app/config.json");
const { subdirectories, files } = await sandbox.fs.ls("/blaxel/app");

const preview = await sandbox.previews.createIfNotExists({        // public URL for port 3000
  metadata: { name: "app" }, spec: { port: 3000, public: true } });
const url = preview.spec?.url;

const drive = await DriveInstance.createIfNotExists({ name: "my-app-data", region: "us-was-1" });
await sandbox.drives.mount({ driveName: drive.name, mountPath: "/mnt/data" });  // shared FS

const snap = await sandbox.snapshots.create("before-risky-change"); // private preview
```
Sources: [Filesystem](https://docs.blaxel.ai/Sandboxes/Filesystem), [Preview URLs](https://docs.blaxel.ai/Sandboxes/Preview-url), [Agent Drive](https://docs.blaxel.ai/Agent-drive/Overview), [Snapshots & forking](https://docs.blaxel.ai/Sandboxes/Fork). The snapshot REST call is `POST https://api.blaxel.ai/v0/sandboxes/{name}/snapshots` with headers `Authorization: Bearer` and `X-Blaxel-Workspace`.

**Agents Hosting** ([Develop agents in TypeScript](https://docs.blaxel.ai/Agents/Develop-an-agent-ts))
- The only requirement is an HTTP server bound to the `HOST` and `PORT` env vars. Max runtime is 15 min. The sync endpoint closes after 100s with no data flowing; streaming resets that timer. (The Overview table says async allows a 10 min maximum, a minor inconsistency.)
```typescript
import { blModel, blTools } from '@blaxel/vercel';   // or @blaxel/langgraph | llamaindex | mastra
import { streamText } from 'ai';
export default async function agent(input: string, stream) {
  const response = streamText({
    model: await blModel("gpt-4o-mini"),                // model via Blaxel gateway
    tools: { ...await blTools(['blaxel-search']) },     // MCP server hosted on Blaxel
    messages: [{ role: 'user', content: input }], maxSteps: 5,
  });
  for await (const d of response.textStream) stream.write(d);
  stream.end();
}
```

**MCP Servers Hosting** ([Create MCP server](https://docs.blaxel.ai/Functions/Create-MCP-server))
- Run `bl new mcp`. The template is a standard `@modelcontextprotocol/sdk` `McpServer` on an Express `/mcp` endpoint using streamable HTTP, listening on `PORT`/`HOST`, with `import "@blaxel/telemetry"`. Test with `pnpm inspect` (MCP Inspector) and deploy with `bl deploy`. OAuth flow and "Code mode" docs also exist — [Functions docs folder](https://github.com/blaxel-ai/docs/tree/main/Functions)

**Batch Jobs** ([Manage job execution (TS)](https://docs.blaxel.ai/Jobs/Manage-job-execution-ts))
```typescript
import { blJob } from "@blaxel/core";
const job = blJob("my-job");
const executionId = await job.createExecution({ tasks: [{ duration: 30 }, { duration: 60 }] });
const result = await job.waitForExecution(executionId);
```
- The concepts are Job (definition), Execution (one run), and Task (a parallel unit within an execution) — [Jobs](https://docs.blaxel.ai/Jobs/Overview)

**Model APIs** ([Model APIs](https://docs.blaxel.ai/Models/Overview))
- A gateway to external providers with centralized credentials and tracing. Bringing your own custom model is an Enterprise feature. Integration pages exist for Anthropic, OpenAI, Azure AI Foundry, Cohere, DeepSeek, HuggingFace, Mistral and xAI — [Integrations folder](https://github.com/blaxel-ai/docs/tree/main/Integrations)

**Agent-facing tooling** ([Blaxel Skills & MCP](https://docs.blaxel.ai/skills-mcp))
- `claude plugin marketplace add blaxel-ai/agent-skills && claude plugin install blaxel` installs the `blaxel-cli` and `blaxel-sdk` skills plus the resource-management MCP server (OAuth). Codex and Cursor equivalents exist. There is also a docs MCP server and `llms-full.txt`.
- Agent-led onboarding (setting up projects through your coding agent) was added 2026-07-19 — [Changelog](https://docs.blaxel.ai/changelog)

### Inferences
- The fastest hackathon path: install the CLI with `bl setup`, which also installs skills into Claude Code/Codex, then let the coding agent scaffold and deploy. Use `@blaxel/core` directly for sandbox work.
- Before demo day, check SDK method names against the live docs. The SDK is pre-1.0 (0.3.x / 0.4.x) and changes often.

### Gaps
- I did not verify the Python framework adapter import paths (e.g., `blaxel.langgraph`) or the full CLI command list.
- The REST API base for sandboxes beyond `api.blaxel.ai/v0` was not detailed here.

## 4. Integrations with agent frameworks

### Takeaway
Blaxel is framework-agnostic. Native TS helpers (`blModel`/`blTools`) exist for LangChain/LangGraph, LlamaIndex, Vercel AI SDK and Mastra. Tutorials cover Claude Agent SDK (three variants), Claude Code, Claude Managed Agents, OpenAI Agents SDK and API, Codex, CrewAI, Google ADK, PydanticAI, n8n, Amp, OpenClaw, NVIDIA OpenShell, DeepSeek Harness, Herdr and Tailscale.

### Cited Findings
- `blModel`/`blTools` convert Blaxel-hosted models and MCP tools into framework-native objects for `langgraph`, `llamaindex`, `vercel` and `mastra` — [Develop agents in TS](https://docs.blaxel.ai/Agents/Develop-an-agent-ts)
- The tutorial directory includes ADK, Amp, Astro, Claude-Agent-SDK (deploy, MCP, Code-Mode), Claude-Code, Claude-Managed-Agents, Code-server, Codex, CrewAI, Custom-Agents, DeepSeek-Harness, Docker, Expo, Herdr, LangChain, LlamaIndex, Mastra, Next.js, OpenAI-Agents-API, OpenAI-Agents-SDK (and Deployment), OpenClaw, OpenShell, PydanticAI, Tailscale, Vercel-AI and n8n — [Blaxel docs: Tutorials](https://docs.blaxel.ai/Tutorials/Overview) (source tree [here](https://github.com/blaxel-ai/docs/tree/main/Tutorials))
- Claude Agent SDK: "Deploy a Claude Agent SDK agent to Blaxel Agents Hosting… and colocate it close to the sandboxes it works on." Agents Hosting "uses the same underlying infrastructure as sandboxes." — [Claude Agent SDK tutorial](https://docs.blaxel.ai/Tutorials/Claude-Agent-SDK)
- OpenAI Agents API integration (2026-09-10): OpenAI-hosted agents run tools in Blaxel sandboxes, keep files on Agent Drive, and reconnect workers by webhook. Requires Agents API preview access — [Changelog](https://docs.blaxel.ai/changelog)
- Non-framework integrations include AgentMail, Gmail, Google Maps and Rippletide — [Integrations folder](https://github.com/blaxel-ai/docs/tree/main/Integrations)

### Inferences
- AgentMail is also a likely adjacent ecosystem player; the sponsor Inkbox is in a similar space. Combining Blaxel sandboxes with other sponsors' agent primitives (Stripe for payments, Supabase for DB, Primitive or Inkbox for communication, Manufact for MCP) is a natural cross-track strategy.

### Gaps
- Python-side framework helper coverage was not confirmed.

## 5. The "Something a Human Would Never Want" prize track

### Takeaway
The YC event page lists the track as "Blaxel: Something a Human Would Never Want." As of my search (2026-10-11), the description still reads "Coming shortly." I found no published prize amount or criteria. The name fits Blaxel's own thesis: a cloud "where AI agents themselves are the primary users."

### Cited Findings
- Event: "Make Something Agents Want," hosted by YC teams building for agents. Sponsors are Armature, Blaxel, Inkbox, Insforge, Manufact, Primitive, Stripe and Supabase. Hacking begins Oct 17, 2026. Submissions and live demos are on Oct 18, with winners announced around 12:15 PM and the event ending at 1:00 PM. Blaxel's track description says "Coming shortly." — [YC event page (via search snippets)](https://events.ycombinator.com/MakeSomethingAgentsWant)
- Other visible tracks: Manufact (best MCP server), Insforge (agent-native cloud), Armature (best agent experience), Primitive.dev (agent communication) — [YC event page (via search)](https://events.ycombinator.com/MakeSomethingAgentsWant)
- The event is at YC's SF HQ with about 200 builders expected — [TipRanks](https://www.tipranks.com/news/private-companies/manufact-deepens-ai-agent-ecosystem-engagement-with-yc-hackathon)
- Blaxel's framing: "Blaxel is a cloud where AI agents themselves are the primary users… Sandboxes give them their own dedicated personal computer(s)" — [Overview](https://docs.blaxel.ai/Overview). Also "agents… will build ad hoc user-facing software to expose as micro-apps to end-users — whether humans-in-the-loop, or other agents" — [Applications](https://docs.blaxel.ai/Applications/Overview)

### Inferences (interpretation; not official)
- The likely meaning is a product whose only sensible customer is an agent. A human would find it useless, tedious or absurd, but agents need it badly. Examples: a service that wakes in 25ms for thousands of sub-second tool calls; a machine-readable-only interface; a workload that would bore any human (forking 50 parallel universes of a codebase, running millions of micro-experiments, waiting weeks on standby for one event).
- Features that probably score well:
  1. **Uses sandboxes as an agent's own persistent computer.** Standby/resume, keepAlive and schedules let the agent sleep for days and wake instantly.
  2. **Agent-native interfaces**: MCP servers (hosted on Blaxel), the sandbox's built-in `/mcp`, llms.txt, JSON-only outputs, with no human UI needed.
  3. **Scale or parallelism humans couldn't manage**: Batch Jobs fan-out, forking sandboxes to explore branches (Carbon, private preview), and Agent Drive as shared memory across agent swarms.
  4. **A live demo where the "user" is visibly an agent**: e.g., Claude Code or an OpenAI agent provisioning and consuming the product on its own through the Blaxel skills or MCP.
  5. **Humor and provocation in the pitch**: the track title invites products that sound absurd to humans but are clearly valuable to agents.
- Watch the event page and Blaxel's X account in the days before Oct 17 for the official criteria and prize. They may differ from this interpretation.

### Gaps
- No official prize amount, judging rubric or eligibility rules found. The track description was still "Coming shortly" in search snippets. I could not fetch the live page directly.
- No Blaxel X/Twitter or blog post about the hackathon was found.

## 6. Project ideas using Blaxel that should score well

### Takeaway
The strongest ideas make an agent the only user and lean on Blaxel's unique primitives: about 25ms standby/resume, the per-sandbox MCP server, snapshots and forking, Agent Drive shared filesystem, Batch Jobs fan-out, proxy secrets injection, and agent-provisioned infrastructure via skills or MCP.

### Cited Findings (capabilities the ideas rely on)
- Every sandbox exposes MCP tools for files, processes, ports and previews — [Sandbox MCP](https://docs.blaxel.ai/Sandboxes/MCP)
- Fork filesystem, processes and memory into new sandboxes; roll back to checkpoints (private preview) — [Snapshots & forking](https://docs.blaxel.ai/Sandboxes/Fork)
- Agent Drive: concurrent shared FS with label-based ACLs and an S3 endpoint — [Agent Drive](https://docs.blaxel.ai/Agent-drive/Overview); [Changelog](https://docs.blaxel.ai/changelog)
- Proxy secrets injection keeps raw keys away from agent code; egress allowlists by domain, method and path — [Proxy secrets injection](https://docs.blaxel.ai/Sandboxes/Proxy-secrets-injection)
- Sandbox schedules (cron, at, delay) and keepAlive processes — [Changelog](https://docs.blaxel.ai/changelog); [Processes](https://docs.blaxel.ai/Sandboxes/Processes)
- Batch Jobs: parallel tasks up to 24h — [Overview](https://docs.blaxel.ai/Overview)
- Applications: fork a sandbox straight into a live app revision with canary traffic (private preview) — [Infrastructure generations](https://docs.blaxel.ai/Infrastructure/Gens)

### Inferences (idea list; my own suggestions)
1. **"Multiverse" (fork-and-race for agents):** an MCP tool that, given a task, forks a sandbox N times (or spawns N sandboxes or Batch Job tasks), tries N strategies in parallel, and returns only the winning diff plus test evidence. No human wants 50 parallel copies of their dev environment; agents do.
2. **Agent "sleep pods" / dead-man's-switch computers:** a long-lived personal computer per agent that sleeps on standby for weeks at near-zero cost and wakes in 25ms on a webhook, schedule or email. It resumes exactly where it left off, with memory and processes intact. The demo shows an agent resuming a half-finished task days later, with no human dashboard.
3. **Agent-only API marketplace / tool-on-demand:** an MCP server where an agent describes a tool it lacks. The service writes it, tests it in a sandbox, and deploys it as a hosted Blaxel MCP server within minutes, which the agent then calls. Pair with Stripe for agent-to-agent payments to hit cross-sponsor tracks.
4. **Hostile-code quarantine for agents:** a service that takes untrusted repos, binaries or pip packages, detonates them in egress-filtered microVMs, and returns structured JSON verdicts. Humans would never read it; agents use it before `pip install`.
5. **Swarm shared memory:** an Agent Drive-backed "shared brain" filesystem with ACLs, through which many agents (Claude Code, Codex, OpenAI agents) coordinate via files. Includes an MCP front-end for locking and claims.
6. **Infinite-patience workers:** Batch Jobs that do work no human would tolerate. Examples: brute-force A/B testing of 1,000 prompt variants; scraping and normalizing every changelog of every dependency; running the full test matrix across 200 library versions. Results are exposed only as machine-readable JSON or llms.txt.
7. **Credential-blind agent runtime:** agents call third-party APIs from sandboxes while the proxy injects secrets, so the agent never sees keys. This is a "vault for agents" demo with audit logs.

Tips for winning (inferred):
- Demo an agent as the end user, e.g., Claude Code with the Blaxel plugin discovering and using your product through MCP.
- Show live numbers on screen: resume latency, sandbox count, fork fan-out and cost.
- Keep the human-facing UI minimal or deliberately absent, consistent with the track title.

### Gaps
- Without published criteria, how judges weigh technical depth against creativity is unknown. Ask the Blaxel booth or Discord at kickoff, and confirm private-preview access (fork, Applications) early.
