# AGENTS.md — The-Canadian-Space

This is how The Canadian Space (TCS) works and what you need to know before making changes.

TCS is an automated aerospace and space news platform: six GitHub repositories, 39 n8n workflows, and a WordPress site that publishes daily articles to around 3,000 readers. It's built on Python scrapers, n8n automation, and Claude/Gemini for writing and editing. It's been running production for two years and handles real traffic, real content, and real infrastructure.

This guide is for anyone (Chris currently, but eventually other contributors) making changes to TCS. Read it first. It's not rigid doctrine—it's accumulated hard-won knowledge about what works and what breaks.

**Maintained by:** Chris Carpenter (Godimas101)  
**Last updated:** 2026-07-11  
**Applies to:** All TCS repos and infrastructure

---

## The TCS Stack

- **Workflow engine:** n8n (39 total workflows, 14 tagged TCS)
- **Content platform:** WordPress on Newfold (thecanadian.space)
- **Infrastructure:** OVH VPS2 (Docker + n8n + Redis + Caddy reverse proxy)
- **Code:** Python 3.9+ (scrapers, helpers), JavaScript (n8n Code nodes), Bash (maintenance)
- **LLM services:** OpenRouter (Anthropic Haiku 4.5 primary, Gemini and Grok as fallbacks)
- **Source control:** GitHub (6 TCS repos in The-Canadian-Space org)

---

## Repositories at a Glance

**In The-Canadian-Space org:**

- **tcs-workflows** (PRIVATE) — Daily backup of live n8n workflows. Read-only. Do not edit.
- **tcs-scripts** (PUBLIC) — Python helpers for each content source (NASA, SpaceX, Commercial, etc.). Edit freely.
- **tcs-tools** (PUBLIC) — Utility tools: article scraper, agency search, cost tracking. Edit freely.
- **tcs-arcade** (PRIVATE) — Browser games (planning phase). Edit freely.
- **tcs-webpage** (PRIVATE) — Custom WordPress rebuild (planning phase). Edit freely.

**Outside the org (intentionally):**

- **tcs-images** (PUBLIC, under Godimas101 permanently) — 100+ images hard-linked in published WordPress posts. Do not edit without explicit approval.

---

## Three Safety Rules

These rules protect real infrastructure:

**1. tcs-images is production.** Every image in that repo has raw.githubusercontent.com URLs baked into published blog posts. If you rename, delete, or move a file, those links break and posts show broken images to readers. Before touching anything in tcs-images:
   - Ask Chris first
   - Audit which posts reference it
   - Plan a URL migration in WordPress
   - Verify the new links work in published posts

**2. Credentials are never in git.** GitHub PAT, WordPress API keys, and OpenRouter tokens live in .env on OVH and in n8n's Docker volume. Never log them, commit them, or print them to console.

**3. Test on staging before production.** All n8n workflow changes and WordPress content updates must run on staging first. If you're unsure whether staging exists, ask.

---

## How to Be Useful

### Before you start

