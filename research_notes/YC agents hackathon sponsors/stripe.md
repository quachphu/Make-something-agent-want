# Stripe for AI Agents (Agentic Commerce): Products, Developer Tooling, and How to Win the Stripe Track

Research date: 2026-10-11. Method note: direct fetches of stripe.com / docs.stripe.com / news sites failed in this environment (DNS/proxy block), so findings come from (a) a fresh clone of the official GitHub repo `github.com/stripe/agent-toolkit` (now titled "Stripe AI", latest commit 2026-10-11) read in full where relevant, and (b) web-search result summaries that quote Stripe docs/blog pages. Items supported only by search snippets or secondary sources are flagged. Status labels (GA / public preview / private preview) are given where a source states them.

Track brief (from assignment): "Build an agent that can safely participate in the economy: buy products, provision services, manage business spending, or pay for the resources it needs to complete a task... useful, creative, end-to-end experiences that give users clear control over what their agents can do and spend." Prizes: Stripe credits $3k/$2k/$1k; $500 credits for all participants; Stripe Atlas fee waived for winners.

## Q1. Stripe Agent Toolkit and the official Stripe MCP server: what exists and what tools are exposed?

### Takeaway
The agent toolkit repo has been reorganized into "Stripe AI" (github.com/stripe/agent-toolkit, also referenced as github.com/stripe/ai). The Python (`stripe-agent-toolkit` 0.7.0) and TypeScript (`@stripe/agent-toolkit` 0.9.1) toolkits are now thin clients of the remote MCP server at `https://mcp.stripe.com`; which tools an agent gets is set by the permissions on a Restricted API Key (rk_*), not by code. A local MCP server (`npx -y @stripe/mcp`, v0.3.3) still exists. The tool set is about Stripe account operations (customers, products/prices, payment links, invoices, subscriptions, refunds, disputes, balance, docs search), so it suits seller/business-ops agents, not an agent spending money as a buyer.

