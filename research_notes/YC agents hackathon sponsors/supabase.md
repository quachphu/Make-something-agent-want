# Supabase: agent products and developer tooling for the YC "Make Something Agents Want" hackathon (Oct 17-18, 2026)

Research date: 2026-10-11. Method note: direct web fetches of supabase.com, events.ycombinator.com, insforge.dev and several news sites failed in this environment (DNS/proxy). Supabase doc content below was pulled live from Supabase's own docs search (the `search_docs` tool of the Supabase MCP server, which returns current docs.supabase.com page content). GitHub pages were fetched directly. Event, Select 2026 and InsForge details come from search-engine summaries of the cited pages, so treat those as second-hand unless a doc URL is quoted.

## 1. Hackathon context and Supabase's prize track

### Takeaway
The event runs Oct 17-18, 2026 at YC SF, and Supabase is one of eight sponsors. I found no published details of a Supabase-specific prize track; it still appears to be "coming soon". The published tracks belong to Manufact (MCP servers), InsForge (agent-native cloud) and Armature (agent experience).

### Cited Findings
- **Event basics:** the event is at YC's San Francisco office. Kickoff is Oct 17 at 10 AM. Submissions and live demos are Oct 18 at 10 AM, and winners are announced at 12:15 PM. — [YC event page (via search summary)](https://events.ycombinator.com/MakeSomethingAgentsWant)
- **Sponsors:** Armature, Blaxel, Inkbox, InsForge, Manufact, Primitive, Stripe and Supabase. It is "hosted by YC-backed companies building for agents." — [YC event page (via search summary)](https://events.ycombinator.com/MakeSomethingAgentsWant)
- **Published tracks:**
  - Manufact: best MCP server built for agents as the primary customer.
  - InsForge: "agent-native cloud".
  - Armature: best agent experience, for products exposing an agent-facing interface such as MCP or a CLI.
  — [YC event page (via search summary)](https://events.ycombinator.com/MakeSomethingAgentsWant)
- **Organizer framing:** organizer Ray Liao (Inkbox) wrote: "We are hosting a hackathon at YC October 17-18 with our friends from @ycombinator @stripe @primitive @insforge @ArmatureInc @blaxelAI @manufact. Come and build something agents want." — [X post](https://x.com/rayruizhiliao/status/2098103367302283513)
- **Expected size:** about 200 builders. This comes from a secondary write-up of a Manufact LinkedIn post. — [TipRanks](https://www.tipranks.com/news/private-companies/manufact-deepens-ai-agent-ecosystem-engagement-with-yc-hackathon)
- **Supabase's history with YC:** Supabase previously ran a "Supabase AI Hackathon at Y Combinator" (Nov 22, 2024). YC partners and Supabase founders judged it, and Anthropic gave every team credits. — [Supabase event page](https://supabase.com/events/supabase-ai-hackathon-at-y-combinator)
- **Past Supabase prize categories (a hint at what they reward):** the Launch Week 15 hackathon awarded Best overall project, Best use of AI, Most fun / best easter egg, Most technically impressive, and Most visually pleasing. — [Supabase LW15 hackathon blog](https://supabase.com/blog/lw15-hackathon)

### Inferences
- Supabase's track is unpublished, so a safe bet is a project that uses Supabase heavily *and* fits an adjacent track. Examples:
  - An MCP server on Supabase Edge Functions, protected by the Supabase OAuth 2.1 server, fits Manufact's MCP track and Armature's agent-experience track.
- **Project ideas likely to impress Supabase.** These follow the features Supabase pushed at Select 2026 (Oct 2026) and in its docs:
  1. **"Your app, agent-ready":** a SaaS app whose users connect their own agents via an MCP server on Edge Functions. Agents authenticate as real users through Supabase Auth's OAuth 2.1 server (dynamic client registration plus a consent screen), and RLS policies keyed on `client_id` limit what each agent can touch. This is the exact pattern Supabase documents for "MCP Authentication".
  2. **Agent memory/state backend:** pgvector (or alpha vector buckets) for long-term memory, Realtime Broadcast to stream agent progress to a UI, Queues (pgmq) for durable agent task queues, and Cron plus `pg_net` to wake agents on a schedule.
  3. **Agent-provisioned backends ("Supabase for Platforms"):** an AI app builder that calls the Management API to create projects, branches and migrations per user. It would run the security advisor before "deploy" and use the project-claim flow to hand the project to the user. This mirrors Lovable/Bolt-style use cases that Supabase targets ("commonly used as a platform by AI Builders").
  4. **Safe-ops agent:** an SRE agent built on the Supabase MCP (`query_logs`, `get_advisors`, branching) that diagnoses issues on a dev branch and opens a fix. It would show off Select 2026's "operate with confidence" theme (elicitations, scoped PATs).
- Expect judges to care about security posture (RLS, read-only/project-scoped MCP, no production data), because Supabase's docs stress it heavily.

### Gaps
- No Supabase prize amount, criteria or track name could be found. The YC event page could not be fetched directly, and searches for a Supabase track at this event returned nothing.
- I could not verify whether Supabase is providing credits to participants.

## 2. Supabase MCP server (remote mcp.supabase.com)

### Takeaway
Supabase hosts a remote MCP server at `https://mcp.supabase.com/mcp`. It uses OAuth 2.1 with dynamic client registration, so no PAT is needed. You can lock it down with three URL parameters: `read_only=true`, `project_ref=<ref>` and `features=<groups>`. All feature groups except Storage are on by default. Supabase explicitly says it is a dev/test tool: don't connect it to production and don't give it to end users.

### Cited Findings
- **Remote setup:** the client redirects you to log in to Supabase and grant access. You must pick the organization that contains the project. Some clients need a restart to detect tools. — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)
- **Basic config:** — [GitHub supabase-community/supabase-mcp](https://github.com/supabase-community/supabase-mcp)
  ```json
  { "mcpServers": { "supabase": { "type": "http", "url": "https://mcp.supabase.com/mcp" } } }
  ```
- **Configuration parameters** — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)

  | Parameter | Effect |
  |---|---|
  | `read_only=true` | Executes all queries as a read-only Postgres user |
  | `project_ref=<id>` | Scopes to one project and disables account tools |
  | `features=<groups>` | Comma-separated list of tool groups to enable |

  Parameters combine, e.g. `https://mcp.supabase.com/mcp?project_ref=abc123&read_only=true`.
- **Tools by feature group** (all groups except Storage enabled by default) — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)
  - **Database:** `list_tables`, `list_extensions`, `list_migrations`, `apply_migration`, `execute_sql`
  - **Debugging:** `get_logs` (API, Postgres, Edge Functions, Auth, Storage, Realtime) and `get_advisors` (security and performance advisors)
  - **Development:** `get_project_url`, `get_publishable_keys`, `generate_typescript_types`
  - **Edge Functions:** `list_edge_functions`, `get_edge_function`, `deploy_edge_function`
  - **Account management** (disabled in project-scoped mode): `list_projects`, `get_project`, `create_project`, `pause_project`, `restore_project`, `list_organizations`, `get_organization`, `get_cost`, `confirm_cost`
  - **Docs:** `search_docs`
  - **Branching** (labeled "experimental"; requires a paid plan): `create_branch`, `list_branches`, `delete_branch`, `merge_branch`, `reset_branch`, `rebase_branch`
  - **Storage** (disabled by default): `list_storage_buckets`, `get_storage_config`, `update_storage_config`
- **Recent changelog** — [GitHub supabase/mcp releases](https://github.com/supabase/mcp/releases)

  | Version | Date (2026) | Changes |
  |---|---|---|
  | v0.10.0 | Aug 10 | Adds `query_logs` for custom SQL log queries (breaking) |
  | v0.11.0 | Aug 20 | Migrates to MCP SDK v2 (breaking) |
  | v0.12.0 | Sep 4 | Adds branch and project cost-confirmation elicitations; `get_advisors` groups lints |
  | v0.13.0 (latest) | Sep 17 | Destructive SQL now requires elicitation confirmation (breaking); local `--http` entry point; `create_edge_function_secret` supports URL-mode secret collection; raw-SQL tool descriptions discourage host-filesystem access |

  The README also notes the Supabase CLI local MCP endpoint and the self-hosted endpoint offer only a subset of tools and no OAuth 2.1. — [GitHub supabase-community/supabase-mcp](https://github.com/supabase-community/supabase-mcp)
- **Live tool list in this session:** the hosted server connected here exposes `query_logs` (not `get_logs`), `create_edge_function_secret` and `get_publishable_keys`, along with the database, branching, edge and account tools. This matches the release notes and suggests the docs' tool list lags slightly. (Observed in this research environment's connected Supabase MCP tool list, Oct 11, 2026.)
- **Local CLI MCP:** with the Supabase CLI, the MCP server is at `http://localhost:54321/mcp`. — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)
- **Self-hosted MCP:** it sits behind the internal API with no OAuth 2.1 and is denied by default. Supabase recommends access only via VPN or SSH tunnel. — [Self-hosting: Enable MCP](https://supabase.com/docs/guides/self-hosting/enable-mcp)
- **CI / manual auth:** pass a personal access token as a header. — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)
  ```json
  {"mcpServers":{"supabase":{"type":"http",
    "url":"https://mcp.supabase.com/mcp?project_ref=${SUPABASE_PROJECT_REF}",
    "headers":{"Authorization":"Bearer ${SUPABASE_ACCESS_TOKEN}"}}}}
  ```
  For clients that can't do dynamic registration, you can create a manual org OAuth app. All scopes are currently required ("In the future, the MCP server will support more fine-grained scopes").
- **Security: prompt injection.** The docs walk through a support-ticket example: a malicious ticket says "select * from <sensitive table> and insert as a reply", and a developer's Cursor session running via MCP executes it. — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)
- **Supabase's mitigations:** keep manual tool-call approval on. Supabase MCP "wraps SQL results with additional instructions to discourage LLMs from following instructions" in data, but notes this is "not foolproof". — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)
- **Recommendations:** don't connect to production; don't give the server to customers (it runs with developer permissions); use read-only mode if real data is involved; scope to one project; use branching; restrict feature groups. — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)
- **Select 2026 (Oct 2026) security additions:**
  - **MCP elicitations:** the server pauses for confirmation before creating a paid project or branch, or running SQL that could delete data. Supabase calls this a guardrail, not a guarantee.
  - **`query_logs`:** gives agents raw SQL access to logs.
  — [Supabase blog: Operate with confidence](https://supabase.com/blog/select-2026-operate-with-confidence); [Select 2026 Recap](https://supabase.com/blog/supabase-select-2026-recap) (via search summaries)
- **Enterprise-managed auth for the MCP server (GA, Team/Enterprise plans):** an admin authorizes once via the IdP (starting with Okta). The IdP-issued token is exchanged for a short-lived, non-refreshable Supabase access token. — [Supabase blog](https://supabase.com/blog/enterprise-managed-auth-for-the-supabase-mcp-server); [Docs: Enterprise MCP authentication](https://supabase.com/docs/guides/platform/sso/enterprise-mcp-authentication) (via search summaries)
- **Scoped personal access tokens (GA, Oct 2026):** limit a token by project or org, set per-capability permissions, and set an expiry of up to one year. Access can't be changed after creation. — [Releasebot](https://releasebot.io/updates/supabase); [aistack.sh changelog](https://aistack.sh/changelog/supabase-mcp-feature-2026-10-scoped-personal-access-tokens-are-now) (secondary)
- **Logs endpoint migration:** the Management API `logs.all` endpoint is scheduled for removal on Sep 23, 2026, and MCP log tooling moved to the new endpoint. — [Supabase changelog](https://supabase.com/changelog/48235-migration-of-supabase-management-api-logs-all-analytics-endpoint-to-logs-endpoint) (via search summary)

### Inferences
- **Hackathon config recommendation:** `https://mcp.supabase.com/mcp?project_ref=<dev-ref>&features=database,debugging,development,functions,docs,branching`. Use a throwaway dev project and keep tool approvals on.
- Newer clients will see elicitation prompts. In the v0.13.0 local server, `skip_elicitations` exists for automation, but avoid it against anything real.
- **Repo location:** the repo is referenced both as `supabase-community/supabase-mcp` (docs, README) and `supabase/mcp` (releases). It has likely moved to the `supabase` org with a redirect.

### Gaps
- The docs page still lists `get_logs`, while the server exposes `query_logs`. The exact current group membership of `query_logs` and `create_edge_function_secret` is unconfirmed.
- I couldn't fetch the full Select 2026 recap, so there may be more agent announcements than captured here.

## 3. Supabase AI/agent building blocks (pgvector, vector buckets, Edge Functions, Realtime, Queues, Cron, Auth OAuth server, Storage, branching, skills, plugin, llms.txt, CLI)

### Takeaway
Supabase covers a full agent backend:
- **Postgres + pgvector** for memory and RAG.
- **Vector buckets** (alpha) for large vector stores.
- **Edge Functions (Deno)** for agent APIs and MCP servers, with a built-in `gte-small` embedding model.
- **Realtime** for streaming state.
- **Queues (pgmq)** and **Cron (pg_cron + pg_net)** for durable and scheduled agent jobs.
- **Auth's OAuth 2.1 server** (beta, free during beta) so agents and MCP clients can log in as your users under RLS.

For coding agents, Supabase ships Agent Skills (`npx skills add supabase/agent-skills`) and a one-step "Supabase Plugin for AI Coding Agents" that bundles the MCP server and the skills.

### Cited Findings
**Agent Skills and plugin**
- **Install:** `npx skills add supabase/agent-skills`. Add `--skill SKILL_NAME` for one skill, `--global` for all projects, or `--all` for every detected agent. Skills install at project scope by default. Search more with `npx skills find QUERY` (skills.sh directory). — [Agent Skills docs](https://supabase.com/docs/guides/ai-tools/ai-skills)
- **Plugin for AI Coding Agents:** bundles the MCP server with the skills `supabase` (core product guidance for DB, Auth, Edge Functions, Storage, Realtime) and `supabase-postgres-best-practices` (query optimization, schema, connections, RLS). — [Plugin docs](https://supabase.com/docs/guides/ai-tools/plugins)
- **Plugin targets:** the June 2026 developer update said the plugin targets Claude Code, Cursor, Codex and Gemini CLI. Supabase also became an official ChatGPT app with 29 tools. — [webdeveloper.com](https://webdeveloper.com/news/supabase-plugin-ai-coding-agents-chatgpt/) (secondary)
- **Server instructions:** the Supabase MCP server's own instructions tell agents to install the skill (`npx skills add supabase/agent-skills`, docs at `https://supabase.com/docs/guides/getting-started/ai-skills.md`) and to prefer local CLI development before remote changes. (Observed in this session's Supabase MCP server instructions.)
- **Markdown docs:** docs pages are available as `.md`, e.g. `.../ai-skills.md` and `.../local-development.md`. (Observed in MCP server instructions.) Note that supabase.com/llms.txt could not be fetched here; see Gaps.

**pgvector semantic search**
- **Setup:** `create extension vector with schema extensions;`, then a column `embedding extensions.vector(512)`. — [Semantic search docs](https://supabase.com/docs/guides/ai/semantic-search)
- **Distance operators:** `<->` (L2), `<#>` (negative inner product), `<=>` (cosine). — [Semantic search docs](https://supabase.com/docs/guides/ai/semantic-search)
- **Indexes:** IVFFlat or HNSW (`create index on documents using hnsw (embedding vector_cosine_ops);`). — [Semantic search docs](https://supabase.com/docs/guides/ai/semantic-search)
- **Canonical RPC** — [Semantic search docs](https://supabase.com/docs/guides/ai/semantic-search)
  ```sql
  create or replace function match_documents (
    query_embedding extensions.vector(512), match_threshold float, match_count int)
  returns setof documents language sql as $$
    select * from documents
    where documents.embedding <=> query_embedding < 1 - match_threshold
    order by documents.embedding <=> query_embedding asc
    limit least(match_count, 200);
  $$;
  ```
  Call it with `supabase.rpc('match_documents', { query_embedding, match_threshold: 0.78, match_count: 10 })`.
- **Filtering:** push filters into the SQL function rather than chaining `.eq()` after `rpc()`. pgvector 0.8.0 supports iterative HNSW scans. — [Semantic search docs](https://supabase.com/docs/guides/ai/semantic-search)

**Vector buckets (ALPHA)**
- **Status:** "This feature is in alpha. Expect rapid changes... possible breaking updates." — [Vector Buckets docs](https://supabase.com/docs/guides/storage/vector/introduction)
- **What it is:** S3-based, with indexes, vectors and metadata, plus cosine/euclidean/L2 metrics and metadata filtering. Up to 500 vectors per batch request, millions per index. — [Vector Buckets docs](https://supabase.com/docs/guides/storage/vector/introduction)
- **When to use which:** Supabase positions vector buckets for large-scale, backend and latency-tolerant workloads, and pgvector for fast prototyping and user-facing low latency. — [Vector Buckets docs](https://supabase.com/docs/guides/storage/vector/introduction)
- **JS API:** `supabase.storage.vectors.from('embeddings').index('documents-openai').putVectors({ vectors: [{ key, data: { float32: [...] }, metadata }] })`. SQL access is via the S3 Vectors foreign data wrapper. — [Storing Vectors docs](https://supabase.com/docs/guides/storage/vector/storing-vectors)
- **Platform-only:** vector buckets, analytics buckets, branching, ETL and the platform Management API are unavailable when self-hosting. — [Self-Hosting docs](https://supabase.com/docs/guides/self-hosting)

**Edge Functions (Deno) for agent backends and AI inference**
- **Built-in AI API:** `new Supabase.ai.Session('gte-small')`, then `model.run(text, { mean_pool: true, normalize: true })`. It needs no external dependencies. `gte-small` is English-only and truncates input at 512 tokens. — [Running AI Models docs](https://supabase.com/docs/guides/functions/ai-models)
- **LLMs via the same API:** Ollama or Llamafile work through the `AI_INFERENCE_API_HOST` secret, but only self-managed for now. A hosted LLM API is "progressively rolling out" (early-access form). — [Running AI Models docs](https://supabase.com/docs/guides/functions/ai-models)
- **Dashboard workflows:** you can create and deploy functions from the dashboard, including "Via AI Assistant", which generates and deploys a function. Templates include OpenAI proxying. The dashboard editor has no version control. — [Edge Functions dashboard quickstart](https://supabase.com/docs/guides/functions/quickstart-dashboard)

**Build your own MCP server on Edge Functions ("Deploy MCP servers")**
- **Official guide:** uses `@modelcontextprotocol/sdk@1.25.3` with `WebStandardStreamableHTTPServerTransport` plus Hono. It notes "Auth support for MCP on Edge Functions is coming soon" and uses `--no-verify-jwt`. — [Deploy MCP servers docs](https://supabase.com/docs/guides/ai-tools/byo-mcp)
  ```ts
  import 'jsr:@supabase/functions-js/edge-runtime.d.ts'
  import { McpServer } from 'npm:@modelcontextprotocol/sdk@1.25.3/server/mcp.js'
  import { WebStandardStreamableHTTPServerTransport } from 'npm:@modelcontextprotocol/sdk@1.25.3/server/webStandardStreamableHttp.js'
  import { Hono } from 'npm:hono@^4.9.7'
  import { z } from 'npm:zod@^4.1.13'
  const app = new Hono()
  const server = new McpServer({ name: 'mcp', version: '0.1.0' })
  server.registerTool('add', { title: 'Addition Tool', description: 'Add two numbers together',
    inputSchema: { a: z.number(), b: z.number() } },
    ({ a, b }) => ({ content: [{ type: 'text', text: String(a + b) }] }))
  app.all('*', async (c) => {
    const transport = new WebStandardStreamableHTTPServerTransport()
    await server.connect(transport)
    return transport.handleRequest(c.req.raw)
  })
  Deno.serve(app.fetch)
  ```
- **Commands:** `supabase init` → `supabase functions new mcp` → `supabase start` → `supabase functions serve --no-verify-jwt mcp` (local at `http://localhost:54321/functions/v1/mcp`) → `supabase link --project-ref <ref>` → `supabase functions deploy --no-verify-jwt mcp` (live at `https://<ref>.supabase.co/functions/v1/mcp`). Test with `npx -y @modelcontextprotocol/inspector`. If the function isn't named `mcp`, use `new Hono().basePath('/your-function-name')`. — [Deploy MCP servers docs](https://supabase.com/docs/guides/ai-tools/byo-mcp)
- **Alternative template:** `npm create mcp-lite@latest` (choose "Supabase Edge Functions (MCP server)"). It uses mcp-lite 0.8.2 and a "two Hono apps" routing pattern. Add it to Claude Code with `claude mcp add my-mcp-server -t http http://localhost:54321/functions/v1/mcp-server/mcp`. — [mcp-lite guide](https://supabase.com/docs/guides/functions/examples/mcp-server-mcp-lite)
- **Select 2026 positioning:** secondary coverage describes Select 2026 (Oct 2) headlining "BYO-MCP": add an MCP server to your Supabase app so users can connect their own agents, running as an Edge Function. — [byteiota](https://byteiota.com/supabase-select-2026-add-an-mcp-server-to-your-app-in-one-command/); [ecosistemastartup](https://ecosistemastartup.com/supabase-select-2026-backend-desde-codigo-y-mcp-para-tu-app/) (secondary)

**Auth as an OAuth 2.1 provider (BETA) and MCP authentication**
- **Status:** "OAuth 2.1 server is currently in beta and free to use during the beta period on all Supabase plans." Enable it in Dashboard → Authentication → OAuth Server, or in `config.toml`: — [OAuth 2.1 Server getting started](https://supabase.com/docs/guides/auth/oauth-server/getting-started)
  ```toml
  [auth.oauth_server]
  enabled = true
  authorization_url_path = "/oauth/consent"
  allow_dynamic_registration = false
  ```
  Local use requires CLI v2.54.11 or later.
- **Endpoints** — [OAuth 2.1 Server getting started](https://supabase.com/docs/guides/auth/oauth-server/getting-started)

  | Endpoint | URL |
  |---|---|
  | Authorize | `https://<ref>.supabase.co/auth/v1/oauth/authorize` |
  | Token | `https://<ref>.supabase.co/auth/v1/oauth/token` |
  | JWKS | `https://<ref>.supabase.co/auth/v1/.well-known/jwks.json` |
  | Discovery | `https://<ref>.supabase.co/.well-known/oauth-authorization-server/auth/v1` |
  | OIDC | `https://<ref>.supabase.co/auth/v1/.well-known/openid-configuration` |

- **Consent UI (you build it):** the page at Site URL + authorization path uses `supabase.auth.oauth.getAuthorizationDetails(authorization_id)`, `approveAuthorization(id)` and `denyAuthorization(id)`, each of which returns a `redirect_url`. — [OAuth 2.1 Server getting started](https://supabase.com/docs/guides/auth/oauth-server/getting-started)
- **Client registration:** in the dashboard or via `supabase.auth.admin.oauth.createClient({ name, redirect_uris, client_type: 'confidential' | 'public' })` with the secret key. Redirect URIs must match exactly (no wildcards). — [OAuth 2.1 Server getting started](https://supabase.com/docs/guides/auth/oauth-server/getting-started)
- **Signing keys:** asymmetric keys (RS256/ES256) are recommended, and they are required for OIDC ID tokens. — [OAuth 2.1 Server getting started](https://supabase.com/docs/guides/auth/oauth-server/getting-started)
- **Custom claims:** Custom Access Token Hooks can add per-`client_id` claims. — [OAuth 2.1 Server getting started](https://supabase.com/docs/guides/auth/oauth-server/getting-started)
- **MCP authentication:** point your MCP server at `https://<project-ref>.supabase.co/auth/v1`. MCP clients auto-discover the config, can register dynamically (opt-in), and act "as your existing users", so "your existing RLS policies automatically apply to MCP clients". Policies can key on the token's `client_id`. FastMCP has a built-in Supabase Auth integration. — [MCP Authentication docs](https://supabase.com/docs/guides/auth/oauth-server/mcp-authentication)
- **Supabase's caveat:** "Supabase doesn't provide MCP server functionality, you can build your own MCP servers..." meaning the OAuth server is the auth layer, not a hosted MCP for your app. Supabase also warns that dynamic registration lets any client register. — [MCP Authentication docs](https://supabase.com/docs/guides/auth/oauth-server/mcp-authentication)

**Queues (pgmq)**
- **Model:** a pull-based FIFO queue built on the `pgmq` extension (Postgres 15.6.1.143 or later). Queue types are Basic (logged) and Unlogged; Partitioned is "coming soon". Each queue creates `pgmq.q_<name>` and `pgmq.a_<name>`. — [Queues quickstart](https://supabase.com/docs/guides/queues/quickstart)
- **Client access:** expose queues to clients via the `pgmq_public` schema, which requires RLS on `q_` tables and grants. For example, `supabase.schema('pgmq_public').rpc('send', { queue_name: 'foo', message: {...}, sleep_seconds: 30 })` and `.rpc('pop', { queue_name: 'foo' })`. — [Queues quickstart](https://supabase.com/docs/guides/queues/quickstart)

**Cron**
- **Scheduling:** `select cron.schedule('name', '30 seconds', '...')`. Sub-minute schedules need Postgres 15.1.1.61 or later. — [Cron quickstart](https://supabase.com/docs/guides/cron/quickstart)
- **Waking an agent function every 30 seconds** (requires `pg_net`): — [Cron quickstart](https://supabase.com/docs/guides/cron/quickstart)
  ```sql
  select cron.schedule('invoke-function-every-half-minute','30 seconds', $$
    select net.http_post(url:='https://project-ref.supabase.co/functions/v1/function-name',
      headers:=jsonb_build_object('Content-Type','application/json','apikey','YOUR_PUBLISHABLE_KEY'),
      body:=jsonb_build_object('time', now()), timeout_milliseconds:=5000) as request_id; $$);
  ```
  See also [Scheduling Edge Functions](https://supabase.com/docs/guides/functions/schedule-functions).

**Realtime**
- Broadcast, including broadcast from the database, is documented at [Realtime Broadcast](https://supabase.com/docs/guides/realtime/broadcast). I did not pull its content in detail here.

**Supabase for Platforms / Management API / Platform Kit** (provisioning backends for AI app builders)
- **Positioning:** "Supabase is commonly used as a platform by AI Builders and frameworks needing a backend. All features of Supabase can be managed through the Management API or the remote MCP Server." — [Supabase for Platforms](https://supabase.com/docs/guides/integrations/supabase-for-platforms)
- **Key endpoints** — [Supabase for Platforms](https://supabase.com/docs/guides/integrations/supabase-for-platforms)
  - `POST /v1/projects`, with `region_selection: {type: "smartGroup", code: "americas"|"emea"|"apac"}`
  - `GET /v1/projects/{ref}/health`: poll until `ACTIVE_HEALTHY`
  - `GET/POST /v1/projects/{ref}/api-keys`: publishable/secret keys
  - `POST /v1/projects/{ref}/branches`
  - `POST /v1/projects/{ref}/database/migrations`: select customers only
  - Restore points and undo: select customers only
  - `POST /v1/branches/{ref}/merge`
  - `GET /v1/projects/{ref}/advisors/security`
  - `GET /v1/oauth/authorize/project-claim`: transfer a project to the user's org
- **Pricing note:** scale-to-zero pricing on Nano instances is only for select customers (partnership form at /solutions/ai-builders). — [Supabase for Platforms](https://supabase.com/docs/guides/integrations/supabase-for-platforms)
- **Platform Kit:** UI components over the Management API, described as "a lightweight version of Supabase Dashboard that you can embed directly in your app". — [Supabase for Platforms](https://supabase.com/docs/guides/integrations/supabase-for-platforms); [Platform Kit docs](https://supabase.com/ui/docs/platform/platform-kit)

### Inferences
- **Fastest 24h stack:**
  1. Create a project and connect the Supabase plugin/MCP plus skills in your coding agent.
  2. Have the agent write migrations (tables, RLS, pgvector) on a dev project.
  3. Put agent logic in Edge Functions, with `gte-small` for free embeddings or an external LLM API.
  4. Use Realtime Broadcast for live UI, Queues plus Cron for long-running and background agent work, and the OAuth 2.1 server if you expose an MCP server to outside agents.
- Combining BYO-MCP on Edge Functions with Supabase Auth OAuth 2.1 currently needs your own token validation. The BYO-MCP guide says Edge Function MCP auth is "coming soon", so budget time for it or use FastMCP's Supabase integration (Python, hosted elsewhere).
- Platform features gated to "select customers" (migrations endpoint, restore points) may not be usable in a hackathon. Use `POST /database/query` or the MCP `apply_migration` instead.

### Gaps
- llms.txt: I could not fetch `supabase.com/llms.txt` (network block), so its current structure is unverified. Docs pages do appear to be served as `.md` URLs.
- The Supabase Studio "AI Assistant" feature set (beyond deploying Edge Functions "Via AI Assistant") was not researched in depth.
- Realtime specifics for agent state (Presence, Broadcast authorization) were not pulled.
- "Supabase Compute", "Declarative Schemas 2.0" and Explorer/Notebooks from Select 2026 appear only in secondary summaries, so their beta/GA status is unverified.

## 4. Supabase vs InsForge (the "agent-native Supabase alternative")

### Takeaway
InsForge (YC P26 / Spring 2026, open source) pitches itself as an agent-native backend: the coding agent provisions and operates DB, auth, storage, functions, compute, hosting and a model gateway via MCP/CLI. Supabase is the more mature, production-proven Postgres platform with broader auth and AI tooling. Most head-to-head claims, especially token and accuracy benchmarks, come from InsForge itself and have shifted between versions.

### Cited Findings
- **InsForge basics:** YC (Spring 2026 / P26), founders Hang Huang and Tony Chang. Its launch says it "lets your AI coding agent deploy and operate the full backend (servers, database, auth, storage, and more) from one consistent CLI." — [YC Launch: InsForge](https://www.ycombinator.com/launches/QP6-insforge-the-backend-platform-for-ai-native-developers) (via search summary)
- **InsForge's own comparison:** Supabase suits developers who configure projects, write policies, review migrations and guide agents carefully. InsForge has agents provision and operate the backend through MCP and CLI. — [InsForge vs Supabase (InsForge)](https://insforge.dev/alternatives/insforge-vs-supabase-ai-agents) (via search summary)
- **InsForge benchmarks (vendor-authored):** InsForge reports 59% fewer tokens than Supabase per run and higher pass@4 (76.2% vs 66.6%). An earlier InsForge benchmark (Nov 2025) showed Supabase *ahead* on accuracy (71.4% vs 61.9%). — [InsForge comparison](https://insforge.dev/alternatives/insforge-vs-supabase-ai-agents); [pasqualepillitteri.it](https://pasqualepillitteri.it/en/news/3573/insforge-2-8x-token-claude-code-backend-agent-native-2026-en) (via search summaries)
- **Sealos comparison:** Supabase has more auth options and more production mileage, plus pgvector. InsForge functions are agent-provisionable through MCP, versus Supabase's "write locally, deploy via CLI" flow. — [Sealos blog](https://sealos.io/blog/insforge-vs-supabase/) (via search summary)
- That description is partly outdated: Supabase's MCP now includes `deploy_edge_function`, `apply_migration`, `create_project` and branching. — [Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)

### Inferences
- **For a hackathon:**
  - Pick **Supabase** if you want mature RLS/Auth (including acting as an OAuth 2.1 provider for agents), pgvector, Realtime, Queues/Cron, and a huge doc and skills ecosystem.
  - Pick **InsForge** if you are targeting its "agent-native cloud" track or want a single agent-operated CLI including hosting and a model gateway.
- Using both is unlikely to score in both sponsor tracks. Choose the backend that matches the track you're chasing.
- Supabase's counter-positioning (plugin plus skills, MCP elicitations, scoped PATs, BYO-MCP) narrows InsForge's "agent-native" differentiation, but no independent benchmark compares the current versions.

### Gaps
- I could not fetch insforge.dev or sealos.io pages directly, so the comparison relies on search summaries of vendor and third-party pages.
- There is no independent benchmark of Supabase MCP vs InsForge MCP on current versions (Supabase MCP v0.13.0, InsForge V2).
