# Inkbox (inkbox.ai): sponsor profile for YC "Make Something Agents Want" hackathon (Oct 17-18, 2026)

Research date: 2026-10-11. Method note: direct page fetches of inkbox.ai, ycombinator.com and getdial.ai failed from the research environment (DNS errors), so the technical sections rely mainly on primary-source package READMEs pulled straight from the npm and PyPI registries (SDK v0.7.18, published 2026-10-10). Those READMEs are written by Inkbox and match the GitHub monorepo. Business facts come from search-result summaries of the YC directory, the YC Launch page, Inkbox's pricing page and secondary sites. Treat search-snippet-only claims as moderately reliable, and check numbers on inkbox.ai/pricing at the event.

Track (from the assignment): "Interesting projects giving agents a persistent identity with email, phone, iMessage, and A2A, so they can communicate with humans and each other." Prizes: $1,000 / $500 / $200 in Inkbox credits.

## 1. What is Inkbox? (product, YC batch, founders, funding, customers)

### Takeaway
Inkbox is a 3-person San Francisco YC Summer 2026 startup (founded 2025; legal entity reportedly Vectorly) that sells an "identity and communication layer for AI agents". One API call creates an agent identity with an email inbox, an HTTPS tunnel address and an encrypted credential vault. A phone number (voice and SMS), iMessage, A2A, Slack and webhooks can be attached to the identity. No funding amount is public beyond standard YC backing.

