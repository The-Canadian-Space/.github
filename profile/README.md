# The Canadian Space

Aerospace news for Canada — fully automated, end-to-end.

## What We Do

The Canadian Space is an automated newsroom that discovers, curates, and publishes aerospace stories relevant to Canada. We run seven specialized blog workflows covering daily aerospace news, NASA missions, SpaceX launches, commercial space ventures, Blue Origin, Rocket Lab, and Canadian satellite data. Each post is researched, edited by AI, fact-checked, and published to WordPress with full cost tracking and SEO optimization—all without manual intervention.

This is a real production system running on a VPS in France, pulling news from 40+ sources, processing through custom Python tools and n8n orchestration, and serving readers at [thecanadian.space](https://thecanadian.space).

## The Repos

**Public**

- **tcs-images** — 100+ images used across published posts. Stays under our original Godimas101 account to avoid breaking URLs on WordPress.
- **tcs-scripts** — n8n workflow node definitions, API cost trackers, and utility scripts for TCS operations.
- **tcs-tools** — Python utilities: article scraper, cost calculations, and data processing helpers.

**Private** (workflow management and future projects)

- **tcs-workflows** — Automated backups of all 39 n8n workflows. Contains the current 14 TCS workflows plus 25 unrelated personal automation.
- **tcs-arcade** — *Planned*. Browser games coming to thecanadian.space.
- **tcs-webpage** — *Planned*. Rebuild of the site frontend (currently WordPress).

## Currently Shipping

**7 Active Blog Workflows**
- Daily Broadcast, NASA Overview, SpaceX Report, Commercial Space, Bright Blue Origin, Rocket Lab Roundup, Canada From Orbit

**Recent Additions**
- **Editor LLM** — Claude Haiku processes every post through SEO rules and fact-checking safeguards before publication. Fallback to Grok 3 on API errors.
- **Cost Tracking** — Real-time tracking of LLM API spend (Anthropic, Google, xAI) with weekly digest reports.
- **Social Posts** — Automated engagement on X and LinkedIn.

## The Stack

- **Orchestration**: n8n (39 workflows total)
- **Python**: Article scraper, cost processors, API helpers
- **CMS**: WordPress (Newfold hosting)
- **LLMs**: Anthropic Claude (Haiku primary, Opus for heavy analysis), Google Gemini, xAI Grok via OpenRouter
- **Infrastructure**: OVH VPS2 (51.195.43.156) — Docker, Redis, Caddy reverse proxy
- **SEO**: Rank Math WordPress plugin

## What's Next

- **tcs-webpage rebuild** — Move away from WordPress to a custom frontend (early design phase).
- **tcs-arcade launch** — Browser games embedded on the site.
- **Fact-checker LLM pass** — Automated verification of claims using extended-thinking models.
- **New news sources** — Expanding coverage to international aerospace news.

## Visit

Read our latest posts at [thecanadian.space](https://thecanadian.space).

## Contributing

This project is currently a solo venture, but we're building with future collaborators in mind. If you're interested in contributing to the newsroom, the Python tools, or the n8n workflows, reach out. Check **AGENTS.md** in any repo for technical onboarding.

---

*The Canadian Space is a personal project and portfolio piece built to demonstrate full-stack automation, AI integration, and infrastructure management. All code, workflows, and infrastructure are by Chris Carpenter (Godimas101).*