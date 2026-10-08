# Agent Strategy & Business Context (Plan v2)

Working plan for the Market Scout project, updated Oct 2026 after a review. The source of truth is the "Plan v2" tab of the Market Scout Google Doc; this file mirrors it for coding sessions. Where this file and older notes disagree, this file wins.

## Situation

- The owner is starting from zero: no store, no listings, no domain yet.
- Goal: a small set of agents that find what to sell and help sell it, building toward passive income.
- The research agent is the core of the system. Most of the value is in spotting trends.

## Key decisions

- **One research agent, not three.** The Market Scout, Trend Validator and Review Miner ship as a single research agent.
  - Scans market trends across Amazon, Etsy and Shopify-based stores.
  - Validates trends (Google Trends, TikTok, Pinterest Trends, Reddit) and separates real trends from one-week spikes, with a confidence score per pick.
  - Mines 1–3 star reviews of top sellers for recurring complaints that point to better products.
  - Produces a weekly report on trends and best-performing products.
  - Runs as a human-operated Claude Code (or Codex) session on the strongest model available at the time. It is not a fully autonomous background bot.
- **Stores launch by hand.** Day one store setup is manual. No Storefront Publisher yet.
- **Own website instead of Shopify.** The site is built with Claude and takes payment through Stripe Checkout. Needs a domain and a Stripe account with a bank account for payouts. Stripe in Canada accepts individuals and sole proprietors, so incorporating is optional at the start.
- **Listing Writer is the first creation piece**, fed by the Keyword/SEO Agent. It comes before the Digital Product and Print-on-Demand Design agents.
- **Mockups use a low-cost model**, starting with Gemini Flash-Lite. Note: Flash-Lite reads images but does not generate them, so generating mockups needs an image-generation model. Still an open question.
- **Margins decide print-on-demand.** Compare print-on-demand against holding inventory before building the Print-on-Demand Design Agent.
- **Competitor Watcher is deferred** until after Layer 4.
- **Orchestrator baseline:** https://github.com/mimurchison/claude-chief-of-staff (Claude Code config, slash commands and YAML files that produce a morning briefing). Adapt it to read agent reports instead of email and calendar.

## Agent lineup and timing

- **Now:** research agent (Scout + Trend Validator + Review Miner).
- **Next:** Listing Writer, Keyword/SEO Agent, Sourcing & Margin Agent (runs the print-on-demand vs inventory comparison), Mockup Agent.
- **Later:** Digital Product Agent, Print-on-Demand Design Agent (only if the margins work), Layer 3 distribution (Affiliate Content, Pinterest/Social, Email), Layer 4 operations (Pricing, Customer Service Drafter, Profit Tracker).
- **After Layer 4:** Competitor Watcher, Orchestrator, Storefront Publisher.

## Build order

1. Research agent, run as a human-operated session on the top model.
2. Manual store launch: domain, website, Stripe Checkout.
3. Listing Writer, with the Keyword/SEO Agent feeding it.
4. Margin comparison: print-on-demand vs inventory.
5. Mockup Agent on a low-cost model.
6. Layers 3 and 4, then the Competitor Watcher and the Orchestrator.

## Margin model (print-on-demand vs inventory)

- **Print-on-demand, per sale:** price − base product cost − shipping − payment fees.
- **Inventory, per sale:** price − unit cost − freight − storage − fulfillment − payment fees, plus the cash tied up in unsold stock.
- **Both:** compare margin per sale against the marketing cost to win one sale. A product works when margin per sale is higher than that cost.
- A lower margin can be acceptable for print-on-demand because it needs no upfront stock and scales without limit. The key metric is revenue against marketing spend.

## Rules for the code

- **Data access: official or licensed sources only.** Etsy Open API, Amazon's affiliate product API, Keepa, Jungle Scout-style data providers, and third-party store trackers for Shopify-based stores.
  - Do not scrape Amazon or any platform against its terms.
  - Do not create throwaway accounts or credentials to get around platform blocks.
  - This protects the accounts the business will later sell and earn affiliate income through.
- **Secrets go in environment variables**, never in the code or committed files. Examples: `KEEPA_API_KEY`, `ETSY_API_KEY`, `STRIPE_SECRET_KEY`, `GEMINI_API_KEY`. In cloud sessions, set them in the cloud environment's settings. Keep a `.env.example` listing variable names without values.
- **Human in the loop.** Agents draft and queue; the owner approves before anything is published, sent or charged.
- **AI content rules.** Platforms (Etsy especially) require clear disclosure of AI-generated products and penalize mass-listing near-identical AI output. Favor fewer, curated products.

## Market reality

- "AI agents for passive income on Etsy" is a crowded idea in 2026, and low-effort digital products are saturated.
- The edge comes from a narrow niche, good research (review mining, trend validation), curation over volume, and building a brand and email list.
- Selling the research itself (a paid weekly or monthly trend report) is a possible revenue stream, since many people are attempting this.

## Open questions

- Which domain name?
- Sign up for Stripe as an individual, or incorporate first?
- Does the mockup step need to create images, or only check them?
- Which niche does the research agent focus on first?