- Clone the repo locally and read its README (even if it's stale, it gives you a sense of the code).
- For n8n workflows: inspect the current node structure in the n8n UI. Never assume JSON is correct without checking the live workflow.
- For Python: understand which source it maps to and test against real API endpoints locally.
- If you find a bug or confusing code, that's valuable—document it.

### Write small changes

- Change one thing at a time. Test after each change.
- If a change is longer than 200 lines, split it into multiple commits.
- Commit messages: be specific. `fix(nasa-scraper): add missing date extraction` is better than `update nasa scraper`.

### Verify it works

- For workflows: execute it, observe the output, verify the result is what you expected.
- For scripts: run it locally with real inputs, check the output matches.
- For infrastructure: verify the change took effect with actual observation, not assumptions.

---

## Common Commands

```bash
# GitHub
gh repo list The-Canadian-Space --limit 100
gh repo clone The-Canadian-Space/tcs-workflows
gh api repos/The-Canadian-Space/tcs-images/contents/README.md

# n8n (local Docker test, if you set one up)
docker logs -f n8n

# WordPress REST API (test before building n8n nodes)
curl -X GET "https://thecanadian.space/wp-json/wp/v2/posts" \
  -H "Authorization: Bearer YOUR_WP_KEY"

# Python
python --version  # Must be 3.9+
pip install -r requirements.txt
```

---

## When to Ask Chris vs. Go Ahead

**Ask Chris if you need to:**
- Modify anything in tcs-images
- Rotate or create credentials
- Make changes to OVH VPS infrastructure
- Deploy changes to production WordPress
- Make breaking changes (rename repos, delete branches, etc.)
- Clarify whether something is TCS scope or personal scope

**You can handle on your own:**
- Write or update code in tcs-scripts, tcs-tools, tcs-arcade, tcs-webpage
- Add or improve documentation
- Test changes locally and push to dev branches
- Update gitignore, issue templates, or non-critical config

---

## Key Things That Have Broken (Learnings)

**n8n-specific:**
- Workflow imports fail silently if credential IDs don't match. Always test imports on staging first.
- GitHub API has a 5,000 request/hour limit. We're well under quota, but monitor if adding more GitHub integrations.
- Base64 encoding is required for binary file uploads to GitHub via REST API. The backup workflow handles this, but be aware if you add new upload nodes.
- Tag filtering: TCS workflows use 'TCS' (capital). Lowercase 'tcs' won't match.

**WordPress integration:**
- Image URLs must be absolute (https://...), never relative. raw.githubusercontent.com URLs will 404 if the repo migrates.
- Featured images require a media attachment ID, not a direct URL link.
- Custom fields set via REST API will overwrite manual edits in the WordPress UI on next workflow execution.

**GitHub + raw URLs:**
- Transferring a repo between organisations does not redirect raw.githubusercontent.com URLs. They 404. This is why tcs-images stays under Godimas101.

**Image processing:**
- Instagram images are composited on OVH (background, padding, centring). Output goes to tcs-images. Keep file sizes under 500 KB.
- tcs-images is sparse-checked locally (only README). Don't un-sparse without explicit permission.

**Deployment:**
- No GitHub Actions. Changes are deployed manually. This means no automated testing—test before you push.
- The backup workflow runs daily at 2 AM UTC. After org migration, it will split TCS workflows from personal workflows.
- OVH maintenance cron runs Sundays 3 AM EST. Don't deploy critical changes on Sundays.

**Author/editor prompts:**
- Anthropic Claude models emit thinking blocks. The editor workflow detects and removes them before publishing.
- SEO rules are enforced on every post: slug, meta description, featured image, category tags. These are non-negotiable.

---

## Project Layout

```
The-Canadian-Space (GitHub org)
├── tcs-workflows (PRIVATE)
├── tcs-images (PUBLIC, under Godimas101)
├── tcs-scripts (PUBLIC)
├── tcs-tools (PUBLIC)
├── tcs-arcade (PRIVATE)
└── tcs-webpage (PRIVATE)

Local: ~/VS Code Projects/n8n-projects/the-canadian-space/
├── tcs-workflows/ (git clone)
├── tcs-images/ (sparse checkout, images not locally stored)
├── tcs-scripts/ (git clone)
├── tcs-tools/ (git clone)
├── tcs-arcade/ (git clone)
├── tcs-webpage/ (git clone)
└── docs/ (local notes, prompts, safeguards)

OVH VPS (/opt/tcs/)
├── n8n/ (Docker config, .env, prompts, Caddy)
├── discordgsm/ (Discord game server monitor)
├── image-prep/ (Instagram compositor)
└── scripts/ (maintenance cron, utilities)
```

---

## Style & Conventions

- **Language:** Canadian English (favour, colour, centre, etc.)
- **Dates:** YYYY-MM-DD. Times in HH:MM EST/UTC.
- **Branch names:** `main` or `develop`, not `master`. Feature branches: `feature/short-name`. Hotfix: `hotfix/issue`.
- **File naming:** Kebab-case for markdown and config (`author-safeguards.md`). Snake_case for Python (`fetch_articles.py`).
- **n8n nodes:** PascalCase (`Fetch Articles`, `Upload to GitHub`).
- **Python:** PEP 8. Format with Black if you can.
- **Commit format:** `type(scope): description`. Types: `feat`, `fix`, `docs`, `refactor`. Example: `feat(spacex-scraper): add propellant data extraction`.

---

## How to Talk to Chris

- Be direct. If something is broken or unclear, say so.
- Document trade-offs. "I chose X over Y because Z" is the kind of note future you (and Chris) will appreciate.
- If you get stuck, that's data—describe the blocker and move on.
- Propose fixes for bugs, don't blame the original author.

---

## About This File

This AGENTS.md is the entry point for anyone working on TCS. It's meant to be:

- **Honest:** Real infrastructure, real constraints, real gotchas.
- **Portfolio-polished:** Someone in the game industry could read this and understand you know what you're doing.
- **Onboarding-friendly:** A future collaborator should be able to get productive without twenty chat sessions.
- **Living:** Update it as learnings emerge or things change. Version it in git.

It's not doctrine. It's accumulated wisdom about what works.

For deeper context on specific systems, see:
- **OPERATIONS.md** — How to access n8n, OVH VPS, and WordPress
- **ARCHITECTURE.md** — Why we chose certain tools and patterns
- **DECISIONS/** — Architectural decision records (ADRs)
- Each repo's README for language-specific setup and contribution guidelines

---

**Questions?** Ask Chris (rustygear@hotmail.com) or open an issue in the relevant repo.