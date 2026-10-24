# web scraping api free: what 5,000 trial credits and 1,000 a month actually buy, and when upgrading makes sense

Searching for a free web scraping API usually gets you a table of headline numbers: 1,000 credits here, 10,000 credits there. The number that actually matters is how many requests your target site costs, because most providers charge multipliers for JavaScript rendering, premium proxies, and hard-to-scrape domains — and the multiplier can shrink a "free 1,000 credits" down to 100 renders or 40 Google searches.

This guide walks through what free tiers really cover, using ScraperAPI as the main example (7-day trial with 5,000 credits, then a permanent free plan of 1,000 credits a month), how its credit system works across paid plans, and how its free offer stacks up against ScrapingAnt, ZenRows, Firecrawl, Tavily, Apify, and others. All ScraperAPI numbers come from its official pricing page and documentation; competitor figures are from their published 2026 tiers.

**Quick picks**

- Just validating a pipeline: sign up for the trial — 5,000 credits for 7 days, no credit card — and after it expires you keep a permanent free plan with 1,000 credits/month and 5 concurrent connections.
- Running real volume: Hobby is the entry point at $49/mo, or $44.10/mo billed annually (10% off), for 100,000 credits.
- 👉 [Start the free ScraperAPI trial and test your actual target sites](https://www.scraperapi.com/?fp_ref=coupons)

## What ScraperAPI's free tier actually includes

You get two free stages: a 7-day trial with 5,000 credits, then a permanent free plan with 1,000 credits per month. Neither requires a credit card.

The feature list on both stages matches the paid plans: JavaScript rendering, premium residential and mobile IPs, CAPTCHA and anti-bot detection, JSON auto-parsing, custom header and session support, automatic retries, unlimited bandwidth, and a 99.9% uptime guarantee. You also get up to 5 concurrent connections.

One exclusion matters more than the rest: the free tier doesn't get ultra-premium proxies. The docs are explicit that `ultra_premium=true` is a paid-plans-only parameter — and it's expensive even there, at 30 credits per request, or 75 with rendering. If your target site sits behind serious bot protection, the paid plans are the ones with the full bypass arsenal.

A practical note from evaluation guides worth borrowing: 50–100 requests across your specific target sites is enough to validate a scraping API. Test 3–5 different pages per target, including pagination, and you'll know whether the free tier is enough for you. On that scale, 5,000 trial credits is genuinely generous — the trial exists precisely for this.

## The credit system, and why "1,000 free credits" can mean 40 requests

Credits are not requests. ScraperAPI prices pages by difficulty, and the official documentation spells out the base rates:

> A standard page costs 1 credit. Amazon (and other e-commerce sites like Walmart and eBay) costs 5, Google and Bing — including all their subdomains — cost 25, and LinkedIn costs 30.

Then the parameters stack on top. Per the docs, per request: `premium=true` adds 10 credits, `render=true` (JavaScript rendering) adds 10, `premium` + `render` together costs 25, and `screenshot=true` adds 10. Meanwhile several parameters you'd expect to pay for are free: `country_code`, `session_number`, `device_type`, `wait_for_selector`, `output_format`, and `autoparse` all cost nothing extra. Sites behind bot protection add 10 credits per request when the bypass succeeds — this covers Cloudflare (including Turnstile), Datadome, PerimeterX/Human, and Akamai.

Run the math on the free 1,000 monthly credits and the headline number changes fast:

- Standard static pages: 1,000 requests
- Amazon or Walmart product pages: 200
- Google or Bing searches: 40
- LinkedIn: 33
- JavaScript-rendered pages: 100
- Anti-bot bypass requests: roughly 91

One caveat on the rendering number: some 2026 third-party reviews cite a lower 5-credit JS rate specifically on the free tier, which conflicts with the current documentation's 10-credit `render=true` price. The docs are the more authoritative and current source, but you don't have to take anyone's word for it — every response includes a `sa-credit-cost` header showing exactly what a request cost. Check it on your first rendered request and you'll know.

Two tools keep this from surprising you at scale. The dashboard's Domain Multiplier (there's also an API endpoint at `api.scraperapi.com/account/urlcost`) shows the exact credit cost of any URL before you spend anything on it, including with rendering enabled. And you can set a `max_cost` per scrape so a single request can't blow through a limit. Using both before pointing the API at Google, LinkedIn, or protected sites is the difference between a plan that works and one that silently burns out in an afternoon.

On billing fairness, the docs are unusually clear: **only successful requests (HTTP 200 and 404) get charged, plus requests you cancel yourself within 70 seconds.** Timeouts, blocks, and other failures don't cost you credits. For a free tier you're using to test a flaky target site, that matters — a 60% failure rate doesn't eat your balance.

This multiplier math is the piece most free-tier roundups skip. They list 1,000 credits next to 10,000 credits and move on, without telling you what a single request on your actual target costs. The table below fills that in.

