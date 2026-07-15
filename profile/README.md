<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=blur&height=220&color=0:0B1021,30:0EA5E9,65:2563EB,100:7C3AED&text=The%20Canadian%20Space&fontColor=ffffff&fontSize=48&fontAlignY=38&desc=Automated%20aerospace%20newsroom%20%C2%B7%20AI%20%C2%B7%20n8n%20%C2%B7%20end-to-end&descAlignY=63&descSize=18&animation=fadeIn" />
</p>

<p align="center">
  <a href="https://thecanadian.space"><img src="https://img.shields.io/badge/thecanadian.space-visit-0EA5E9?style=for-the-badge&logo=rocket&logoColor=white" alt="thecanadian.space" /></a>
  <a href="https://wiki.thecanadian.space"><img src="https://img.shields.io/badge/Public%20Wiki-docs-14B8A6?style=for-the-badge&logo=readthedocs&logoColor=white" alt="Public wiki" /></a>
  <a href="https://patreon.com/Godimas101"><img src="https://img.shields.io/badge/Patreon-project%20log-FF424D?style=for-the-badge&logo=patreon&logoColor=white" alt="Patreon" /></a>
  <a href="https://www.linkedin.com/in/rustygear/"><img src="https://img.shields.io/badge/LinkedIn-work%20stuff-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
</p>

> **"Aerospace news for Canada — fully automated, end-to-end."**

The Canadian Space is a real production newsroom that discovers, researches, edits, and publishes aerospace stories relevant to Canada — without human intervention. Seven specialized blog workflows, an AI editor pass, cost tracking, and social publishing, all orchestrated in **n8n** on a self-hosted VPS. Stories land at [**thecanadian.space**](https://thecanadian.space) 24/7.

## 🚀 Shipping now

**Seven active blog workflows:**

| Blog | Focus |
|---|---|
| **Daily Broadcast** | Cross-cutting aerospace news for the day |
| **NASA Overview** | NASA missions + programs |
| **SpaceX Report** | SpaceX launches, Starship, Dragon |
| **Commercial Space** | Rocket Lab-adjacent commercial ventures |
| **Bright Blue Origin** | Blue Origin coverage |
| **Rocket Lab Roundup** | Rocket Lab-specific reporting |
| **Canada From Orbit** | Canadian satellite + payload data |

Plus:
- **Editor LLM** — Claude Haiku with SEO rules + fact-check safeguards; Grok 3 fallback on API errors
- **Cost tracking** — real-time LLM API spend (Anthropic + Google + xAI), weekly digest
- **Social posts** — automated X + LinkedIn engagement
- **Multi-source ingestion** — 40+ news sources via Crawl4AI + plain HTTP + WordPress REST APIs

## 🧰 The stack

<p align="left">
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/WordPress-21759B?style=for-the-badge&logo=wordpress&logoColor=white" alt="WordPress" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" alt="Redis" />
  <img src="https://img.shields.io/badge/Caddy-1F88C0?style=for-the-badge&logo=caddy&logoColor=white" alt="Caddy" />
  <img src="https://img.shields.io/badge/OVH%20VPS-123F6D?style=for-the-badge&logo=ovh&logoColor=white" alt="OVH VPS" />
  <img src="https://img.shields.io/badge/Claude-DC7B4C?style=for-the-badge&logo=anthropic&logoColor=white" alt="Claude" />
</p>

- **Orchestration:** n8n (39 workflows total)
- **Python:** article scraper, cost processors, API helpers
- **CMS:** WordPress (Newfold hosting)
- **LLMs:** Anthropic Claude (Haiku primary, Opus for heavy analysis), Google Gemini, xAI Grok via OpenRouter
- **Infrastructure:** OVH VPS2 — Docker + Redis + Caddy reverse proxy
- **SEO:** Rank Math WordPress plugin

## 📚 The repos

**Public**

| Repo | What's in it |
|---|---|
| [**tcs-tools**](https://github.com/The-Canadian-Space/tcs-tools) | Python utilities — article scraper, cost calc, data processing |
| [**tcs-scripts**](https://github.com/The-Canadian-Space/tcs-scripts) | n8n workflow node definitions, API cost trackers, utility scripts |
| [**tcs-public-wiki**](https://github.com/The-Canadian-Space/tcs-public-wiki) | Source for the public-facing docs at [wiki.thecanadian.space](https://wiki.thecanadian.space) |
| [**tcs-images**](https://github.com/Godimas101/tcs-images) | 100+ images used across published posts. Stays under `Godimas101/` to preserve WordPress URLs. |

**Private** *(workflow management + games in development)*

| Repo | Status |
|---|---|
| **tcs-workflows** | Automated backups of all 39 n8n workflows |
| **tcs-docs** | Internal wiki (Cloudflare-Access-gated) |
| **tcs-archive** | Historical dev artifacts |
| **tcs-webpage** | *Planned* — rebuild of the site frontend (moving off WordPress) |
| **idle-launch** | *In development* — a space-themed browser idle game for launch-watchers |
| **autodoom** | *In development* — an auto-playing take on Doom, inspired by Clickpocalypse 2 |

## 🎯 What's next

- **tcs-webpage rebuild** — move away from WordPress to a custom frontend (design phase)
- **TCS arcade launch** — two browser games in development ([`idle-launch`](https://github.com/The-Canadian-Space/idle-launch) + [`autodoom`](https://github.com/The-Canadian-Space/autodoom), currently private during build)
- **Fact-checker LLM pass** — automated claim verification via extended-thinking models
- **International aerospace sources** — expanding beyond Canada-adjacent coverage

## 📖 Visit

- **Blog:** [thecanadian.space](https://thecanadian.space)
- **Public wiki:** [wiki.thecanadian.space](https://wiki.thecanadian.space)
- **Behind the scenes:** [Patreon — project log](https://patreon.com/Godimas101)

## 🤝 Contributing

Currently a solo venture, but built with future collaborators in mind. If you're interested in the newsroom, the Python tools, or the n8n workflows, reach out. Every repo has an **AGENTS.md** at the root for technical onboarding — start there.

## 🧡 Support

The Canadian Space is a personal project + portfolio piece. If you like what we're building, **Patreon** is where the running project log lives — behind-the-scenes notes, dev diaries, cost breakdowns, and updates you won't see on the blog.

[![Support on Patreon](https://raw.githubusercontent.com/Godimas101/personal-projects/main/patreon/images/buttons/patreon-medium.png)](https://patreon.com/Godimas101)

---

*The Canadian Space is built + operated by [Chris Carpenter (Godimas101)](https://github.com/Godimas101). Full-stack automation, AI integration, and self-hosted infrastructure — running live 24/7.*

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&section=footer&height=120&color=0:0B1021,30:0EA5E9,65:2563EB,100:7C3AED" />
</p>