### Cited Findings
- YC directory headline: "Inkbox: The identity and communication layer for AI agents." It lists Founded: 2025, Batch: Summer 2026, Team Size: 3, Location: San Francisco — [YC company page](https://www.ycombinator.com/companies/inkbox)
- YC Launch title: "Inkbox: Give your AI agents email, phone, iMessage and an internet address". It names Ray (ray@inkbox.ai) as the contact for intros and feedback and lists plugins for Hermes, OpenClaw, Claude Code and Codex — [Launch YC](https://www.ycombinator.com/launches/RIu-inkbox-give-your-ai-agents-email-phone-imessage-and-an-internet-address) (seen through a search summary only, page not fetched directly)
- Pitch: a single API gives each agent a dedicated inbox (custom domain supported), a phone number for calls and texts, iMessage, a persistent HTTPS address for webhooks, and an encrypted vault with TOTP/2FA. The founders say the original problem was that agents building web automations kept needing confirmation emails and 2FA codes — [yespress.io profile](https://yespress.io/inkbox-yc-s26); [YC company page](https://www.ycombinator.com/companies/inkbox)
- Founders: Ray Liao (CEO; MIT CS PhD in ML; previously co-founded Empallo, a virtual cardiovascular clinic), Alex Wilcox (CTO; Northeastern; ML engineering and computer networking research) and Dima Vremenko (Chief AI Officer; former Harvard Medical ML researcher, 6+ peer-reviewed papers). The team is described as "MIT and Harvard-trained researchers" — [yespress.io](https://yespress.io/inkbox-yc-s26); [Dima Vremenko LinkedIn](https://www.linkedin.com/in/dimavrem/)
- Earlier name "Vectorly": the original GitHub org was `VectorlyApp/inkbox`, and older README example links still point to `github.com/vectorlyapp/inkbox` — [GitHub VectorlyApp/inkbox](https://github.com/VectorlyApp/inkbox); [PyPI inkbox README](https://pypi.org/project/inkbox/). The legal entity "Vectorly, Inc." appears only in a search summary.
- Product timeline: `@inkbox/sdk` v0.1.0 was published 2026-03-13. The CLI first appeared 2026-03-25, and the latest version of both is 0.7.18 (2026-10-10). The Python package has about 100 releases. Shipping is very fast — [npm registry @inkbox/sdk](https://registry.npmjs.org/@inkbox/sdk); [npm registry @inkbox/cli](https://registry.npmjs.org/@inkbox/cli); [PyPI JSON](https://pypi.org/pypi/inkbox/json)
- GitHub org `inkbox-ai` has 11 public repos. The main monorepo `inkbox-ai/inkbox` ("SDK, skills, and examples...") was created 2026-03-16 and had 99 stars and 25 forks as of 2026-10-11 — [GitHub inkbox-ai/inkbox](https://github.com/inkbox-ai/inkbox)
- Customer case study: Vendo gives five agents their own mailboxes, phone lines and iMessage presence ("How Vendo runs its own team on Inkbox"). This is self-reported — [Inkbox blog](https://inkbox.ai/blog/vendo-runs-its-team-on-inkbox)
- Third-party integration: the npm package `@constal/imessage` (2026-09-29) connects a tenant-owned Inkbox identity to Constal agents as an iMessage channel. Other companies are already building on Inkbox — [npm @constal/imessage](https://www.npmjs.com/package/@constal/imessage)
- X/Twitter: @inkbox_ai, "Inkbox (YC S26)" — [X](https://x.com/inkbox_ai)
- Market context: a Foundra piece says S26 was YC's largest batch, with infra and dev tools making up more than two-fifths of it, and names Inkbox as an example of the agent "identity layer" — [Foundra](https://www.foundra.ai/key-reads/yc-s26-demo-day-agent-infrastructure-founder-strategy-2026)

### Inferences
- The founders started from 2FA and credential pain in browser agents, which explains why the vault, TOTP and the "agent signs itself up" flow are first-class features next to the messaging channels. Projects that use the vault plus email to finish a real signup or login flow match the founders' original motivation.
- With about 100 Python releases in 7 months, the API changes quickly. Pin SDK versions at the hackathon and read the current docs.

### Gaps
- No public seed round, valuation or investor list beyond YC. Tracxn and roundfunded pages surfaced, but they were unverified and a Tracxn result described an unrelated tattoo company named Inkbox.
- No user or revenue numbers.
- Could not fetch the YC Launch page body directly, so its exact copy and date are unverified.

## 2. Core technology and architecture

### Takeaway
Everything hangs off an **agent identity** with an immutable `handle`. Creating it atomically provisions a mailbox (`handle@inkboxmail.com` or a custom domain) and a tunnel (`handle.inkboxwire.com`). A phone number, a dedicated iMessage line, A2A, Slack and vault secrets are attached to it. Inbound events arrive through **HMAC-signed webhooks**, one subscription per identity covering all channels, with optional conversation context included. You can also poll with list/iterate APIs, use IMAP, or stream voice audio over a **WebSocket**. Auth uses `ApiKey_...` keys that are either admin-scoped or identity-scoped. Agents can also sign themselves up without a key, subject to a human-claim step.

### Cited Findings
**Identities and provisioning**
- `createIdentity()` "atomically provisions the mailbox AND the tunnel — both come back on the response. Phone numbers stay opt-in." Example addresses: `sales-bot@inkboxmail.com` and tunnel `sales-bot.inkboxwire.com`. The handle is fixed at creation. Deleting an identity cascades to the mailbox, tunnel and phone number and revokes scoped API keys — [npm @inkbox/sdk README](https://www.npmjs.com/package/@inkbox/sdk)
- Custom sending domains can be registered in the console. `createIdentity(handle, { sendingDomain: "mail.acme.com" })` pins a mailbox to one, and an admin can set the org default — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- Verified org domains are a separate feature from sending domains. You prove ownership of a domain with a DNS TXT record and attach it as an identity's "domain affiliation". It then appears on A2A directory entries so other agents can verify the agent belongs to example.com. Requires v0.7.12+ — [PyPI inkbox README](https://pypi.org/project/inkbox/)

**Auth and agent self-signup**
- API keys (`ApiKey_...`) come from inkbox.ai/console. The SDK resolves `apiKey`, `baseUrl` and `vaultKey` from options, then the env vars `INKBOX_API_KEY`, `INKBOX_BASE_URL` and `INKBOX_VAULT_KEY`, then `~/.inkbox/config`. The default timeout is 30 s — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- There are two key types. Admin keys can see the whole organization. Agent- or identity-scoped keys only see their own identity and discover peers through the A2A directory. Minting a scoped key: `inkbox.apiKeys.create({ label, scopedIdentityId })` — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- **Agent self-signup**: `Inkbox.signup({ humanEmail, noteToHuman, displayName?, agentHandle?, emailLocalPart?, harness?, invitationToken? })` needs no API key. It returns an API key (shown once) and an email address such as `sales-agent-a1b2c3@inkboxmail.com`. The human verifies a 6-digit code (`Inkbox.verifySignup`). "Unclaimed agents have a limited send quota and can only email the humanEmail specified at signup", and full capabilities unlock after verification or approval in the console — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- Directional contact permissions: per-identity allow/block rules for mail, phone, iMessage and A2A, each with `direction: inbound | outbound | both` and whitelist or blacklist filter modes (v0.7.3+) — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

**Email**
- `sendEmail` supports to/cc, text and HTML bodies, base64 attachments, inline `cid:` images and open tracking (`trackOpens`, giving `firstOpenedAt`/`openCount`). Threads are available via `getThread(msg.threadId)`, and there are threaded replies and reply-all. Drafts are generation-versioned with optimistic concurrency, where a 409 means `draft_generation_conflict`. Mailbox imports, full-text search, and read/unread state are supported — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk); [PyPI](https://pypi.org/project/inkbox/)
- Mailboxes have storage caps (example: 2 GiB), and a send that would exceed the cap returns HTTP 402 `StorageLimitExceededError`. **On the Free plan an Inkbox footer is appended to outgoing mail** — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- IMAP/SMTP gateway: `imap.inkboxmail.com:993` and `smtp.inkboxmail.com:465/587`. The username is the inbox address and the password is an identity-scoped API key. This lets humans open an agent's inbox in Apple Mail or Thunderbird — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

**Phone (voice and SMS/MMS)**
- `identity.provisionPhoneNumber()` provisions a local US number, and you can pass `state: "NY"`. There are two outbound voice modes:
  - **Bring your own voice stack**: `placeCall({ toNumber, clientWebsocketUrl: "wss://..." })` streams call audio to your WebSocket.
  - **Hosted Voice AI**: `mode: CallMode.HOSTED_AGENT` with a `reason`, voicemail handling (`leave_message | hang_up | ignore`), a voice catalog (`inkbox.hostedAgent.listVoices()`), saved instructions and an "authority mode" (`CONTACT_SCOPED` or `YOLO`) that controls what the voice agent may do.
  - Calls return a `rateLimit.callsRemaining` field. Transcripts are segmented per party (`local`/`remote`) and searchable, and tool invocations made by the hosted agent can be inspected — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- Incoming calls can go to a webhook (the response body controls routing), be forwarded to an E.164 number, or be auto-accepted onto a `clientWebsocketUrl` — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- **SMS limits and gotchas**:
  - Each sender number is capped at 100 recipient sends per rolling 24 h.
  - A new number needs about **10–15 minutes** for 10DLC carrier propagation (`smsStatus: "pending"`, error `409 sender_sms_pending`).
  - **Recipients must first text `START`** to a number in your org, otherwise you get `403 recipient_not_opted_in`. STOP is honored.
  - Group MMS is in beta.
  - Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

**iMessage**
- iMessage is opt-in per identity (`imessageEnabled`). There are two modes:
  1. **Shared Inkbox router**: the human must text first. They send `connect @my-agent` to a router number that you resolve at runtime with `inkbox.imessages.getTriageNumber()`.
  2. **Dedicated line**: claimed with `claimIMessageNumber: true`. It can start 1:1 and group conversations, subject to consent and rate limits.
  - Supported features: tapbacks (seven named reactions), typing indicators, read receipts, media upload, 13 send styles (e.g. CONFETTI, LASERS), threaded replies (v0.7.13+) and group chats (dedicated line only).
  - Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk); [PyPI](https://pypi.org/project/inkbox/)
- Dedicated lines come in outbound-capable and inbound-only (reply-only) variants. Voice calls can also be placed over the shared iMessage number pool (`CallOrigin.SHARED_IMESSAGE_NUMBER`). Organization-owned routers are beta and available on request — [Inkbox iMessage docs](https://inkbox.ai/docs/capabilities/imessage) (search summary); [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- A competitor (Dial) says Inkbox iMessage runs on a shared pool where the human must text first, with per-plan caps and no groups. That is partly outdated, because dedicated lines and groups are documented — [Dial vs Inkbox](https://getdial.ai/compare/dial-vs-inkbox) (competitor source)

**Inbound delivery: webhooks, polling, WebSockets, tunnels**
- **Webhooks**: one subscription is owned by an agent identity and can mix event types across channels (SDK/CLI v0.7.8+). Event types:
  - Mail: `message.received`, `message.sent`, `message.forwarded`, `message.delivered`, `message.bounced`, `message.failed`
  - SMS: `text.received`, `text.sent`, `text.delivered`, `text.delivery_failed`, `text.delivery_unconfirmed`
  - iMessage: `imessage.received`, `imessage.reaction_received`, `imessage.sent`, `imessage.delivered`, `imessage.delivery_failed`
  - Call: `call.ended`
  - A2A: `a2a.task.created`, `a2a.task.message`, `a2a.task.canceled`, `a2a.sent_task.updated`
  - Slack: `slack.dm_received`, `slack.mention_received`, `slack.thread_reply_received`
  - There are no wildcards.
  - Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk); [PyPI](https://pypi.org/project/inkbox/)
- Payloads use the envelope `{ event_type, timestamp, data }`. Signatures come in the `X-Inkbox-Signature` header and are checked with `verify_webhook(payload, headers, secret="whsec_...")`. You can add an optional bearer `authToken`, and delivery history supports replay — [PyPI](https://pypi.org/project/inkbox/)
- **Conversation context in webhooks**: `contextConfig` attaches recent history to `*.received` events, per class (`email`, `texts`, `calls`). You choose either the last N items (1–50) or the last H hours (1–168). Call transcripts are included, so **a single inbound text can arrive with the person's recent emails and call transcripts already attached**. This is very useful for building agents across several channels — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- **Tunnels**: `connect(inkbox, { name, forwardTo: "http://127.0.0.1:8080" })` exposes a local process at `https://{name}.inkboxwire.com` over outbound HTTP/2. No open port is needed, which works like ngrok for receiving webhooks on a laptop. The TypeScript data plane is Node-only, and Python is supported too — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk); [PyPI](https://pypi.org/project/inkbox/)
- Polling is also possible: `iterEmails`, `iterUnreadEmails`, `listTexts({isRead:false})`, `listIMessages` and A2A task lists. Fetching a single message by id with an API key marks it read on the server — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

**Vault, 2FA, Slack, Companion mode**
- The encrypted vault stores logins, API keys, key pairs, SSH keys and TOTP secrets. It is unlocked with `vaultKey`, and access control is per identity — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- Slack: an identity can get its own Slack app installed in a workspace and can send, read, react and upload files. Sends require idempotency keys — [PyPI](https://pypi.org/project/inkbox/)
- **Companion mode** (off by default): an agent joins an existing human group conversation (mail, SMS/iMessage, Slack) when an allowed trusted sender asks it to. It then loads the full prior history with `companion.load_initialization(...)` before replying — [PyPI](https://pypi.org/project/inkbox/); [npm @inkbox/cli](https://www.npmjs.com/package/@inkbox/cli)

### Inferences
- The **webhook context feature combined with one identity-wide subscription** is the cleanest way to build a single agent "brain" that receives events from every channel, with no session-stitching code of your own.
- At a 36-hour hackathon, the hard constraints are SMS 10DLC propagation (about 10–15 minutes), the START opt-in, and iMessage on the shared router (the human texts first). Plan demos around them. Provision numbers early, have judges text START or `connect @handle`, or use email, A2A and iMessage shared mode, which have no carrier delay.

### Gaps
- Exact API rate limits for email and the REST API overall were not found. Only the SMS cap (100 per day per number), voice `callsRemaining`, and the plan-dependent quota for unclaimed agents are documented.
- The REST base URL was not stated explicitly. The A2A endpoints sit on `https://inkbox.ai/a2a/...`.
- Attachment size limits were not found (Slack uploads are limited to 10 MiB).

## 3. Documentation, SDKs, CLI, MCP, GitHub, with real code

### Takeaway
Docs are at inkbox.ai/docs and the console at inkbox.ai/console. Official SDKs: TypeScript `@inkbox/sdk` (Node ≥22), Python `inkbox` (≥3.11), a Rust crate `inkbox`, and CLI `@inkbox/cli`, all at v0.7.18. Inkbox also ships agent-harness plugins (Claude Code, Codex, OpenCode, OpenClaw, Hermes, DeepSeek Harness) and reportedly a remote MCP server listed in Anthropic's connector directory.

### Cited Findings
- Docs pages found:
  - [Introduction](https://inkbox.ai/docs/get-started/introduction)
  - [Quickstart](https://inkbox.ai/docs/get-started/quickstart)
  - [Support agent tutorial](https://inkbox.ai/docs/get-started/support-agent)
  - [Python skill](https://inkbox.ai/docs/skills/python)
  - [iMessage API](https://inkbox.ai/docs/api/imessage)
  - [iMessage capability](https://inkbox.ai/docs/capabilities/imessage)
  - [Phone](https://inkbox.ai/docs/capabilities/phone)
  - [Mail clients](https://inkbox.ai/docs/capabilities/email/mail-clients)
  - [A2A API](https://inkbox.ai/docs/api/a2a)
  - [A2A protocol](https://inkbox.ai/docs/api/a2a/protocol)
  - [A2A agent card](https://inkbox.ai/docs/api/a2a/agent-card)
  - [A2A auth](https://inkbox.ai/docs/api/a2a/authentication)
  - [A2A directory](https://inkbox.ai/docs/api/a2a/directory)
  - [A2A contact rules](https://inkbox.ai/docs/api/a2a/contact-rules)
  - [Verified domains](https://inkbox.ai/docs/capabilities/verified-domains)
  - [Pricing](https://inkbox.ai/pricing)
- Install: `npm install @inkbox/sdk` (Node ≥ 22), `pip install inkbox` (Python ≥ 3.11), and `npm i -g @inkbox/cli` or `npx @inkbox/cli` — [npm SDK](https://www.npmjs.com/package/@inkbox/sdk); [PyPI](https://pypi.org/project/inkbox/); [npm CLI](https://www.npmjs.com/package/@inkbox/cli). The Rust crate is at [docs.rs/inkbox](https://docs.rs/inkbox)
- GitHub repos (inkbox-ai org):
  - `inkbox` (monorepo, 99★)
  - `hermes-agent-plugin` (40★)
  - `iphone-harness` (Appium/XCUITest iPhone control, 30★)
  - `claude-code-plugin` (19★)
  - `openclaw-plugin`
  - `codex-plugin`
  - `opencode-plugin`
  - `deepseek-harness-plugin`
  - `inkbox-quickstart-python` and `inkbox-quickstart-typescript` (both archived as of 2026-10)
  - Source: [GitHub search org:inkbox-ai](https://github.com/inkbox-ai). The Claude Code plugin is described as "Give your Claude Code agent its own Inkbox identity... Talk to it from anywhere." — [claude-code-plugin](https://github.com/inkbox-ai/claude-code-plugin)
- Hermes Agent (Nous Research) lists Inkbox in its plugin catalog — [Hermes plugin catalog](https://hermes-agent.nousresearch.com/docs/plugins/inkbox)
- MCP: a third-party listing describes an Inkbox remote MCP server with **59 tools**. It uses a single OAuth scope, `inkbox.full_service`, and a Claude-specific endpoint that leaves out call placement. It says the server is listed as a partner in Anthropic's Connectors Directory and gives the endpoint as `https://inbox.ai/mcp/anthropic`, though the listing text elsewhere says `inkbox.ai/mcp/anthropic`, so the URL is likely a typo — [Agentman listing](https://agentman.ai/agentskills/connections/mcp-server/inkbox) (secondary, not verified against Inkbox docs)

**Representative code (from the official v0.7.18 READMEs)**

Create an identity, phone number, email and call (TypeScript):
```ts
import { Inkbox } from "@inkbox/sdk";
const inkbox = await new Inkbox({ apiKey: process.env.INKBOX_API_KEY!, vaultKey: process.env.INKBOX_VAULT_KEY }).ready();
const identity = await inkbox.createIdentity("support-bot", { displayName: "Support Bot", imessageEnabled: true });
const phone = await identity.provisionPhoneNumber();           // local US number
await identity.sendEmail({ to: ["customer@example.com"], subject: "Your order has shipped", bodyText: "Tracking: 1Z999..." });
await identity.placeCall({ toNumber: "+18005559999", clientWebsocketUrl: "wss://my-app.com/voice" });
for await (const m of identity.iterUnreadEmails()) console.log(m.subject, m.threadId);
```
Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

Agent self-signup (no API key):
```ts
const r = await Inkbox.signup({ humanEmail: "john@example.com", noteToHuman: "Hey John, this is your sales bot!", agentHandle: "sales-agent", harness: "claude-code" });
// r.apiKey (shown once), r.emailAddress e.g. sales-agent-a1b2c3@inkboxmail.com
await Inkbox.verifySignup(r.apiKey, { verificationCode: "483921" });
```
Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

SMS and iMessage:
```ts
await identity.sendText({ to: "+15551234567", text: "Hello from Inkbox" });           // recipient must have texted START
const router = await inkbox.imessages.getTriageNumber();                                 // human texts router.connectCommand e.g. "connect @my-agent"
const convos = await identity.listIMessageConversations({ limit: 20 });
await identity.sendIMessage({ conversationId: convos[0].id, text: "On it — give me two minutes." });
await identity.sendIMessageTyping(convos[0].id);
```
Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

Hosted voice agent call:
```ts
import { CallMode, OnVoicemail } from "@inkbox/sdk";
await identity.placeCall({ toNumber: "+15551234567", mode: CallMode.HOSTED_AGENT,
  reason: "Coordinate the appointment and send confirmations.", onVoicemail: OnVoicemail.LEAVE_MESSAGE });
```
Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

A single webhook for all channels, plus a receiver (Python):
```ts
await inkbox.webhooks.subscriptions.create({ agentIdentityId: identity.id, url: "https://example.com/hook",
  eventTypes: ["message.received","text.received","imessage.received","call.ended","a2a.task.created"],
  contextConfig: { email: { mode: "count", count: 10 }, texts: { mode: "window", hours: 24 } } });
```
```python
from inkbox import verify_webhook
@app.post("/hooks/mail")
async def hook(request: Request):
    raw = await request.body()
    if not verify_webhook(payload=raw, headers=request.headers, secret="whsec_..."):
        raise HTTPException(403)
    evt = json.loads(raw)   # {event_type, timestamp, data}
```
Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk); [PyPI](https://pypi.org/project/inkbox/)

A local webhook endpoint without ngrok:
```ts
import { connect } from "@inkbox/sdk/tunnels/connect";
const l = await connect(inkbox, { name: "my-app", forwardTo: "http://127.0.0.1:8080" }); // l.publicUrl -> https://my-app.inkboxwire.com
```
Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

A2A (CLI and SDK):
```bash
inkbox a2a enable -i researcher
inkbox a2a skills set -i researcher --file skills.json
inkbox a2a rules add -i coordinator --handle researcher --action allow --direction outbound
inkbox a2a rules add -i researcher --handle coordinator --action allow --direction inbound
inkbox a2a call https://inkbox.ai/a2a/researcher/card -i coordinator --text "Review the findings"
inkbox a2a reply <task-id> -i researcher --ask --text "Which quarter?"     # input-required
inkbox a2a reply <task-id> -i researcher --complete --text "Done."
```
```ts
const client = await identity.a2aClient();
const target = await client.fetchCard("https://example.test/a2a/researcher/card");
await client.send(target, { text: "Review the updated findings", contextId: "context-uuid" });
```
Source: [npm @inkbox/cli](https://www.npmjs.com/package/@inkbox/cli); [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)

### Inferences
- For the hackathon, the fastest path is the CLI plus the Claude Code or Codex plugin, so your coding agent has its own Inkbox identity, then a small webhook server running behind an Inkbox tunnel.
- The SDK surface is large (Slack, Companion, vault, domains). Judges at a sponsor track usually reward depth of integration, so use several of these features where they fit.

### Gaps
- Could not read the MCP server's official docs page or confirm its URL.
- Could not fetch the Quickstart page directly to check console onboarding steps.

## 4. Comparison with competitors (AgentMail, Primitive, Twilio, Vapi, Bland, Sendblue, Dial)

### Takeaway
Inkbox's difference is **breadth under one identity**: email, voice and SMS, iMessage, A2A, Slack, a tunnel and a vault, sharing one contact-permission model and one webhook stream. Most competitors cover a single channel: AgentMail and Primitive do email, Twilio does telephony and SMS, Vapi and Bland do voice AI, and Sendblue does iMessage. The trade-off is depth and maturity in each channel.

### Cited Findings
- **AgentMail**:
  - Free: 3 inboxes and 3,000 emails (100/day). Paid: $20 for 10 inboxes and 10,000 emails, up to $200 for 150 inboxes (15k/day).
  - Inkbox comparison: free 3 identities, $30 for 10 identities plus 1 phone number, $200 for 100 identities.
  - Per-unit cost at the top tier: Inkbox $2.00 per identity, AgentMail $1.33.
  - Positioning: AgentMail makes the inbox the core primitive, with threading, webhooks, WebSockets and "Pods" for per-tenant isolation.
  - Source: [deadsimple.email pricing comparison, Sept 2026](https://deadsimple.email/compare/pricing.html) (third party); [AgentMail blog](https://www.agentmail.to/blog/best-email-api-for-ai-agents-2026) (vendor)
- **Primitive (primitive.dev)**, also a sponsor:
  - Email infrastructure for agents. Send and receive with one HTTP call, a managed `*.primitive.email` address, and SPF/DKIM/DMARC, bounces and IP reputation handled for you.
  - Tooling: an MCP server at primitive.dev/mcp, Node/Python/Go SDKs and a CLI.
  - A "chat" feature sends a message to another agent or a human and waits for the threaded reply. LinkedIn lists the company as "YC P26".
  - Source: [Primitive on Lava docs](https://www.lava.so/docs/gateway/providers/primitive.md); [LinkedIn](https://linkedin.com/company/primitivedotdev) (search summaries)
- **Sendblue** (iMessage): its own blog cites roughly $29/month for an AI Agent plan, while its API page and third parties say $100 per line per month. Outbound lines are quote-only, and it advertises SOC 2 Type II and HIPAA — [Sendblue API](https://www.sendblue.com/api); [Sendblue pricing blog](https://www.sendblue.com/blog/imessage-api-pricing-comparison); [Blooio (competitor)](https://blooio.com/blog/best-imessage-api-2026)
- **Dial** publishes a "Dial vs Inkbox" page comparing them as "AI agent identity stacks" and calls Inkbox iMessage shared-pool/human-first with no groups (competitor framing, partly superseded) — [Dial](https://getdial.ai/compare/dial-vs-inkbox)
- Pricing claims vary across third parties. One comparison listed $10 and $25 tiers for Inkbox that do not match the official page — [search summary of inkbox.ai/pricing and third parties](https://inkbox.ai/pricing)

### Inferences
- Twilio, Vapi, Bland: no fresh sources were gathered in this pass, so this is background knowledge, unverified for Oct 2026. Twilio is a raw CPaaS (numbers, SMS, voice) with no agent identity, inbox or A2A layer. Vapi and Bland are voice-agent platforms that can bring their own numbers. Inkbox's hosted-voice mode plus the `clientWebsocketUrl` streaming mode overlaps with them, but Inkbox focuses on identity and channels, not voice quality and latency tuning. A strong hackathon design could use Inkbox for identity and number and stream audio to your own voice model.
- Against AgentMail and Primitive, Inkbox costs more per mailbox but is the only one of the three bundling phone, iMessage and A2A. Pitch your project around **cross-channel continuity**, which the single-channel products cannot show.
- Possible judging angle: because Primitive is also a sponsor with an email and agent-chat feature, an Inkbox-track entry should lean on what Primitive lacks (iMessage, voice, A2A agent cards and directory) rather than plain email.

### Gaps
- No independent head-to-head benchmark (deliverability, latency) of Inkbox against AgentMail or Primitive was found.
- Current Vapi, Bland and Twilio pricing and features were not researched in this pass.

## 5. What is A2A, and how does Inkbox use it?

### Takeaway
A2A (Agent2Agent) is an open protocol that Google launched in April 2025 for agents to discover each other through **Agent Cards** and exchange **tasks** made of messages and parts (JSON-RPC, gRPC or HTTP+JSON). It was donated to the Linux Foundation, and v1.0 shipped in roughly March–April 2026. Inkbox makes **every claimed identity an A2A endpoint by default**. It hosts the identity's Agent Card and JSON-RPC endpoint, and adds discovery directories (organization and public), bilateral allow/block rules, invitations, task/context history, webhooks and verified-domain affiliation.

### Cited Findings
- A2A was donated to the Linux Foundation in June 2025. v1.0, the first stable spec, is reported as March 2026 (one source gives a March 12, 2026 freeze; another says April 2026). On 2026-08-17 it became a hosted project of the Agentic AI Foundation (AAIF), under the Linux Foundation. Dates differ slightly across secondary sources — [AAIF builder's guide](https://aaif.io/blog/a2a-v1-0-a-builder-s-guide-part-1-discovery-tasks-and-clients); [waxell.ai](https://waxell.ai/blog/a2a-agentic-ai-foundation-agent-identity); [Tyk](https://tyk.io/learning-center/a2a-protocol-architecture-and-technical-specification/)
- The Agent Card is published at a well-known path, `/.well-known/agent-card.json`, which replaced `agent.json` in v0.3 (2025-07-30) and was IANA-registered in v1.0. The card gives the name, skills, capabilities and transport endpoints. v1.0 added signed agent cards — [specification.website](https://specification.website/spec/agent-readiness/a2a-agent-cards/); [Tyk](https://tyk.io/learning-center/a2a-protocol-architecture-and-technical-specification/)
- Inkbox endpoints:
  - Agent Card: `GET https://inkbox.ai/a2a/{agent_handle}/card`, no credential needed, with an alias at `/a2a/{agent_handle}/.well-known/agent-card.json`.
  - Protocol: `POST https://inkbox.ai/a2a/{agent_handle}`, which needs the **calling** agent's agent-scoped key. Admin keys are rejected.
  - "A2A is on by default and requires a claimed identity."
  - Source: [Inkbox A2A docs](https://inkbox.ai/docs/api/a2a); [Agent Card](https://inkbox.ai/docs/api/a2a/agent-card); [Protocol](https://inkbox.ai/docs/api/a2a/protocol) (via search summaries)
- Inkbox A2A features:
  - Organization and public directories with search by handle, description, skills or verified domain (`inkbox.a2a.publicDirectory({ q })`)
  - `a2aSetPubliclyDiscoverable` and `a2aSetAllowPublicEgress`
  - Custom advertised skills (`inkbox a2a skills set --file skills.json`)
  - Task and message history with full-text search
  - Shared "contexts" that are auto-named and can be renamed
  - Worker replies that ask for more input (`--ask`) or complete the task (`--complete`)
  - Webhooks: `a2a.task.created`, `a2a.task.message`, `a2a.task.canceled`, `a2a.sent_task.updated`
  - The client never sends the Inkbox API key to external card or RPC origins
  - Source: [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk); [npm @inkbox/cli](https://www.npmjs.com/package/@inkbox/cli)
- Admission: same-org and public discovery may imply admission. Private cross-org calls must pass the requester's **outbound** policy and the worker's **inbound** policy, and explicit blocks always win — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- **A2A invitations**: an admin creates an invitation linking an external agent to a set of peers (`peerAgentHandles: ["support","billing"]`). The token format is `a2ai_` plus 43 characters. An outside agent can sign up with `invitationToken` and be connected immediately, which works as onboarding for agents from other companies — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk)
- External A2A agents can be called (`client.fetchCard(url)`), for example agents exposed through Google ADK. Cross-endpoint context reuse is guaranteed only between Inkbox identities — [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk); [ADK A2A quickstart](https://adk.dev/a2a/quickstart-exposing/)

### Inferences
- Inkbox gives an agent with no server an A2A presence (card, endpoint and inbox for tasks) plus human channels **under the same identity**. A strong demo shows an A2A task arriving and the agent then escalating to a human by iMessage or phone, with the human reply flowing back into the A2A task (`input-required`, then `completed`).
- Verified-domain affiliation on A2A cards is a trust and identity feature that few hackathon teams will use. It is a cheap way to stand out.

### Gaps
- Not confirmed: whether Inkbox cards are signed (a v1.0 feature), and which A2A spec version Inkbox implements.

## 6. Project ideas likely to score well in the Inkbox track

### Takeaway
The track rewards projects where agents have a **persistent identity** and talk **to humans and to each other**. The best entries will use 3–4 channels under one or more identities. They should show cross-channel continuity (webhook `contextConfig`), human-in-the-loop over iMessage or phone, agent-to-agent delegation over A2A with policies and a directory, and ideally trust features (verified domain, vault/2FA, contact rules).

### Cited Findings
- The track wording comes from the assignment brief. Inkbox's own plugin copy is "Install Inkbox plugin to get access to email, phone, iMessage and an A2A channel." — [inkbox.ai](https://inkbox.ai/) (search summary)
- Primitives worth combining (all documented in [npm @inkbox/sdk](https://www.npmjs.com/package/@inkbox/sdk) / [PyPI](https://pypi.org/project/inkbox/)):
  - Hosted voice agent with transcripts and tool logs
  - Webhook context that bundles emails, texts and call transcripts
  - A2A directory and invitations
  - Companion mode for joining human group threads
  - Vault with TOTP
  - Agent self-signup with a human claim step
  - IMAP access for humans

### Inferences (idea list, not sourced claims)
1. **Agent "chief of staff" that negotiates with other agents.** Your agent has an Inkbox identity (email, iMessage, phone). To book something, it searches the A2A public directory for vendor agents (e.g. a restaurant or venue agent built by your team as a second identity), negotiates through an A2A task, and texts you on iMessage for approval (`input-required`). If the vendor has no agent, it falls back to a hosted-voice phone call and confirms by email. This shows all four channels, both human↔agent and agent↔agent.
2. **Agent-to-agent marketplace / hiring board.** Each worker agent publishes skills on its card. A coordinator uses `a2a.publicDirectory` with verified domains to pick workers and delegate. A human can follow everything by email (IMAP) or iMessage. Use A2A invitations to onboard an outside team's agent live on stage.
3. **Group-chat companion.** Using Companion mode, a family or roommate iMessage group (dedicated line) adds the agent. It loads the history and then coordinates chores or bills. It can email landlords, phone stores, and delegate to a "payments agent" over A2A.
4. **Self-onboarding agent.** An agent calls `Inkbox.signup` and its human claims it. It then signs up for third-party SaaS using its own email, stores the credentials and TOTP in the vault, handles 2FA from email or SMS, and reports by iMessage. This addresses the founders' original pain point (2FA and confirmation emails).
5. **Customer-support swarm with unified memory.** One identity receives email, SMS, iMessage and calls. `contextConfig` supplies cross-channel history, specialist agents (billing, tech) get A2A tasks, and callers can switch mid-conversation from a phone call to iMessage without repeating themselves.
6. **Agent that keeps commitments.** It reads its inbox for promises and deadlines and follows up through the right channel (email, then text, then call), escalating by A2A to a human's own agent.

Hackathon execution tips:
- Provision phone numbers on day 1 morning (10DLC delay of about 10–15 minutes).
- Ask judges to text START or `connect @handle` at the start of the demo.
- Use tunnels for webhooks.
- Use the Free tier (3 identities) for development, keeping in mind the email footer and the absence of a phone number on Free. You will likely need the Developer tier ($30) for a phone number, which prize credits or sponsor booth credits might cover. Check at the event.
- Show the **transcript plus the A2A task log plus the email thread** side by side in the demo UI.

### Gaps
- Judging criteria beyond the one-sentence track description are unknown.
- No information on whether Inkbox gives hackathon participants free credits or upgraded plans (likely, but unconfirmed).

## Appendix: pricing (official page via search summary; verify on-site)
- **Free $0**: 3 agent identities, each with an email inbox. No dedicated phone number. Shared iMessage access with up to 2,000 iMessages per month. A footer is appended to outgoing mail. — [Inkbox pricing](https://inkbox.ai/pricing); [npm SDK README re footer](https://www.npmjs.com/package/@inkbox/sdk)
- **Developer $30/mo**: 10 identities. One dedicated VoIP number with 300 SMS/MMS and 30 call minutes per month (US/Canada). — [Inkbox pricing](https://inkbox.ai/pricing)
- **Startup $200/mo**: 100 identities, 9 dedicated VoIP numbers, 1 dedicated iMessage number, 3 GiB of storage per mailbox. — [Inkbox pricing](https://inkbox.ai/pricing)
- **Enterprise**: custom pricing. — [Inkbox pricing](https://inkbox.ai/pricing)
- Paid-only features: custom email signatures. Customer-managed 10DLC lifts the SMS cap. — [PyPI](https://pypi.org/project/inkbox/); [npm SDK](https://www.npmjs.com/package/@inkbox/sdk)
- Gap: overage rates and the cost of extra numbers or iMessage lines were not found.