## Every plan, with current pricing

All tiers from the official pricing page, monthly and annual (annual saves 10%):

| Plan | Credits/mo | Concurrency | Geo-targeting | Monthly / Annual | Buy |
| --- | --- | --- | --- | --- | --- |
| Free | 1,000 | 5 | — | $0 | [ Try 5,000 free credits](https://www.scraperapi.com/?fp_ref=coupons) |
| Hobby | 100,000 | 20 | US & EU only | $49 / $44.10 | [ Get Hobby](https://www.scraperapi.com/?fp_ref=coupons) |
| Startup | 1,000,000 | 50 | US & EU only | $149 / $134.10 | [ Get Startup](https://www.scraperapi.com/?fp_ref=coupons) |
| Business | 3,000,000 | 100 | Country-level | $299 / $269.10 | [ Get Business](https://www.scraperapi.com/?fp_ref=coupons) |
| Scaling | 5,000,000 | 200 | Country-level | $475 / $427.50 | [ Get Scaling](https://www.scraperapi.com/?fp_ref=coupons) |
| Professional | 10,500,000 | 300 | Country-level | $975 / $877.50 | [ Get Professional](https://www.scraperapi.com/?fp_ref=coupons) |
| Advanced | 21,500,000 | 500 | Country-level | $1,975 / $1,777.50 | [ Get Advanced](https://www.scraperapi.com/?fp_ref=coupons) |
| Enterprise | 22,000,000+ (custom) | 500+ | Country-level | Contact sales | [ Request custom pricing](https://www.scraperapi.com/?fp_ref=coupons) |

A few things the table can't show:

- **Hobby and Startup only support US & EU geo-targeting.** Country-level targeting starts at Business. If your targets are in Asia-Pacific or Latin America, $299/mo is your real entry point, and Hobby's lower price is irrelevant to you.
- **Hobby keeps only 30 days of analytics history.** Business and up get unlimited history in the dashboard.
- **Concurrency limits return a 429, not a queue.** Requests over the limit are declined and you're not charged for them, which is fairer than services that throttle or bill anyway.
- **Running out of credits doesn't have to stop your job.** By default scraping pauses until credits renew. Hobby through Professional offer opt-in auto-upgrade (moves you to the next plan when credits run out). Scaling and above can use pay-as-you-go at a fixed per-credit rate, capped at a monthly spend you set. Annual plans — and any plan, via the dashboard — can renew early for a fresh batch of credits.

Check the live numbers before committing — third-party reviewers note that entry-tier pricing has shifted before, and one 2026 review tracked the Startup plan moving from $99 to $149. The official page is the source of truth: 👉 [compare all ScraperAPI plans and current prices](https://www.scraperapi.com/?fp_ref=coupons)

## How the free offer compares to other scraping APIs

Here's what competitors publish as of their 2026 free tiers. Information only — check each vendor's site for current terms.

| Service | Free tier | Renews monthly | Multipliers / limits |
| --- | --- | --- | --- |
| ScraperAPI | 5,000-credit trial (7 days) + 1,000/mo | Yes | Google 25×, LinkedIn 30×, anti-bot +10, render +10; no ultra-premium proxies on free |
| ScrapingAnt | 10,000 credits/mo, no card | Yes | 1 credit datacenter, 125 credits residential+browser → ~80 protected pages |
| ZenRows | 5,000 credits/mo, no card | Yes | No multipliers at all — 5,000 credits is 5,000 requests |
| Firecrawl | 1,000 credits/mo, no card | Yes | +4 for JSON extraction, modifiers stack → 1,000 credits ≈ 200 extracted pages |
| Tavily | 1,000 credits/mo, no card | Yes | 1 credit basic search, 2 advanced; no charge for failed extractions |
| Bright Data | 5,000 requests/mo | Yes | Per-request, pay as you go |
| Decodo | 2,000 requests/mo | Yes | 1,000 with JavaScript |
| Apify | $5 platform usage/mo | Yes | Metered by platform usage |
| Scrapfly | 1,000 credits | Sources differ: one 2026 comparison lists it as monthly, another as one-time with SMS verification | +5 JS rendering, +25 residential |
| Jina AI Reader | Keyless, ~20 req/min | n/a | Effectively unmetered for light use |

Two observations worth your attention.

First, the biggest headline number isn't the best free tier. ScrapingAnt's 10,000 credits is the largest on the board, but a browser request over residential proxies costs 125 credits, so the realistic figure for protected pages is about 80 requests. ZenRows' 5,000 credits, with no multipliers anywhere, is arguably the more honest free tier for mixed workloads.

Second, generous free tiers sometimes belong to weak performers. An independent benchmark cited in a 2026 roundup measured ScrapingAnt at around 45% success and called it unusable for production regardless of price. Scrapeway's testing put ZenRows at roughly 51% success against an industry average near 58% — well below the vendor's own reported 99.93% — and ZenRows dropped to 15% in one August 2026 test run. Neither figure is settled; treat vendor-reported success rates with skepticism in both directions.

Where does ScraperAPI fit in this picture? Its permanent 1,000 credits/month sits mid-pack, and the search-engine multipliers are steep. What offsets that is a combination the others don't quite match: a 5,000-credit no-card trial with paid-tier features (so you can measure 200 Google requests before deciding anything), documented no-charge-for-failures billing, and per-request cost transparency via the `sa-credit-cost` header and the URL cost estimator. If your priority is the largest recurring free allowance for easy static pages, the competitors above are worth checking. If your priority is a trial that reflects the real paid product on hard targets, this structure favors you.

## Choosing a plan by workload, not by credit count

Match the plan to what you're actually scraping:

- **Validating whether a target site is scrapeable at all** → the 7-day trial. Run your real targets, check the URL cost estimator first, and don't decide anything until the trial tells you the per-request cost.
- **A personal script or hobby project under ~1,000 standard pages a month** → stay on the free plan indefinitely. Upgrading buys you nothing you need.
- **Amazon or e-commerce monitoring** → Hobby at $49/mo. 100,000 credits at the 5-credit e-commerce rate is roughly 20,000 product pages per month.
- **SERP or search-engine data** → budget carefully. At 25 credits per Google request, Hobby's 100,000 credits is 4,000 searches. If you need more, the jump to Startup (1M credits, $149) covers 40,000.
- **Targets outside the US and EU** → Business at $299/mo. No lower plan supports country-level geo-targeting, so this is your floor regardless of volume.
- **Continuous production jobs that can't pause** → Scaling ($475/mo) or above, where pay-as-you-go keeps requests flowing past the credit limit instead of stopping mid-job.
- **Scraping millions of URLs asynchronously, needing a dedicated support team and Slack channel** → Enterprise, custom-priced at 22M+ credits.

One more wrinkle: the main API endpoint returns raw HTML you parse yourself. ScraperAPI also sells dedicated structured endpoints — Amazon Product, Amazon Search, Amazon Offers, Google Search, Google Shopping, Google News, Google Jobs, Walmart Product and Search — that return ready-made JSON for those specific sites. If your use case matches one of those exactly, check whether the endpoint covers it before writing your own parser.

## FAQ

**Is the free plan really free forever?**
Yes. After the 7-day trial (5,000 credits), you keep a permanent free plan with 1,000 credits per month and 5 concurrent connections. No credit card is required at signup. The main limitation is the missing ultra-premium proxy pool, not a time limit.

**How many Google searches can I do with 1,000 free credits?**
40, at 25 credits per Google or Bing request including their subdomains. LinkedIn costs 30, e-commerce sites cost 5, and standard pages cost 1. With JavaScript rendering enabled, each request adds 10 credits per the current docs.

**Do failed requests cost credits?**
No. The documentation states that only successful requests — HTTP 200 and 404 status codes — are billed, plus requests you cancel within 70 seconds before completion. Anything else doesn't touch your balance.

**What happens when I hit the concurrency or credit limit?**
Exceeding concurrency returns a 429 and declines the request without charging you. Running out of credits pauses scraping until renewal by default; Hobby and above can enable auto-upgrade, and Scaling and above can enable pay-as-you-go with a monthly cap you set.

**Will free-tier performance match what I get on a paid plan?**
Not perfectly. Evaluation guides note that some providers route free-tier traffic through lower-priority proxy pools or apply stricter throttling. If your free-tier success rates are borderline, that's a signal to test a handful of paid requests before committing — production performance is typically better.

**Is there a promo code?**
A code called START10 appears in third-party reviews, but it isn't confirmed on the official pricing page as of writing, so don't count on it. The 10% annual discount is the reliably published one.

## Before you sign up

The decision comes down to one number: the credit cost of your actual target site with your actual parameters, times your monthly volume. Run it through the URL cost estimator during the trial and most of the plan confusion disappears. Concretely:

- Standard pages, under 1,000/month → free plan, done.
- Amazon at scale → Hobby, and annual billing knocks it to $44.10/mo.
- Google/Bing/LinkedIn data or non-US/EU targets → the free tier's math won't hold; price it out on Hobby vs. Business based on whether you need country-level geo.
- Heavy bot protection → the trial is the honest test, since bypasses cost +10 credits per request and ultra-premium proxies are paid-only.

One last practical tip: after your first few requests, glance at the `sa-credit-cost` response header. It tells you exactly what each request consumed, which turns every estimate in this article into a measurement for your specific setup. The trial costs nothing and asks for no card, so there's no reason to guess when you can measure: 👉 [open your free ScraperAPI account and check your real per-request costs](https://www.scraperapi.com/?fp_ref=coupons)
