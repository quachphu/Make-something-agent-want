# One agent-native build can stack three prizes

The best bet at YC's "Make Something Agents Want" hackathon (Oct 17–18, 2026) is one agent-facing product that enters several tracks at once. Concretely: an MCP server built on Manufact's mcp-use framework, instrumented with Armature's analytics, that uses Primitive email for human and agent-to-agent communication. Those three tracks hold most of the event's cash: first prizes of **$3,000 (Primitive), $3,000 plus $6,000 in credits (Manufact) and $1,000 plus $1,000 in credits (Armature)**. All three judge panels value the same things: agents as the primary user, a few well-designed tools, asynchronous human-in-the-loop, and measured evidence that agents succeed ([YC event page](https://events.ycombinator.com/MakeSomethingAgentsWant)). The eight sponsors cover four layers of an agent's stack:

| Layer | Sponsors |
|---|---|
| Interface | Manufact, Armature |
| Communication | Primitive, Inkbox |
| Infrastructure | InsForge, Supabase, Blaxel |
| Economy | Stripe |

Sponsors in the same layer compete directly. Primitive and Inkbox both sell agent email with keyless agent self-signup, and InsForge publishes benchmarks against Supabase's MCP server. Pick one sponsor per layer. Almost every judging panel is the founders or core engineers of the product being judged, so they will notice whether you use their newest features properly or just wrap them. The bigger risk is account limits and preview access, not code:

| Sponsor | Main limit |
|---|---|
| Primitive | Sends only to addresses that wrote to you first, unless you verify a domain |
| Inkbox | SMS needs a carrier-registration wait and a START opt-in from each recipient |
| Stripe | The agent-specific card product (Issuing for agents) is private preview |
| Blaxel | Sandbox forking is private preview |
| Supabase | Branching needs a paid plan |

As of Oct 11, Blaxel's and Supabase's tracks are still unannounced. There are about **23.5 hours** between the 10:30 AM kickoff and the 10:00 AM demo deadline, so set up accounts, phone numbers and preview access this week.

## Eight sponsors map onto four layers of an agent's stack

Every sponsor sells some part of the same idea: software whose main user is an agent, not a person. The table below collects each track's prize, judges and likely priorities. The tracks differ a lot in cash. Primitive's track is **$6,000 in cash**. Manufact's is **$4,500 in cash plus $9,300 in credits**. InsForge and Armature each offer **$1,800 in cash plus matching credits**. Stripe and Inkbox pay only in credits. Blaxel and Supabase have published no amounts ([YC event page](https://events.ycombinator.com/MakeSomethingAgentsWant)).

| Sponsor | Track | Prizes (1st / 2nd / 3rd) | Judges (role at sponsor) | What judges likely reward |
|---|---|---|---|---|
| Manufact | Best MCP Server for Agents | $3,000 + $6,000 credits / $1,000 + $3,000 / $500 + $300 | Luigi Pederzani (co-founder), Enrico Toniato (CTO), Andrew Khadder (founding engineer) | Idiomatic mcp-use v2 code, stateless design with handles, structured output, annotations, Skills, deployed on Manufact, evals |
| Primitive | Best Agent Communication Setup | $3,000 / $2,000 / $1,000 cash | Ethan Byrd (CEO), Ben Poile (founding MTS), Ashley Ha (likely MTS) | Agent identity, threaded asking and replying, attachments, async coordination, safe handling of inbound mail |
| Stripe | Agents safely participating in the economy | $3k / $2k / $1k credits; $500 credits for every participant; Atlas fee waived for winners | Not announced | A full transaction, clear user control over what the agent can spend, usefulness, creativity |
| InsForge | Agent-Native Cloud | $1,000 / $500 / $300 cash + equal credits | Hang Huang (CEO), Tony Chang (co-founder) | The agent runs the infrastructure; branching plus human approval; token and reliability numbers |
| Armature | Best Agent Experience (AX) | $1,000 / $500 / $300 cash + equal credits | Theodore Otzenberger, Louis Scremin (co-founders) | Agents find, choose and finish workflows with your tool; before/after evals; agent-installable setup |
| Inkbox | Persistent agent identity (email, phone, iMessage, A2A) | $1,000 / $500 / $200 credits | Not announced (Inkbox's CEO organized the event) | Continuity across channels; both human↔agent and agent↔agent |
| Blaxel | Something a Human Would Never Want | TBA ("coming shortly") | TBA | Products only an agent would want, built on perpetual sandboxes |
| Supabase | TBA | TBA | TBA | Security posture (RLS, scoped MCP), heavy platform use |

Judge roles come from the sponsor research: [Manufact blog](https://manufact.com/blog/category/all), [primitive.dev/about](https://www.primitive.dev/about), [Dealroom on InsForge](https://dealroom.co/news/158042-insforge-raises-8m-seed-to-build-cloud-infrastructure-for-ai-agents/) and [YC on Armature](https://www.ycombinator.com/companies/armature). Inkbox CEO Ray Liao announced the event on X ([X post](https://x.com/rayruizhiliao/status/2098103367302283513)), and about **200 builders** are expected at YC's SF office ([TipRanks](https://www.tipranks.com/news/private-companies/manufact-deepens-ai-agent-ecosystem-engagement-with-yc-hackathon)).

Three themes run through the sponsors.

**First, they all ship the same kind of interface for agents.** Each offers some combination of installable Agent Skills (`npx skills add …`), a CLI with `--json` output, a hosted MCP server and a Claude Code or Codex plugin:

| Sponsor | Where the agent-facing tooling is documented |
|---|---|
| Armature | [skills](https://github.com/armature-tech/skills) |
| Blaxel | [skills-mcp](https://docs.blaxel.ai/skills-mcp) |
| Primitive | [skills](https://github.com/primitivedotdev/skills) |
| InsForge | [insforge-skills](https://github.com/InsForge/insforge-skills) |
| Supabase | [AI skills](https://supabase.com/docs/guides/ai-tools/ai-skills) |
| Stripe | [Stripe AI](https://github.com/stripe/agent-toolkit) |

Inkbox and Primitive go further: an agent can create its own account without an API key, and a human confirms it with a 6-digit code ([npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk), [Primitive skills](https://github.com/primitivedotdev/skills)). A project that follows these conventions itself (a `SKILL.md`, a `doctor` command, JSON output, an MCP endpoint) shows the judges you build the way they do.

**Second, agent freedom is limited by human consent everywhere.** Each sponsor builds in a point where a human approves or limits what the agent does:

| Sponsor | Human-consent mechanism |
|---|---|
| InsForge | InstaCloud sends sensitive infrastructure changes to a human for approval ([Dealroom](https://dealroom.co/news/158042-insforge-raises-8m-seed-to-build-cloud-infrastructure-for-ai-agents/)) |
| Supabase | Its MCP server pauses for confirmation before destructive SQL ([supabase/mcp releases](https://github.com/supabase/mcp/releases)) |
| Stripe | The Link agent wallet asks the user to approve every purchase ([TechCrunch](https://techcrunch.com/2026/04/30/stripe-link-digital-wallet-ai-agents-shopping/)) |
| Inkbox | Unclaimed agents can only email the human who signed them up |
| Primitive | Self-signed-up agents can only reply to people who emailed them first |

Visible guardrails are a strong selling point for nearly every panel.

**Third, these products change quickly.** Recent releases:

| Package | Latest version | Release date |
|---|---|---|
| Inkbox SDK | 0.7.18 (about 100 Python releases in 7 months) | Oct 10 |
| Primitive Node SDK | 2.4.0 (CLI at 1.65.0) | Oct 10 |
| `@blaxel/core` | 0.3.25 | Oct 11 |
| `mcp-use` | 2.8.2 | Oct 9 |

Sources: [npm @inkbox/sdk](https://registry.npmjs.org/@inkbox/sdk), [npm @primitivedotdev/sdk](https://registry.npmjs.org/@primitivedotdev%2Fsdk), [npm @blaxel/core](https://registry.npmjs.org/@blaxel/core), [npm mcp-use](https://www.npmjs.com/package/mcp-use). Pin versions on Friday night and check method names against the live docs.

## The interface layer: Manufact pays the most, Armature measures what agents actually do

### Manufact's $9,000 first prize goes to idiomatic, stateless MCP

Manufact is the renamed **mcp-use**. It is a YC S25 company that raised a **$6.3M seed led by Peak XV** in February 2026 ([SiliconANGLE](https://siliconangle.com/2026/02/12/manufact-raises-6-3m-help-developers-connect-ai-agents-model-context-protocol/)). It has two layers. The first is the open-source mcp-use framework (TypeScript server, client, agent, Inspector, tunnel and scaffolder, plus a Python package), which had **10.7k GitHub stars** on Oct 11. The second is Manufact Cloud, which hosts MCP servers from Git with "observability, analytics, evals, submission readiness, and Git-based preview environments" ([mcp-use README](https://github.com/mcp-use/mcp-use)). Hosting is **GitHub-backed only**: you install the Manufact GitHub App, push your repo and run `npx mcp-use deploy`. The CLI never uploads local source ([deployment docs](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/server/deployment/mcp-use.mdx)). One pricing page puts credits at **$0.01 each** ([Manufact pricing.md](https://manufact.com/pricing.md)). If that is current, the $6,000 first-prize credit grant is about 600,000 credits. The live pricing page differs, so the exact terms are uncertain.

The v2 API is typed and stateless. It requires Node ≥ 22.22.2 and ESM. Every tool with an `outputSchema` must return matching `structuredContent`. Session stores are gone: "Do not key business state to an MCP transport session" ([v2 migration doc](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/server/migration.mdx)). This matches the MCP spec dated **2026-07-28**. That spec removes the `initialize` handshake and `Mcp-Session-Id`, keeps state in handles that tools return and the model passes back, makes MCP Apps and Tasks formal extensions, and deprecates sampling, roots and logging ([MCP blog](https://blog.modelcontextprotocol.io/posts/2026-07-28-release-candidate/)).

```ts
import { MCPServer } from "mcp-use"; import { z } from "zod";
const server = new MCPServer({ name: "weather-app", title: "Weather App", version: "1.0.0" });
export const getWeather = server.tool({
  name: "get-weather", description: "Get the current weather for a city",
  inputSchema: z.object({ city: z.string().describe("City to look up") }),
  outputSchema: z.object({ city: z.string(), temperature: z.number(), conditions: z.string() }),
  annotations: { readOnlyHint: true, destructiveHint: false, openWorldHint: true },
}, async ({ city }) => ({ content: [{ type: "text", text: `...` }],
  structuredContent: { city, temperature: 22, conditions: "Sunny" } }));
export default server;
// npx -y create-mcp-use-app@latest → npm run dev (Inspector at /mcp/inspector) → npm run deploy
```

Source: [mcp-use README](https://github.com/mcp-use/mcp-use).

mcp-use also publishes a `skills/<name>/SKILL.md` folder automatically as **Skills over MCP**, which implements the draft SEP-2640 ([skills doc](https://github.com/mcp-use/mcp-use/blob/main/docs/v2/typescript/server/skills.mdx)). It also ships one-line OAuth adapters (Auth0, Clerk, Supabase, WorkOS and others) and OpenAPI-to-MCP conversion ([docs.json](https://github.com/mcp-use/mcp-use/blob/main/docs/docs.json)).

None of the judges has published a rubric. The company's own priorities point to what they will reward:

| Signal | Why it matters to these judges |
|---|---|
| "Agent-first and headless" design ([README](https://github.com/mcp-use/mcp-use)) | Stated product value |
| Testing and evals | Khadder wrote Manufact's screenshot-CLI and MCP-testing posts ([Manufact blog](https://manufact.com/blog/category/all)) |
| Deployment on Manufact Cloud | Their hosting product |
| Few consolidated tools; `response_format` concise/detailed; pagination with hints for narrowing the query; errors that teach the fix; destructive/read-only annotations | Anthropic's guidance on writing tools for agents, the de facto standard for this track ([Anthropic Engineering](https://www.anthropic.com/engineering/writing-tools-for-agents)) |

The track is for servers where agents are the main customer. So MCP App UI Views are polish, not the core of an entry. This track will also be the most crowded, because nearly every team at the event will ship an MCP server.

### Armature rewards proof that agents choose your tool and finish the job

Armature (YC P26) is a three-person company. It started as agent-workflow testing, moved to MCP analytics and evals in July–August 2026, and now sells "get your product picked by coding agents," with **agent.reviews** ("G2 for agents") as its public product ([YC](https://www.ycombinator.com/companies/armature), [Show HN](https://news.ycombinator.com/item?id=49995539)). Its founders are the two judges. Their view is empirical. In a study of **16,893 sessions across 75 repositories**, Claude Code, Codex and Cursor picked the same tool only **42%** of the time. Codex searched the web in about 94% of sessions, Claude Code in about 30% ([Armature blog](https://armature.tech/blog/which-tools-coding-agents-install)). Critics note the headline figures come from a validated subset and that Armature benefits commercially from the result ([cursorworkshop](https://www.cursorworkshop.com/research/17k-runs-of-claude-codex-and-cursor)). Even so, the study shows what matters to these judges: whether agents **discover** a tool and whether they **succeed** with it.

Armature's MCP Analytics SDKs (TypeScript, Python, Go and PHP; Apache-2.0) add an optional `telemetry` argument to every tool schema. The agent fills in `user_intent` and `call_purpose`, and the SDK strips that argument before your handler runs. The SDKs also add a `send_feedback` tool by default, which records requests for capabilities your server lacks ("unmet demand"). A `doctor` CLI checks the setup, and `--json` makes its report machine-readable ([mcp-analytics README](https://github.com/armature-tech/mcp-analytics)). With no API key set, the SDK silently does nothing. Serverless hosts need `delivery: "await"`.

```ts
// npm install @armature-tech/mcp-analytics @modelcontextprotocol/sdk@^1.29.0 zod
import { createMcpAnalyticsServer } from "@armature-tech/mcp-analytics";
const server = createMcpAnalyticsServer(createMyMcpServer);
// env: ANALYTICS_INGEST_API_KEY=ami_us_…, ANALYTICS_INGEST_URL=https://app.armature.tech/api/mcp-analytics/ingest
// verify: npx @armature-tech/mcp-analytics doctor --url http://localhost:3000/mcp --json
```

```python
from armature_mcp_analytics import instrument_fastmcp
from fastmcp import FastMCP
mcp = FastMCP("my-server"); instrument_fastmcp(mcp, {"armature": {"delivery": "await"}})
```

Sources: [mcp-analytics](https://github.com/armature-tech/mcp-analytics), [mcp-analytics-python](https://github.com/armature-tech/mcp-analytics-python).

The agent.reviews rubric spells out Armature's idea of agent experience (AX):

| Element | Contents |
|---|---|
| Scores (1–5) | Usefulness, ease, reliability |
| Outcome | `completed`, `partial` or `blocked` |
| Friction tags | `auth`, `docs`, `unclear_error`, `destructive_risk`, `permissions`, `rate_limit` and others |

Source: [armature-tech/skills](https://github.com/armature-tech/skills).

Armature's own CLI follows the same practices: every command outputs JSON, login doesn't block the terminal (the agent prints an approval link, then `check` completes sign-in), and the token is never shown to the agent ([agent-reviews README](https://github.com/armature-tech/agent-reviews)).

A winning AX demo shows a real agent completing a workflow end to end and the captured `user_intent` in Armature's sessions view. It should also report a before/after pass rate after you rewrote tool descriptions, and show `send_feedback` catching a capability gap. It is unknown whether using Armature's SDK is required for this track; it is clearly an advantage.

**Overlap note:** Manufact Cloud also sells analytics and evals. Armature's SDK has a `/v2` entry point for MCP SDK v2, and mcp-use v2 is built on the official v2 SDK, so the two should work together. That compatibility is untested, so run `doctor` against your mcp-use server in the first hour. If wrapping fails, fall back to `createAnalyticsRecorder`, which supports custom dispatchers.

## The communication layer: Primitive goes deep on email, Inkbox goes wide on channels

### Primitive's $6,000 cash pool rewards threaded, asynchronous, safe email

Primitive (primitive.dev, YC P26) describes itself as "email infrastructure for AI agents." Founder and CEO Ethan Byrd posts as @itsjustemail ([sdks repo](https://github.com/primitivedotdev/sdks), [X](https://x.com/itsjustemail)). Two of its three judges build the product.

The API is at `api.primitive.dev/v1`, runs on Cloudflare Workers, and is generated from an OpenAPI spec into Node, Python and Go SDKs plus a `primitive` CLI. Each account gets a managed `*.primitive.email` domain. Inbound mail arrives in one of three ways:

| Inbound mode | How it works |
|---|---|
| Webhooks | HMAC-signed `email.received` events to your URL |
| Primitive Functions | Hosted JavaScript that runs on each inbound email, with no server |
| `primitive listen` | A durable WebSocket queue that can forward to localhost |

Source: [primitive-functions SKILL.md](https://github.com/primitivedotdev/skills/blob/main/skills/primitive-functions/SKILL.md).

Replies are threaded on the server: the `Re:` subject is derived from the parent message, and the API deliberately rejects a custom subject on reply. Sends without an idempotency key are deduplicated over a 5-minute window ([sdk-node README](https://github.com/primitivedotdev/sdks/blob/main/sdk-node/README.md)). The key feature for agents is ask-and-wait. `GET /sent-emails/{id}/reply?wait=true` long-polls for up to 30 seconds. The CLI's `primitive chat` wraps it with exit codes; exit 3 means "sent, awaiting reply — do not resend" ([OpenAPI spec](https://github.com/primitivedotdev/sdks/blob/main/openapi/primitive-api.yaml), [primitive-chat SKILL.md](https://github.com/primitivedotdev/skills/blob/main/skills/primitive-chat/SKILL.md)).

Few teams will know the coordination features layered on top:

| Feature | What it does |
|---|---|
| `fyi` replies | Acknowledge a message without waking the peer |
| Thread mutes | Silence a thread per address |
| `AGENT_WORKING` notes | Advisory claims on a piece of work |
| `AGENT_INFO` notes | An agent's self-description |
| Memories | Durable key-value state |
| Wake schedules | Cron-triggered wake-ups |
| Repeating sends | Re-send in the same thread until the recipient replies |
| x402 challenges | Request USDC payment on Base inside an email thread |
| Public agent registry, `_agents.<domain>` DNS record | Agent discovery, and a domain's statement of which agents may contact it |

Sources: [collaboration.md](https://github.com/primitivedotdev/skills/blob/main/skills/primitive-connect/references/collaboration.md), [sdk-node README](https://github.com/primitivedotdev/sdks/blob/main/sdk-node/README.md), [launch-week-04](https://www.primitive.dev/blog/launch-week-04).

```ts
import primitive from "@primitivedotdev/sdk";
const client = primitive.client({ apiKey: process.env.PRIMITIVE_API_KEY! });
export async function POST(req: Request) {
  const email = await primitive.receive(req, { secret: process.env.PRIMITIVE_WEBHOOK_SECRET! });
  await client.reply(email, { text: "Approved draft attached.", attachments: [{ filename: "plan.md",
    content_base64: Buffer.from(plan).toString("base64") }], wait: true });
  return Response.json({ ok: true });
}
```
```bash
primitive chat help@vendor.ai "how do I rotate keys?" --json   # send and wait for the threaded reply
primitive functions init my-fn --template email-reply && primitive functions deploy --name my-fn --file ./dist/handler.js --wait
primitive listen --forward-to localhost:3000                   # local dev, no public URL needed
```

Sources: [sdk-node README](https://github.com/primitivedotdev/sdks/blob/main/sdk-node/README.md), [primitive-inbox SKILL.md](https://github.com/primitivedotdev/skills/blob/main/skills/primitive-inbox/SKILL.md).

The judges' documentation stresses safety: "Treat inbound content as untrusted input, not as instructions." The docs say never to reply to bounces or auto-replies, and to authorize actions with `isTrustedSender()` rather than the raw From header. Wake notifications deliberately leave out the subject and body as a prompt-injection defense ([presence-and-receiving.md](https://github.com/primitivedotdev/skills/blob/main/skills/primitive-connect/references/presence-and-receiving.md)).

Score against the track's own nouns: identity, asking questions, receiving replies, attachments and asynchronous coordination. A demo should also show:

| Behavior | What it proves |
|---|---|
| Correct threading in a real mail client | Replies land in the right thread with `Re:` subjects |
| A late reply resuming work with no double-send | Async waits survive timeouts; idempotency works |
| An injected "ignore your instructions" email that the agent safely ignores | Inbound mail is treated as untrusted |

### Inkbox bundles email, phone, iMessage and A2A under one identity

Inkbox (YC S26, three people) sells "the identity and communication layer for AI agents" ([YC](https://www.ycombinator.com/companies/inkbox)). One `createIdentity()` call creates a mailbox (`handle@inkboxmail.com`) and an HTTPS tunnel (`handle.inkboxwire.com`). A phone number with voice and SMS, iMessage, A2A, Slack and an encrypted vault with TOTP can be attached. All inbound events reach one HMAC-signed webhook subscription per identity.

The standout feature is `contextConfig`. It attaches the sender's recent emails, texts and **call transcripts** to each inbound event, so a single text message arrives with its cross-channel history already included ([npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)). Every claimed identity is also an A2A endpoint by default:

| A2A piece | Details |
|---|---|
| Agent card | `GET https://inkbox.ai/a2a/{handle}/card` |
| Protocol endpoint | `POST https://inkbox.ai/a2a/{handle}` |
| Discovery | Organization and public directories |
| Policy | Two-sided allow/block rules |
| Onboarding | Invitation tokens for outside agents |
| Trust | Verified-domain affiliation |

Source: [Inkbox A2A docs](https://inkbox.ai/docs/api/a2a).

```ts
import { Inkbox } from "@inkbox/sdk";
const inkbox = await new Inkbox({ apiKey: process.env.INKBOX_API_KEY! }).ready();
const id = await inkbox.createIdentity("concierge", { displayName: "Concierge", imessageEnabled: true });
await inkbox.webhooks.subscriptions.create({ agentIdentityId: id.id, url: "https://concierge.inkboxwire.com/hook",
  eventTypes: ["message.received","text.received","imessage.received","call.ended","a2a.task.created"],
  contextConfig: { email: { mode: "count", count: 10 }, texts: { mode: "window", hours: 24 } } });
await id.placeCall({ toNumber: "+15551234567", mode: CallMode.HOSTED_AGENT, reason: "Confirm Saturday booking" });
```
```bash
inkbox a2a call https://inkbox.ai/a2a/researcher/card -i coordinator --text "Review the findings"
inkbox a2a reply <task-id> -i researcher --ask --text "Which quarter?"   # input-required
```

Sources: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk), [npm @inkbox/cli](https://www.npmjs.com/package/@inkbox/cli).

The founders started out fighting 2FA codes and confirmation emails in browser agents ([yespress](https://yespress.io/inkbox-yc-s26)). So projects that use the vault plus email to finish a real signup also match the company's origin.

Pricing limits shape the demo:

| Plan | Price | What you get |
|---|---|---|
| Free | $0 | 3 identities, no phone number, a footer added to outgoing mail |
| Developer | $30/month | One dedicated number with 300 SMS and 30 call minutes |

Source: [Inkbox pricing](https://inkbox.ai/pricing).

### Head to head: pick one communication backbone, not both

| Dimension | Primitive | Inkbox |
|---|---|---|
| Channels | Email only, very deep | Email, voice, SMS/MMS, iMessage, Slack, A2A, tunnel, vault |
| Agent-to-agent | Email threads plus networks, registry, `fyi` acks, work claims | Standard A2A protocol: agent cards, directories, invitations |
| Ask and wait | `chat` / `reply?wait=true` long-poll; Functions; `listen` | Webhooks with cross-channel `contextConfig`; polling iterators |
| Keyless agent signup | Yes; reply-only `agent` plan | Yes; unclaimed agents can only email their human |
| Unique extras | Memories, wake crons, repeating sends, x402 over email, DNS consent record | Hosted voice agent, iMessage tapbacks and group chats, Companion mode, TOTP vault |
| Prize | **$6,000 cash** | **$1,700 credits** |

Both sell agent email, both let agents sign themselves up with a 6-digit human code, and both ship Claude Code plugins. Third-party coverage already frames them as competitors ([Primitive research via Lava docs](https://www.lava.so/docs/gateway/providers/primitive.md), [Dial vs Inkbox](https://getdial.ai/compare/dial-vs-inkbox)).

A project that sends email through one and calls through the other could formally qualify for both tracks, but each panel would see a diluted use of its product. The cash difference favors Primitive as the backbone. The exception is an idea that genuinely needs voice or iMessage, such as a concierge agent that phones a business with no agent of its own. For those, Inkbox's breadth is the whole pitch and it should be the only communication vendor.

## The infrastructure layer: three backends compete for the same agent

### InsForge sells branching and human approval as the "agent-native cloud"

InsForge is an Apache-2.0 "backend platform for agentic coding" with **13.1k GitHub stars**. It bundles Postgres, auth, S3-style storage, an OpenAI-compatible model gateway, Deno edge functions, site hosting and microVM compute ([GitHub](https://github.com/InsForge/InsForge)). On **Sept 29, 2026** it announced an **$8M seed** and **InstaCloud**, "the agent-native serverless cloud," with the line "to kill AWS, GCP, and Azure" ([X @hanghuang_](https://x.com/hanghuang_/status/2104949571789148416)). The track name almost certainly comes from that launch. The judges are the two founders. The company says "almost 99% of all operations and requests now come from agents instead of humans" ([InsForge V2 blog](https://insforge.dev/blog/insforge-launch-v2)).

Agents use InsForge through three layers:

| Layer | Package | Role |
|---|---|---|
| Skills | `npx skills add insforge/insforge-skills` | Static knowledge loaded into the agent's context |
| CLI | `@insforge/cli` | Deterministic actions; most commands support `--json` and `-y`; recommended for agents |
| MCP | `@insforge/mcp` | Live state; `get-backend-metadata` dumps the whole backend in one call |

Sources: [CLI repo](https://github.com/InsForge/CLI), [insforge-mcp](https://github.com/InsForge/insforge-mcp).

```sh
npx @insforge/cli login && npx @insforge/cli link
npx @insforge/cli branch create feature-x          # work on a copy of the whole backend
npx @insforge/cli db query "SELECT * FROM users LIMIT 10" --json
npx @insforge/cli functions deploy my-function --file ./handler.ts
npx @insforge/cli deployments deploy ./dist --json
npx @insforge/cli diagnose advisor                 # self-debugging
npx @insforge/cli branch merge feature-x           # after human review of the diff
```
```ts
import { createClient } from '@insforge/sdk';
const insforge = createClient({ baseUrl: 'https://<app>.insforge.app', anonKey: '…' });
await insforge.database.from('posts').insert([{ title: 'Hello' }]);
const c = await insforge.ai.chat.completions.create({ model: 'anthropic/claude-3.5-haiku', messages });
```

The CLI also covers compute, schedules, secrets, Cloudflare domain purchase, `payments stripe` and `config plan/apply` ([CLI repo](https://github.com/InsForge/CLI)).

The company's evidence is its own MCPMark benchmark. In v2, InsForge reported a **Pass^4 of 42.86% against Supabase MCP's 33.33%** and **7.3M against 17.9M tokens** ([MCPMark v2](https://insforge.dev/blog/mcpmark-benchmark-results-v2)). The benchmark is vendor-run on 21 tasks, and an earlier InsForge benchmark had Supabase ahead on accuracy ([pasqualepillitteri.it](https://pasqualepillitteri.it/en/news/3573/insforge-2-8x-token-claude-code-backend-agent-native-2026-en)).

Read that as a judging signal, not a verdict: these judges count tokens and pass rates. A winning entry has an agent run the cloud with no dashboard clicks. It should work on a branch, send a schema or policy diff to a human, merge and deploy, and show token and intervention counts on screen. Two caveats: the CLI and Skills work only with the hosted cloud, and Compute is in private preview ([GitHub](https://github.com/InsForge/InsForge)).

### Supabase counters with OAuth 2.1 for agents and a hardened MCP server

Supabase's track is still unpublished. Its agent tooling is the most mature in the field.

The remote MCP server at `https://mcp.supabase.com/mcp` uses OAuth 2.1 with dynamic registration. Three URL parameters lock it down: `read_only=true`, `project_ref=<ref>` and `features=<groups>`. Its tool groups cover database, debugging, development, Edge Functions, account, docs, branching and storage. Branching is experimental and needs a paid plan ([Supabase MCP docs](https://supabase.com/docs/guides/ai-tools/mcp)). Version v0.13.0 (Sept 17) requires confirmation before destructive SQL ([releases](https://github.com/supabase/mcp/releases)). Supabase's documentation openly walks through a prompt-injection attack through a support ticket and tells developers never to connect the MCP server to production or give it to end users.

The more interesting piece for this event is **Auth as an OAuth 2.1 provider** (beta, free during the beta). External agents can authenticate as your real users, "your existing RLS policies automatically apply to MCP clients," and policies can check the token's `client_id` ([MCP Authentication docs](https://supabase.com/docs/guides/auth/oauth-server/mcp-authentication)). The rest of the agent backend:

| Feature | What it gives an agent backend |
|---|---|
| pgvector `match_documents` RPC | Memory and retrieval |
| Queues (pgmq) | Durable agent task queues |
| Cron + `pg_net` | Waking an agent function on a schedule, as often as every 30 seconds |
| Edge Functions with built-in `gte-small` embeddings | Agent logic and free embeddings |

Sources: [semantic search](https://supabase.com/docs/guides/ai/semantic-search), [Cron quickstart](https://supabase.com/docs/guides/cron/quickstart), [AI models](https://supabase.com/docs/guides/functions/ai-models).

```json
{"mcpServers":{"supabase":{"type":"http",
  "url":"https://mcp.supabase.com/mcp?project_ref=<dev-ref>&features=database,debugging,development,functions,docs"}}}
```
```toml
[auth.oauth_server]           # supabase/config.toml
enabled = true
authorization_url_path = "/oauth/consent"
allow_dynamic_registration = false
```
```sql
select cron.schedule('wake-agent','30 seconds', $$ select net.http_post(
  url:='https://<ref>.supabase.co/functions/v1/agent-tick',
  headers:=jsonb_build_object('Content-Type','application/json','apikey','<publishable>'),
  body:=jsonb_build_object('time', now())) $$);
```

Sources: [OAuth 2.1 server](https://supabase.com/docs/guides/auth/oauth-server/getting-started), [Cron quickstart](https://supabase.com/docs/guides/cron/quickstart).

Supabase's official "Deploy MCP servers" guide hosts MCP on Edge Functions with `--no-verify-jwt`, and notes "Auth support for MCP on Edge Functions is coming soon" ([BYO-MCP docs](https://supabase.com/docs/guides/ai-tools/byo-mcp)). The cleaner hackathon route is to build the MCP server with mcp-use, which has a one-line Supabase OAuth adapter, host it on Manufact, and use Supabase as the database and identity provider. Past Supabase hackathons gave awards for best overall, best use of AI, most fun, most technically impressive and most visually pleasing ([LW15 hackathon](https://supabase.com/blog/lw15-hackathon)). That suggests a broader, more general-purpose panel than the startup sponsors'.

### Blaxel gives each agent a computer that wakes in 25 ms

Blaxel calls itself "a cloud where AI agents themselves are the primary users" ([Blaxel docs](https://docs.blaxel.ai/Overview)), which matches the hackathon's theme almost word for word. It is a YC X25 company that raised a $7.3M seed led by First Round. **Baseten acquired it on Sept 10, 2026**, and Blaxel says "your sandboxes, storage, networking, API keys, credits, and support contacts stay the same" ([Baseten blog](https://www.baseten.co/blog/blaxel-is-joining-baseten-to-build-the-future-of-agentic-cloud/), [Blaxel about](https://blaxel.ai/company/about)).

Its core product is the microVM sandbox. A sandbox snapshots its full memory, processes and filesystem when idle, resumes from standby in **under 25 ms**, and costs nothing for memory while in standby ([Sandboxes docs](https://docs.blaxel.ai/Sandboxes/Overview)). Every sandbox exposes its own MCP server at `/mcp`, with tools for files, processes, ports and preview URLs ([Sandbox MCP](https://docs.blaxel.ai/Sandboxes/MCP)). Other capabilities:

| Capability | Status |
|---|---|
| Proxy secrets injection: code never sees raw API keys; egress filtered by domain, method and path | Public preview |
| Agent Drive (shared POSIX filesystem) | Available |
| Batch Jobs (tasks up to 24 hours) | Available |
| Hosted agents and MCP servers | Available |
| Snapshots and forking | **Private preview** |

Sources: [Proxy secrets](https://docs.blaxel.ai/Sandboxes/Proxy-secrets-injection), [Snapshots & forking](https://docs.blaxel.ai/Sandboxes/Fork).

Third-party sources put pricing at about **$0.04 per GB-hour** of active memory and **$200** in signup credits ([AgentDeals](https://agentdeals.dev/best/free-agent-sandbox)). These figures are unverified against Blaxel's own pricing page.

```typescript
import { SandboxInstance } from "@blaxel/core";
const sb = await SandboxInstance.createIfNotExists({ name: "agent-pc-42", image: "blaxel/base-image:latest",
  memory: 4096, ports: [{ target: 3000, protocol: "HTTP" }], externalId: "agent-42", region: "us-pdx-1" });
const r = await sb.process.exec({ command: "npm test", workingDir: "/app", waitForCompletion: true });
const preview = await sb.previews.createIfNotExists({ metadata: { name: "app" }, spec: { port: 3000, public: true } });
```

Source: [Sandboxes docs](https://docs.blaxel.ai/Sandboxes/Overview). Install with `curl -fsSL https://blaxel.ai/install.sh | sh`, then `bl login`, then `bl setup` to put Blaxel skills into Claude Code or Codex ([Get started](https://docs.blaxel.ai/Get-started)).

The track name, "Something a Human Would Never Want," still has the description "Coming shortly" ([YC event page](https://events.ycombinator.com/MakeSomethingAgentsWant)). The most natural reading is a product only an agent would use. Examples: forking 50 copies of a dev environment to race strategies, sleeping for weeks and waking on a webhook in 25 ms, or quarantining untrusted packages in egress-filtered microVMs. This interpretation is inference, not published criteria.

| Dimension | InsForge | Supabase | Blaxel |
|---|---|---|---|
| Core abstraction | Agent-operated full backend + cloud | Postgres platform + agent tooling | Agent-owned microVM computers |
| Branching / snapshots | `branch create/merge/reset` via CLI | MCP branching, experimental and paid | Snapshot/fork, private preview |
| Agents as end users | Model gateway, x402 integrations | OAuth 2.1 server + RLS per `client_id` | Sandbox MCP per VM, secrets proxy |
| Hosts MCP servers | Functions/compute | Edge Functions (auth "coming soon") | MCP Servers Hosting |
| Prize | $1,800 cash + credits | TBA | TBA |

InsForge positions itself as the agent-native alternative to Supabase, while Supabase has narrowed the gap with skills, elicitations and scoped tokens. Neither claim has independent benchmark support ([Sealos comparison](https://sealos.io/blog/insforge-vs-supabase/)). Pick InsForge if you are chasing its cash track. Pick Supabase if you need mature auth and RLS for agents acting on behalf of users. Using both in one project will look unfocused to both panels. Blaxel is complementary to either: it is compute, not a database.

## The economy layer: Stripe gives agents five ways to spend safely

Stripe's track asks for an agent that can "safely participate in the economy: buy products, provision services, manage business spending, or pay for the resources it needs," with "clear control over what their agents can do and spend" ([YC event page](https://events.ycombinator.com/MakeSomethingAgentsWant)). Every participant gets $500 in credits regardless of outcome.

The agent toolkit has become a thin client of the remote MCP server at `https://mcp.stripe.com`. Version 0.7.0+ initializes asynchronously and **fails with no fallback if mcp.stripe.com is unreachable**. The permissions on a Restricted API Key (`rk_…`), not code, decide which tools an agent gets ([MIGRATION.md](https://github.com/stripe/agent-toolkit/blob/main/tools/python/MIGRATION.md)). Those tools are seller-side business operations (customers, payment links, invoices, refunds, subscriptions, disputes and docs search), not purchasing ([agent-toolkit](https://github.com/stripe/agent-toolkit)).

The products where an agent spends money are newer, and several are gated:

| Need | Stripe product | Status (Oct 2026) |
|---|---|---|
| Agent buys from a merchant | Shared Payment Tokens (`usage_limits` max_amount/currency/expires_at, seller-scoped, revocable) | Public preview, `Stripe-Version: 2026-09-30.preview` ([SPT docs](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens?agent-seller=agent)) |
| Agent holds a card | Issuing for agents (single-use virtual cards) | **Private preview** ([Issuing agents](https://docs.stripe.com/issuing/agents/programmatic-checkout)) |
| Consumer approves each purchase | Link agent wallet | Launched 2026-04-29 ([TechCrunch](https://techcrunch.com/2026/04/30/stripe-link-digital-wallet-ai-agents-shopping/)) |
| Agent provisions SaaS (Neon, Supabase, Vercel, Clerk…) | Stripe Projects CLI | Developer preview / beta ([Stripe blog](https://stripe.com/blog/stripe-projects-adds-new-agents-providers-developer-controls)) |
| Agent pays another business | `stripe pay` + Stripe Directory | Requires a funded financial account ([stripe-pay skill](https://github.com/stripe/agent-toolkit/blob/main/skills/stripe-pay/SKILL.md)) |
| Pay per API call (HTTP 402) | MPP with Tempo (launched 2026-03-18); x402 USDC on Base | Early access / preview ([The Block](https://www.theblock.co/post/389352/stripe-adds-x402-integration-usdc-agent-payments)) |
| Bill users for LLM tokens | `@stripe/token-meter`, `@stripe/ai-sdk` | **Private preview** ([token-meter](https://github.com/stripe/agent-toolkit/blob/main/llm/token-meter/README.md)) |

The most reliable demo path needs no preview access: standard Issuing in test mode. Create virtual cards with `spending_controls`, simulate purchases with test-helper authorizations, and approve or decline each authorization live through the `issuing_authorization.request` webhook, which must answer **within 2 seconds** ([real-time authorizations](https://docs.stripe.com/issuing/controls/real-time-authorizations)). Whether Issuing test mode is open to every new sandbox account is unverified, so check it this week.

```python
card = stripe.issuing.Card.create(cardholder=holder.id, currency="usd", type="virtual", status="active",
    spending_controls={"spending_limits": [{"amount": 5000, "interval": "per_authorization"},
                                           {"amount": 20000, "interval": "monthly"}],
                       "allowed_categories": ["computer_software_stores"]},
    metadata={"agent_id": "agent_42", "task_id": "task_9"})
stripe.issuing.Authorization.TestHelpers.create(card=card.id, amount=1999,
    merchant_data={"category": "computer_software_stores", "name": "Acme SaaS"})

@app.post("/webhooks/issuing")            # must answer in < 2 s
def hook():
    event = stripe.Webhook.construct_event(request.data, request.headers["Stripe-Signature"], WHSEC)
    if event.type == "issuing_authorization.request":
        a = event.data.object
        return jsonify({"approved": policy_allows(a.card.metadata["agent_id"], a.amount, a.merchant_data)})
    return "", 200
```

Source: patterns from [Stripe Issuing controls docs](https://docs.stripe.com/issuing/controls/real-time-authorizations). Check exact field names against current docs.

Because of the 2-second window, a human cannot approve inside the webhook. Human approval has to happen *before* the purchase, for example by raising a limit or minting a short-lived SPT after a reply. The webhook then enforces the policy automatically.

Judges will look for:

| Signal | Example |
|---|---|
| A least-privilege restricted key | The agent's key can only do what its job needs |
| A visible policy UI | Where the user sets limits and rules |
| A declined out-of-policy attempt | Shown live on stage |
| Approval followed by success | The same purchase going through after a human approves |
| A kill switch | Freeze the card or revoke the SPT |
| An audit trail | Each authorization tied to agent, task and reasoning through `metadata` |

Avoid building around ChatGPT Instant Checkout: one secondary source says OpenAI retired it in March 2026 ([Hypotenuse AI](https://www.hypotenuse.ai/blog/chatgpts-instant-checkout-the-next-phase-of-agentic-commerce)).

## Five bundles stack cleanly; four pairings collide

No published rule confirms that one project can enter several sponsor tracks. Ask at kickoff. Assuming it can, the sponsors' APIs line up into a few natural bundles. Some integrations already exist:

| Existing integration | Source |
|---|---|
| mcp-use has a Supabase OAuth adapter | [docs.json](https://github.com/mcp-use/mcp-use/blob/main/docs/docs.json) |
| InsForge's CLI has `payments stripe` | [CLI](https://github.com/InsForge/CLI) |
| Stripe Projects lists Supabase as a provider | [Stripe blog](https://stripe.com/blog/stripe-projects-adds-new-agents-providers-developer-controls) |
| Primitive supports x402 payment challenges over email; Stripe accepts x402 USDC on Base | [sdk-node README](https://github.com/primitivedotdev/sdks/blob/main/sdk-node/README.md), [The Block](https://www.theblock.co/post/389352/stripe-adds-x402-integration-usdc-agent-payments) |

Bridging Primitive's x402 with Stripe's is a plausible but untested combination.

| Bundle | Tracks | Why it fits together | Cash ceiling (1st place everywhere) |
|---|---|---|---|
| Interface core | Manufact + Armature | Both judge an agent-facing MCP or CLI. Armature's SDK wraps the mcp-use server; Manufact hosts it | $4,000 cash + $7,000 credits |
| Communication + interface | Primitive + Manufact + Armature | An MCP server whose tools are "ask a human or agent by email and wait" | $7,000 cash + $7,000 credits |
| Economy + communication | Stripe + Primitive (or Inkbox) | Approval requests travel by email or iMessage; Stripe enforces limits | $3,000 cash + $3,000 credits |
| Backend + economy | InsForge + Stripe, or Supabase + Stripe | `insforge payments stripe`; Stripe Projects provisioning Supabase | $1,000 cash + $4,000 credits (InsForge) |
| Agents-only compute | Blaxel + Manufact | A Manufact-hosted MCP front end over Blaxel sandboxes | $3,000 cash + $6,000 credits + Blaxel TBA |

These pairings collide:

| Collision | Why it hurts |
|---|---|
| **Primitive vs Inkbox** | Same category; each panel wants to be the backbone |
| **InsForge vs Supabase** | InsForge benchmarks itself against Supabase's MCP |
| **Where the MCP server is hosted** | Manufact Cloud, Blaxel MCP hosting, Supabase Edge Functions and InsForge functions all do it. The host shows which sponsor you're backing, so host on Manufact if you want its $9,000 first prize |
| **Analytics** | Manufact Cloud and Armature both sell MCP analytics and evals. Use Armature for the session evidence and Manufact for hosting, and present them as two separate jobs |

## Twelve gotchas that can break a live demo

Most failure modes here are account-level, not bugs. With 23.5 hours of hacking and live demos at 10:00 AM on a Saturday, each one costs a slot on stage.

| Sponsor | Gotcha | Mitigation |
|---|---|---|
| Primitive | Sends succeed only to `*.primitive.email`, your verified domains, or addresses that sent you authenticated mail; upgrading to the developer plan "does not unlock sending to arbitrary recipients" ([OpenAPI spec](https://github.com/primitivedotdev/sdks/blob/main/openapi/primitive-api.yaml)) | Have judges email the agent first; keep agents on `*.primitive.email`; verify a domain; ask about an `any_recipient` grant or a signup code |
| Primitive | Per-attachment download endpoint is "Pending service release"; Functions can't import `node:crypto` | Use `attachments_download_url` or `attachments.tar.gz`; import from `@primitivedotdev/sdk/api` ([functions skill](https://github.com/primitivedotdev/skills/blob/main/skills/primitive-functions/SKILL.md)) |
| Inkbox | New numbers need **10–15 minutes** of carrier (10DLC) registration; recipients must text **START** first; 100 recipients per number per day ([npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)) | Provision numbers Friday morning; have judges text START or `connect @handle` before the demo |
| Inkbox | Shared iMessage router requires the human to text first; the Free plan has no phone number and adds a footer to mail ([Inkbox pricing](https://inkbox.ai/pricing)) | Budget $30 for the Developer plan or ask the booth for credits; claim a dedicated iMessage line if groups are needed |
| Stripe | Issuing for agents, token billing and MPP are private preview or early access; SPTs need a preview API version | Build on standard Issuing test mode plus test helpers; request preview access this week |
| Stripe | Toolkit v0.7+ fails hard if `mcp.stripe.com` is unreachable; the 2-second authorization webhook can't wait for a human | Test the venue network early; approve *before* authorization |
| Blaxel | Snapshot/fork and Applications are private preview; free-plan quotas cap concurrent sandboxes; external connections drop on standby ([Quotas](https://docs.blaxel.ai/Security/Quotas)) | Fall back to N fresh sandboxes from one image; use `keepAlive` during the demo |
| Supabase | Branching is experimental and paid; Edge Function MCP auth is "coming soon"; OAuth 2.1 server is beta; vector buckets are alpha | Use a throwaway dev project; host MCP on Manufact with mcp-use's Supabase OAuth adapter |
| Supabase | MCP v0.13 asks for confirmation before destructive SQL, which can stall headless agents | Keep approvals on in the demo and narrate them as a safety feature |
| InsForge | CLI and Skills work only on the hosted cloud; Compute is private preview; InstaCloud's URL is unconfirmed | Create the cloud project before the event; keep a self-hosted Docker fallback (port 7130) |
| Manufact | Deploy is GitHub-only; v2 needs Node ≥ 22.22.2 and ESM; v2 has no session state | Push the repo early; design tools around handles; deploy a hello-world on Friday |
| Armature | SDK silently does nothing without a key; US and EU keys can't be mixed; serverless needs `delivery: "await"` | Run `doctor --json` right after wiring ([mcp-analytics](https://github.com/armature-tech/mcp-analytics)) |

Most of this can be done before Oct 17 without writing hackathon code:

| Before Oct 17 | Why |
|---|---|
| Create accounts with every sponsor you plan to use | Saves kickoff time |
| Install each sponsor's skills or plugin into your coding agent | Lets the agent scaffold and deploy immediately |
| Request Stripe Issuing test mode and any preview access | Preview access is the hardest dependency to get |
| Ask Blaxel about fork access | Private preview may need enabling for your workspace |
| Verify a sending domain for Primitive | Lifts the recipient restriction |
| Watch the event page for the Blaxel and Supabase criteria | Both tracks are still unannounced |

## Ranked project ideas for a 23.5-hour build

The table ranks ideas by cash ceiling (if a project wins first in every track it enters), chance of winning given likely crowding, and how much can realistically be built between 10:30 AM Friday and 10:00 AM Saturday. Ceilings assume multi-track eligibility; they are maximums, not expected values.

| Rank | Project | Tracks | Cash / credits ceiling | Feasibility | Main risk |
|---|---|---|---|---|---|
| 1 | **"Callback": human-and-agent loop as an MCP server** | Primitive, Manufact, Armature | $7,000 / $7,000 | High | Primitive recipient restrictions |
| 2 | **"Allowance": agent spending control plane** | Stripe, Primitive (approvals), Armature | $4,000 / $4,000 + $500 | Medium | Issuing test-mode access |
| 3 | **"Multiverse": fork-and-race sandboxes for agents** | Blaxel, Manufact, Armature | $4,000 / $7,000 + Blaxel TBA | Medium | Fork is private preview; track criteria unknown |
| 4 | **"Ship-with-a-veto": agent operates InsForge with branch approvals over email** | InsForge, Primitive, Stripe | $4,000 / $4,000 | Medium-high | Splits focus across three panels |
| 5 | **"Agent-ready SaaS": OAuth 2.1 + RLS so users' agents act as them** | Supabase, Manufact, Armature | $4,000 / $7,000 + Supabase TBA | High | Supabase track may favor something else |
| 6 | **Multi-channel concierge with A2A negotiation** | Inkbox, Stripe | $0 / $4,000 | Medium | Credits only; SMS/iMessage opt-in logistics |
| 7 | **AX doctor: an MCP server that grades other MCP servers** | Armature, Manufact | $4,000 / $7,000 | High | Crowded idea; judges may see it as overlapping their own products |

**1. "Callback" is the best combination of value and feasibility.** It is a small mcp-use v2 server whose tools turn human-in-the-loop and agent-to-agent messaging into stateless handles:

| Tool | What it does |
|---|---|
| `ask(to, question, attachments?)` | Sends the question by email and returns a `question_id` handle |
| `await_reply(question_id, timeout)` | Wraps Primitive's long-poll `reply?wait=true` |
| `delegate(agent_handle, task)` | Hands a task to another agent by email |
| `next_awaiting()` | Wraps `inbox next`: the oldest email still waiting for a reply |

Each agent gets its own `*.primitive.email` identity and an `AGENT_INFO` profile. Suspended state lives in Primitive Memories. A `repeat` reminder nags slow humans, and `isTrustedSender` gates any reply that grants approval.

Add Armature's wrapper so the dashboard shows each call's `user_intent`, and ship a `skills/` playbook through Skills over MCP. The demo has Claude Code reach a decision during a refactor, email the human a diff, and time out. It then resumes with no double-send when the human's threaded reply arrives with a corrected file attached. Finally an injected malicious email is shown being ignored.

This hits every item in Primitive's track text, Manufact's stateless-handle design and Armature's measurement thesis in one artifact. Its weakness is that Primitive already runs an MCP server, so the pitch must stress orchestration and coordination (claims, `fyi` acks, resumption) rather than wrapping its API.

**2. "Allowance" is the strongest Stripe entry and reuses most of Callback's plumbing.** A user creates an agent and receives two things: a restricted Stripe key and a test-mode Issuing card with `spending_controls` and an allowlist of merchant categories. The real-time authorization webhook enforces the policy within 2 seconds. Anything above the auto-approve threshold first goes to the human over Primitive email; a trusted "approve" reply raises the limit or issues a single-use card. The demo shows a declined out-of-policy purchase, an email approval, a successful retry, and a kill switch that freezes the card, all tied to an audit log through card `metadata`. If Stripe grants SPT or Issuing-for-agents access, swap those in for a more native story.

**3. "Multiverse" fits Blaxel's thesis best but carries the most unknowns.** An MCP tool takes a coding task, starts N sandboxes from the same image and repository state (or forks one, if private-preview access arrives), runs N strategies in parallel, and returns only the winning diff with test evidence and a cost meter. Nobody wants 50 parallel copies of their dev environment, but agents do. Keep it in reserve until Blaxel publishes criteria. If they reward absurd-to-humans products, rank it first for that track.

Ideas 4 through 7 are solid single-track entries. "Ship-with-a-veto" speaks InsForge's language: branches, human diff approval and token counts. "Agent-ready SaaS" builds the exact pattern Supabase documents: MCP clients acting as real users under RLS keyed on `client_id`. The Inkbox concierge earns only credits, but it competes in a smaller field. The AX doctor is the quickest to build, and it will likely face many similar entries.

## Conclusion

The judging panels agree more than the sponsor list suggests. Founders of an MCP framework, an AX analytics company, an email provider and a backend cloud all describe the same winning entry: an agent can find the product, act through a few typed tools, pause for a human or another agent without losing state, and leave measurable evidence that it succeeded. That agreement is why one well-designed project can credibly enter three tracks. It also means the scarce resource is depth of integration with each sponsor's newest features, not breadth. Asynchronous waits, claims and acknowledgements, branches with approval, spending limits enforced at authorization, and session-level telemetry are what separate a sponsor's own engineers' praise from a polite nod.

The less obvious lesson is that consent is now a product category. Five of the eight sponsors have independently built a human veto point into their agent flows, and the biggest demo risks (Primitive's recipient rules, Inkbox's START opt-in, Stripe's preview gates) all come from the same concern about agents contacting or charging people unprompted. Teams that design around those limits openly will match the judges' own worldview: the agent only contacts people who wrote first, every purchase passes a policy check, and every risky change goes through a branch. With Blaxel's and Supabase's criteria still unpublished, keep one track slot open until kickoff and lock everything else in this week.