### Cited Findings
- Repo README (title "Stripe AI") calls itself "the one-stop shop for building AI-powered products and businesses on top of Stripe". It lists `@stripe/ai-sdk` (Vercel AI SDK billing) and `@stripe/token-meter` (native OpenAI/Anthropic/Gemini SDK metering), the remote MCP server at `https://mcp.stripe.com` ("secure MCP client access via OAuth", docs https://docs.stripe.com/mcp), and Agent Skills — [stripe/agent-toolkit README, commit 735b42d, 2026-10-11](https://github.com/stripe/agent-toolkit)
- Official plugin install commands: Claude Code `claude plugin install stripe@claude-plugins-official`; Codex `codex plugin add stripe@openai-curated`; Cursor `/add-plugin stripe`; Grok Build `grok plugin install stripe --trust`; manual skills `npx skills add https://docs.stripe.com` — [README](https://github.com/stripe/agent-toolkit)
- The Claude plugin's MCP config is just `{"mcpServers":{"stripe":{"type":"http","url":"https://mcp.stripe.com"}}}` — [providers/claude/plugin/.mcp.json](https://github.com/stripe/agent-toolkit/tree/main/providers/claude/plugin)
- The toolkit "enables popular agent frameworks including MCP, OpenAI's Agent SDK, LangChain, CrewAI, and Vercel's AI SDK to integrate with Stripe APIs through function calling... not exhaustive of the entire Stripe API" — [tools/README.md](https://github.com/stripe/agent-toolkit/blob/main/tools/README.md)
- Breaking change v0.6.x to v0.7.0+ (Python): initialization is now async and "connects to `mcp.stripe.com`"; "If the server is unreachable, initialization fails with no fallback"; tool names changed to snake_case (`create_customer`, `list_customers`, `create_payment_link`); the `configuration.actions` option was removed, and "Tool permissions are now controlled entirely by your Restricted API Key (RAK) on the server side"; only the `context` option (e.g. `account: "acct_123"` for Connect) remains — [tools/python/MIGRATION.md](https://github.com/stripe/agent-toolkit/blob/main/tools/python/MIGRATION.md)
- Versions in repo: Python `stripe-agent-toolkit` 0.7.0 (Python 3.11+), TypeScript `@stripe/agent-toolkit` 0.9.1 (Node 18+, subpaths `/langchain`, `/ai-sdk`, `/openai`, `/modelcontextprotocol`), local MCP `@stripe/mcp` 0.3.3. Python examples cover OpenAI Agents SDK (incl. a customer-support agent), LangChain, CrewAI, and Strands — [repo tree](https://github.com/stripe/agent-toolkit/tree/main/tools)
- Python setup snippet (official):
  ```python
  from agents import Agent
  from stripe_agent_toolkit.openai.toolkit import create_stripe_agent_toolkit

  async def main():
      toolkit = await create_stripe_agent_toolkit(secret_key="rk_test_...")  # RAK scopes = tool list
      agent = Agent(name="Stripe Agent",
                    instructions="You are an expert at integrating with Stripe",
                    tools=toolkit.get_tools())
      ...
      await toolkit.close()
  ```
  TypeScript: `import { createStripeAgentToolkit } from "@stripe/agent-toolkit/langchain"; const toolkit = await createStripeAgentToolkit({ secretKey: process.env.STRIPE_SECRET_KEY!, configuration: {} }); const tools = toolkit.getTools();` — [tools/README.md](https://github.com/stripe/agent-toolkit/blob/main/tools/README.md)
- Local MCP: `npx -y @stripe/mcp --api-key=YOUR_STRIPE_SECRET_KEY [--stripe-account=acct_...]`; Claude Desktop config `{"mcpServers":{"stripe":{"command":"npx","args":["-y","@stripe/mcp","--api-key=STRIPE_SECRET_KEY"]}}}`; Docker image `mcp/stripe`; Gemini CLI `gemini extensions install https://github.com/stripe/ai` then `/mcp auth stripe` (OAuth). "Tool permissions are controlled by your Restricted API Key (RAK)" — [tools/modelcontextprotocol/README.md](https://github.com/stripe/agent-toolkit/blob/main/tools/modelcontextprotocol/README.md)
- Tool names referenced in the repo's code/tests: `create_customer`, `list_customers`, `create_product`, `list_products`, `create_price`, `list_prices`, `create_payment_link`, `create_invoice`, `create_invoice_item`, `finalize_invoice`, `list_invoices`, `list_payment_intents`, `retrieve_balance`, `create_refund`, `list_disputes`, `update_dispute`, `create_coupon`, `list_coupons`, `list_subscriptions`, `update_subscription`, `cancel_subscription`, `get_stripe_account_info`, `search_stripe_documentation` (alias `search_documentation`) — [repo grep, stripe/agent-toolkit](https://github.com/stripe/agent-toolkit). The authoritative live list is at https://docs.stripe.com/mcp#tools, and third-party listings say the live list is "supplied by the server when your MCP client connects" (one counts 23 tools) — [MCPBundles](https://app.mcpbundles.com/skills/stripe-mcp); [lagrowthmachine](https://lagrowthmachine.com/stripe-mcp/)
- Remote MCP uses OAuth (Dynamic Client Registration per a third-party source); restricted keys with narrow scopes are recommended — [flowhunt](https://www.flowhunt.io/mcp-servers/stripe/)
- New agent skills shipped in the repo, synced from `docs.stripe.com/.well-known/skills`: `stripe-best-practices`, `stripe-docs`, `stripe-projects`, `stripe-directory`, `stripe-pay`, `stripe-apps`, `connect-recommend`, `upgrade-stripe`, `metronome`. "LLM readable Docs (append .md to the end of any Docs)" — [skills/README.md](https://github.com/stripe/agent-toolkit/tree/main/skills)
- Token billing: `@stripe/token-meter` (`createTokenMeter(STRIPE_API_KEY); meter.trackUsage(response, 'cus_xxx')` for OpenAI/Anthropic/Gemini, including streaming) and `@stripe/ai-sdk` (a Vercel AI SDK provider that routes through Stripe's LLM proxy `llm.stripe.com`, e.g. `stripe('openai/gpt-5')`, plus a `/meter` wrapper). Both say: "currently only available to organizations participating in the Billing for LLM Tokens **Private Preview**" (request at https://docs.stripe.com/billing/token-billing) — [llm/token-meter/README.md](https://github.com/stripe/agent-toolkit/blob/main/llm/token-meter/README.md); [llm/ai-sdk/README.md](https://github.com/stripe/agent-toolkit/blob/main/llm/ai-sdk/README.md)

### Inferences
- For a hackathon, the remote MCP + RAK is the quickest way to give an agent Stripe "business ops" powers (invoice a customer, refund, make a payment link). Scoping the RAK *is* the safety story for this path and is worth showing in a demo ("this agent's key can only create refunds under X").
- Because toolkit v0.7+ requires network access to mcp.stripe.com, teams should test connectivity on the venue network early.
- Older blog tutorials using `StripeAgentToolkit(... configuration={"actions": ...})` are outdated. Use the async `create_stripe_agent_toolkit` API.
- The Billing for LLM Tokens packages are private preview. Hackathon teams should plan to use standard Billing Meters (meter events) unless they get access.

### Gaps
- I could not fetch docs.stripe.com/mcp to confirm the full current tool list (e.g. whether Issuing, SPT or Checkout tools are exposed). Teams should connect a client and list tools.
- I could not confirm whether `stripe-agent-toolkit` still supports the OpenAI Agents SDK, CrewAI and LangChain as first-class Python integrations beyond the examples folder (the subpackages exist in the repo).

## Q2. Agentic commerce products: ACP / Instant Checkout, SPTs, Agentic Commerce Suite, MPP/Tempo, x402/stablecoins, Link for agents, Issuing for agents, Order Intents, token billing, Projects/Directory/`stripe pay`. What exists as of Oct 2026, and what is in preview?

### Takeaway
Stripe has a full stack across both sides of a transaction. On the buyer/agent side: Shared Payment Tokens (public preview, API version `2026-09-30.preview`), Issuing for agents (private preview), the Link wallet for agents (launched 2026-04-29, per-purchase approval), `stripe pay` with Stripe Directory, and Stripe Projects (agents provision and pay for SaaS). On the seller side: the Agentic Commerce Suite, ACP (with OpenAI), UCP (Google), and machine payments via MPP (Stripe+Tempo, launched 2026-03-18) and x402 (USDC on Base, preview since Feb 2026), all landing in PaymentIntents. The status of ChatGPT Instant Checkout is disputed: one secondary source says it was retired in March 2026.

### Cited Findings
**Timeline / announcements**
- Sessions 2025 (May 6–8, 2025): Stripe announced an **Order Intents API** ("create a commerce agent in seconds"; a third-party write-up says the merchant hands the agent a URL and a budget and the agent completes the purchase), previewed Issuing-based programs and a no-code Issuing rules engine, and said "agents can now earn, store, and spend funds" — [Stripe blog: top product updates Sessions 2025](https://stripe.com/blog/top-product-updates-sessions-2025); [IDC note](https://my.idc.com/getdoc.jsp?containerId=US53602225)
- Sept 2025: Stripe powers **Instant Checkout in ChatGPT** and released the **Agentic Commerce Protocol (ACP)**, co-developed with OpenAI (open source, Apache 2.0, date-versioned) — [Stripe newsroom](https://stripe.com/newsroom/news/stripe-openai-instant-checkout); [OpenAI "Buy it in ChatGPT"](https://openai.com/index/buy-it-in-chatgpt/); [OpenAI Delegated Payment Spec](https://developers.openai.com/commerce/specs/payment)
- Stripe's launch post describes SPTs as tokens that "can be scoped to a business, limited by time or amount, and revoked at any time" — [Stripe blog: Introducing our agentic commerce solutions](https://stripe.com/blog/introducing-our-agentic-commerce-solutions)
- Jan 2026: commercetools "Stripe Agentic Commerce Suite module" entered early access (2026-01-16) — [commercetools release note](https://docs.commercetools.com/api/releases/2026-01-16-stripe-agentic-commerce-suite-module-is-now-supported-in-early-access). Google announced the Universal Commerce Protocol (UCP) in Jan 2026 — [Opascope](https://opascope.com/insights/ai-shopping-assistant-guide-2026-agentic-commerce-protocols/)
- Feb 2026: Stripe added **x402** machine payments with USDC on Base (preview). A developer creates a PaymentIntent, Stripe generates a deposit address, the agent pays, and funds settle into the Stripe balance — [The Block](https://www.theblock.co/post/389352/stripe-adds-x402-integration-usdc-agent-payments); [Coinbase Dev on X](https://x.com/CoinbaseDev/status/2021358906480656621). Secondary sources: US businesses only, 1.5% per charge, charges as low as 0.01 USDC; network list (Base vs. Solana/Tempo) conflicts across sources — [stablecoininsider](https://stablecoininsider.org/how-to-accept-x402-usdc-payments-on-stripe/); [wavect](https://wavect.io/blog/x402-payments-comparison-2026/)
- Feb 2026: OpenAI expanded Instant Checkout; Stripe remained the "foundational partner" — [Digital Commerce 360, 2026-02-16](https://www.digitalcommerce360.com/2026/02/16/openai-expands-agentic-commerce-push/). **Conflict:** one secondary blog says OpenAI **retired Instant Checkout in March 2026** and moved checkout back to merchant environments — [Hypotenuse AI](https://www.hypotenuse.ai/blog/chatgpts-instant-checkout-the-next-phase-of-agentic-commerce). Not confirmed by OpenAI or Stripe in sources I could reach.
- 2026-03-18: **Machine Payments Protocol (MPP)**, co-authored by Stripe and Tempo, launched alongside Tempo mainnet. A server returns HTTP 402 with a payment challenge; the client pays, retries with a credential, and gets the resource plus a receipt. It supports Tempo stablecoins, cards via Stripe, and Bitcoin via Lightning. Docs: https://docs.stripe.com/payments/machine/mpp; spec at mpp.dev; "sign up for early access" — [Stripe on X](https://x.com/stripe/status/2034257912973963374); [Tempo docs: Machine Payments](https://docs.tempo.xyz/learn/tempo/machine-payments); [The Defiant](https://thedefiant.io/news/blockchains/tempo-launches-mainnet-unveils-machine-payments-protocol-with-stripe). MPP "sessions" let an agent authorize a spending limit upfront and stream micropayments (per The Defiant).
- 2026-04-29 **Sessions 2026**: Agentic Commerce Suite (upload a catalog, choose which AI agents may sell your products from the Dashboard; a platform preview for connected accounts); Meta native checkout in Facebook ads; Google AI Mode/Gemini via UCP ("soon"); MPP acceptance through the Payment Intents API in stablecoins and in fiat (cards, Klarna, Affirm via SPTs); Link agent wallet; Issuing for agents previewed ("programmatically issue single-use virtual cards"). Microsoft Copilot Checkout is powered by Stripe — [Stripe blog: Everything we announced at Sessions 2026](https://stripe.com/blog/everything-we-announced-at-sessions-2026) (via search summary); [Rankly summary](https://rankly.substack.com/p/stripes-recent-announcements-on-agentic)

**Shared Payment Tokens (SPT): public preview**
- The agent mints an SPT with `POST /v1/shared_payment/issued_tokens` from the customer's saved PaymentMethod and the seller's Stripe profile, with `usage_limits[currency]`, `usage_limits[max_amount]`, `usage_limits[expires_at]`. Examples use the header `Stripe-Version: 2026-09-30.preview`. A SharedPaymentIssuedToken "is a limited-use reference to a PaymentMethod", can be revoked, and has status `active | requires_action | deactivated` — [Stripe docs: SPT concepts (agent view)](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens?agent-seller=agent); [API: Issued Tokens](https://docs.stripe.com/api/shared-payment/issued-token)
- Seller side: a read-only SharedPaymentGrantedToken (`GET /v1/shared_payment/granted_tokens/:id`) used with a PaymentIntent. It has `usage_limits{currency, expires_at, max_amount}` and `usage_details.amount_captured`. Test helper: `POST /v1/test_helpers/shared_payment/granted_tokens` — [API: Granted Token object](https://docs.stripe.com/api/shared-payment/granted-token/object); [SPT concepts](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens)
- Representative agent-side call, reconstructed from the docs' described parameters (preview; verify exact field names):
  ```bash
  curl https://api.stripe.com/v1/shared_payment/issued_tokens \
    -u "$STRIPE_SECRET_KEY:" -H "Stripe-Version: 2026-09-30.preview" \
    -d payment_method=pm_123 \
    -d "seller_details[network_business_profile]=profile_abc" \
    -d "usage_limits[currency]=usd" -d "usage_limits[max_amount]=2500" \
    -d "usage_limits[expires_at]=1760000000"
  # seller then: PaymentIntent with shared_payment_granted_token=spt_...
  ```
  — [SPT concepts](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens?agent-seller=agent)
- A developer reports undocumented shapes, e.g. `requires_action` returned with HTTP 200 for cards needing authentication (one developer's observations) — [DEV Community](https://dev.to/hkarekar403/stripe-shared-payment-tokens-five-wire-shapes-i-only-found-by-shipping-3ch3)

**Issuing for agents: private preview**
- Docs at https://docs.stripe.com/issuing/agents. Lets businesses and agent platforms issue (single-use) virtual cards for agent purchases, with spend limits, merchant-category controls, freezing, and real-time authorization. Labeled private preview — [Stripe Issuing for agents docs (search summary)](https://docs.stripe.com/issuing/agents); [stripe.com/issuing](https://stripe.com/issuing)
- "Pay with Issuing in agentic payment flows": creating a PaymentMethod from an Issuing card (`card[issuing_card]`) requires private preview access ("without access, we reject `card[issuing_card]` as an unknown parameter"). Spend controls "remain in effect for every authorization on the card, including payments funded through an SPT" — [docs.stripe.com/issuing/agents/programmatic-checkout](https://docs.stripe.com/issuing/agents/programmatic-checkout)
- Pricing: one secondary source lists $0.10 per virtual card plus 0.2% + $0.20 per transaction (unverified) — [useproxy.ai](https://www.useproxy.ai/blog/virtual-card-apis-compared-2026)
- A competitor's view: Stripe provides card rails, but builders must add intent tracking, agent-scoped policies, and approval workflows themselves (vendor opinion) — [Crossmint](https://www.crossmint.com/learn/agent-card-payments-compared)

**Link wallet for agents: launched 2026-04-29**
- The user connects Link to an agent via OAuth. Each spend request goes to the user for review in the Link app or web. Only after approval does the agent receive a one-time-use card or an SPT, and it never sees the underlying card. The wallet is built on Issuing for agents. Stripe says user-set spending limits and unattended actions are planned, not shipped — [TechCrunch, 2026-04-30](https://techcrunch.com/2026/04/30/stripe-link-digital-wallet-ai-agents-shopping/); [Stripe on X](https://x.com/stripe/status/2049529444092838116) ("you approve every purchase"); [agenticplug](https://agenticplug.ai/blog/what-is-stripe-link-wallet-for-ai-agents)
- Unverified: caps of $5,000 per request/day and $20,000 per month with a 10-minute approval window — [AlphaSignal](https://alphasignal.ai/news/stripe-s-link-wallet-lets-ai-agents-buy-things-on-your-behalf). A leaked screen (Aug 2026) reportedly shows budgets, recurring purchases, and pre-approved future purchases (unconfirmed) — [Runtimewire](https://runtimewire.com/article/stripe-link-balance-ai-agents-unattended-spending). Official info: link.com/agents.

**Stripe Projects, Stripe Directory, `stripe pay`: agents provision and pay for services**
- Stripe Projects (projects.dev) is a CLI (`stripe plugin install projects`; `stripe projects catalog|search|init|add|status|env --json`) that "lets you or your agents provision multiple services, generate and store credentials, and manage usage and billing". Providers include Neon, Supabase, Vercel, PostHog, Clerk, PlanetScale, Twilio, Hugging Face, Databricks, Cloudflare. Status is reported variously as developer preview or open beta (Sessions 2026); a $100/month default cap is mentioned by one third-party source — [Stripe blog: Projects adds new agents/providers/controls](https://stripe.com/blog/stripe-projects-adds-new-agents-providers-developer-controls); [Neon](https://neon.com/blog/neon-works-with-stripe-projects-for-agentic-provisioning); [Databricks](https://www.databricks.com/blog/databricks-and-stripe-projects-infrastructure-built-agents); [skills/stripe-projects/SKILL.md](https://github.com/stripe/agent-toolkit/blob/main/skills/stripe-projects/SKILL.md)
- **Stripe Directory** is described as "the discovery and engagement layer for agents that need an external business, merchant, nonprofit, provider, platform, API, or software service". It resolves verified recipients and "their documented payment or engagement path", ranked by "agent-readiness". Docs: https://docs.stripe.com/directory.md#agents — [skills/stripe-directory/SKILL.md](https://github.com/stripe/agent-toolkit/blob/main/skills/stripe-directory/SKILL.md). Web search found no news coverage, which suggests it is very recent.
- **`stripe pay`** (Stripe CLI) sends B2B money to another Stripe business by Stripe Profile handle (`@recipient`) or network ID. It requires a sender Stripe Profile and a funded financial account (Money Management / Global Payouts), and it reports fee and timing before confirmation. The official skill's safety rules: show the exact command, dry-run with `--agent`/`--json` first, do not pass `-y/--yes` until the user confirms, never guess amounts or recipients. Docs: https://docs.stripe.com/cli/pay — [skills/stripe-pay/SKILL.md](https://github.com/stripe/agent-toolkit/blob/main/skills/stripe-pay/SKILL.md)

**Usage-based billing for agents**
- Billing for LLM Tokens (`@stripe/token-meter`, `@stripe/ai-sdk`, `llm.stripe.com` proxy): **private preview** — [token-meter README](https://github.com/stripe/agent-toolkit/blob/main/llm/token-meter/README.md). Repo also ships a `metronome` skill (Stripe acquired Metronome; usage billing) — [skills dir](https://github.com/stripe/agent-toolkit/tree/main/skills)

### Inferences
- Map for builders:
  - The agent *buys* from merchants: SPT (public preview) or Link agent wallet (consumer approval per purchase), or Issuing virtual cards (private preview).
  - The agent *provisions services*: Stripe Projects.
  - The agent *pays another business*: `stripe pay` + Directory.
  - The agent *pays per API call*: MPP/x402 (HTTP 402).
  - The agent *gets paid / bills users for compute*: Billing meters / token billing, Agentic Commerce Suite, ACP.
- Preview gating matters at a hackathon. Standard Issuing in test mode (cards with `spending_controls`, the authorization webhook, test-helper authorizations) is the most reliable way to demo "agent with a card plus guardrails" without special access. SPT test helpers exist for the seller side. Plan on Stripe mentors for preview access (Issuing-for-agents `card[issuing_card]`, MPP early access, token billing).
- Do not center a project on ChatGPT Instant Checkout, given the unconfirmed report of its retirement. ACP/UCP/MPP as protocols are safer bets.

### Gaps
- Could not verify OpenAI's own statement on Instant Checkout status after March 2026.
- Could not confirm whether the Order Intents API (Sessions 2025) still exists as a separate product or was folded into the Agentic Commerce Suite / Issuing for agents. No 2026 source mentions it.
- Could not confirm current MPP availability (early access vs. GA), x402 supported networks, or exact Projects spend caps from primary docs.
- No primary source found for a "Stripe + Coinbase" partnership beyond x402-on-Base coverage.

## Q3. How to enforce user control over agent spending, with code, and how to win the Stripe track

### Takeaway
Stripe gives five layers of control. (1) A Restricted API Key scopes which tools and endpoints an agent can call. (2) SPT `usage_limits` (max_amount, currency, expires_at, revocable, seller-scoped) cap a single purchase. (3) Issuing `spending_controls` (amount per interval, allowed/blocked MCCs) apply to every authorization, including SPT-funded ones. (4) The real-time `issuing_authorization.request` webhook lets your own policy engine or a human approve or decline within about 2 seconds. (5) Human-in-the-loop approval, as in the Link agent wallet and the `stripe pay` confirm step. A winning project demos these layers end to end with a clear user-facing control panel.

### Cited Findings
- RAKs are the permission boundary for the toolkit and MCP: "Tool availability is determined by the permissions you configure on the restricted key" — [tools/README.md](https://github.com/stripe/agent-toolkit/blob/main/tools/README.md); restricted-key docs: https://docs.stripe.com/keys#create-restricted-api-keys
- SPTs are scoped to a seller, limited by amount/time, and revocable — [Stripe blog](https://stripe.com/blog/introducing-our-agentic-commerce-solutions); [API: Issued Token](https://docs.stripe.com/api/shared-payment/issued-token)
- Issuing spend controls stay in force for every authorization, including SPT-funded payments — [Pay with Issuing in agentic flows](https://docs.stripe.com/issuing/agents/programmatic-checkout)
- Real-time authorizations: respond to the `issuing_authorization.request` webhook within 2 seconds with HTTP 200 and JSON `{"approved": true|false}` (optionally `amount` for a partial hold when `is_amount_controllable` is true), or call the approve/decline API. On timeout, Stripe falls back to the account's timeout setting. With no webhook configured, Stripe approves authorizations it has no reason to decline. `issuing_authorization.created` follows. Insufficient Issuing balance means a decline with no event — [Stripe docs: Issuing real-time authorizations](https://docs.stripe.com/issuing/controls/real-time-authorizations)
- Issuing rules engine (no-code authorization rules in the Dashboard) since Sessions 2025 — [Stripe Sessions 2025 blog](https://stripe.com/blog/top-product-updates-sessions-2025)
- Link agent wallet: explicit per-purchase consumer approval before a credential is released — [TechCrunch](https://techcrunch.com/2026/04/30/stripe-link-digital-wallet-ai-agents-shopping/)
- The `stripe pay` skill encodes a human-approval pattern: preview (`--agent`/`--json`), show the exact command, confirm, then `--yes` — [skills/stripe-pay/SKILL.md](https://github.com/stripe/agent-toolkit/blob/main/skills/stripe-pay/SKILL.md)
- Market view: most agent purchases still require human approval as of mid-2026 — [CoinGecko: Top Agent Cards 2026](https://www.coingecko.com/learn/top-agent-cards-ai-payments)

**Representative Issuing code.** This is the long-standing public Issuing API (cardholder, card, and `spending_controls` fields: `spending_limits[{amount, interval: per_authorization|daily|weekly|monthly|yearly|all_time, categories}]`, `allowed_categories`, `blocked_categories`, plus `allowed_merchant_countries` / `blocked_merchant_countries`). It is drawn from Stripe's standard Issuing docs (https://docs.stripe.com/issuing/controls/spending-controls). Verify against current docs.
```python
import stripe
stripe.api_key = "sk_test_..."
holder = stripe.issuing.Cardholder.create(
    type="individual", name="Shopping Agent for Jane", email="jane@example.com",
    billing={"address": {"line1": "1 Main St", "city": "SF", "state": "CA",
                          "postal_code": "94111", "country": "US"}})
card = stripe.issuing.Card.create(
    cardholder=holder.id, currency="usd", type="virtual", status="active",
    spending_controls={
        "spending_limits": [{"amount": 5000, "interval": "per_authorization"},
                            {"amount": 20000, "interval": "monthly"}],
        "allowed_categories": ["computer_software_stores", "digital_goods_applications"],
    },
    metadata={"agent_id": "agent_42", "task_id": "task_9"})
# Simulate a purchase in test mode:
stripe.issuing.Authorization.TestHelpers.create(card=card.id, amount=1999,
    merchant_data={"category": "computer_software_stores", "name": "Acme SaaS"})
```
```python
# Real-time policy/human gate (Flask): must answer in < 2s
@app.post("/webhooks/issuing")
def issuing_hook():
    event = stripe.Webhook.construct_event(request.data, request.headers["Stripe-Signature"], WHSEC)
    if event.type == "issuing_authorization.request":
        auth = event.data.object
        ok = policy_allows(auth.card.metadata["agent_id"], auth.amount, auth.merchant_data)
        return jsonify({"approved": ok}), 200, {"Stripe-Version": "2025-..."}  # per docs
    return "", 200
```
(Webhook response shape per [real-time authorizations docs](https://docs.stripe.com/issuing/controls/real-time-authorizations). The header detail is an assumption; check the docs.)

### Inferences: project ideas that would score well
The judging language rewards (a) usefulness, (b) creativity, (c) end-to-end (the agent actually completes a transaction), and (d) clear user control over what the agent can do and spend. Strong patterns:
1. **"Agent allowance" control plane plus a doing-agent.** A dashboard where a user (or finance lead) creates an agent, gets a scoped RAK and a virtual Issuing card with spending_controls and MCC allowlist, and sets policies: auto-approve under $X, ask me via push/Slack above it, block categories. The real-time authorization webhook enforces policy live. Demo: the agent buys a domain or SaaS seat, gets declined on an out-of-policy merchant, then requests approval and succeeds. Hits "manage business spending" and "user control".
2. **Task agent that pays for its own resources.** An agent that, for a task like "build me a landing page with a DB", uses Stripe Projects to provision Neon/Vercel/Clerk, pays per call for data APIs via MPP/x402 (HTTP 402), and shows a live budget meter against a user-set task budget. A kill switch revokes the SPT or freezes the card. Hits "provision services" and "pay for resources".
3. **Shopping/procurement agent with SPT checkout.** The agent researches products, builds a cart, and asks the user to approve one purchase. On approval it mints an SPT with `max_amount` equal to the cart total and a short `expires_at`, and checks out on a demo merchant built with the Agentic Commerce Suite/ACP seller side (both sides in test mode). Shows "buy products" end to end with cryptographically bounded spend.
4. **B2B accounts-payable agent.** It reads invoices from email, resolves vendors via Stripe Directory, and drafts `stripe pay` transfers with a dry-run preview and human confirmation. Includes an audit log and per-vendor limits.
5. **Metered agent product.** An agent-as-a-service that bills end users per task or token via Billing meters (or token billing if access is granted), with user-visible spend caps. Weaker fit unless combined with the agent spending money itself.

Differentiators judges will likely notice: a visible policy UI; an approval UX (push/SMS/Slack); an immutable audit trail tying each authorization to agent, task and reasoning (card/SPT `metadata`); a demo of a *declined* out-of-policy attempt; revocation/kill switch; test-mode end-to-end flow including the seller side; least-privilege RAKs. Use test mode and test helpers so the live demo is deterministic.

### Gaps
- Could not verify the exact current Issuing `spending_controls` enum values or the webhook response header requirements from live docs. The snippets above rely on long-standing API knowledge and should be checked.
- Could not confirm whether Issuing test mode is available to all new sandbox accounts without an application (historically US-only and gated for live mode).
- The hackathon's own judging rubric, Stripe mentor availability, and whether preview features (Issuing for agents, MPP, token billing) will be unlocked for participants are unknown. Ask Stripe staff at kickoff.
