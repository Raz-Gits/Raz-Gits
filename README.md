## Raz Sela

I build the systems behind marketing and sales: lead pipelines, email infrastructure,
CRM integrations, and the automation that has to keep working when nobody is watching it.

Most of what I build runs in production for a small number of businesses rather than
in the open, so a lot of my repositories here are private. Six that are not, plus a
skill I packaged:

### [outbound-pipeline](https://github.com/Raz-Gits/outbound-pipeline)

The enrichment and delivery half of my outbound engine, extracted and made
source-agnostic: a CSV of leads goes in, verified emails come out, and shipping to
the sequencer is report-only unless three separate gates agree. Providers run
cheapest first, from SMTP-verified pattern guessing through four free-quota finders
to paid lookups behind explicit spend gates with hard monthly caps that fail closed
on a corrupt ledger. The do-not-contact list is append-only plain text, checked at
ship time rather than run start, because people opt out mid-run.

Python, one dependency. The README's "parts that took the longest to learn" section
is the honest changelog of what production taught me.

### [n8n-workflows](https://github.com/Raz-Gits/n8n-workflows)

n8n work, exported and cleaned for sharing. The first is a hiring-signal pipeline. A
company posting its first SDR job is about to build outbound from nothing, so the
workflow finds those postings, asks Apollo how many SDRs are already there, finds a
decision maker through an Apollo, Hunter and Snov cascade, verifies the address, has
GPT write three openers from the company's own site, and routes first-SDR companies to
their own Instantly campaign.

n8n, JavaScript, PostgreSQL, Apollo, Hunter, Snov, OpenAI, Instantly.

### [claude-code-skills](https://github.com/Raz-Gits/claude-code-skills)

Skills and a subagent for Claude Code, built around the idea that an agent is most
useful when it is willing to tell you something you did not want to hear. `grill-me`
interrogates a claim three levels deep instead of stopping at the rehearsed first
answer, and returns a verdict per claim rather than a list of questions.
`blast-radius` asks what a change touches before anyone notices, which is the
question that actually predicts incidents. `integration-forensics` is the catalogue
of ways a third-party API lies to you. `memory` borrows the bi-temporal model from
temporal knowledge graphs so a stored fact can expire instead of quietly going stale.
`voice` learns how you write from your corrections.

Markdown, an installer, no dependencies. MIT.

### [poke-research](https://github.com/Raz-Gits/poke-research)

Pokémon TCG analytics. A ridge model fit per rarity cluster estimates each card's
expected price from explainable signals, and the gap against the live market flags
cards trading above or below fundamentals. Also computes expected value per sealed
set. A daily GitHub Actions pipeline pulls from open APIs, accrues its own market
history, and redeploys the site.

Python, NumPy (the ridge fit is hand-rolled, not scikit-learn), GitHub Actions, Netlify.

### [Instantly-Reply-Bot](https://github.com/Raz-Gits/Instantly-Reply-Bot)

Reply triage for cold-email campaigns. A webhook classifies every inbound reply using
OpenAI structured outputs, with deterministic rules running first so the obvious cases
never reach the model. Unsubscribes process automatically through the sending
platform's API, anything needing a person routes to a channel with full context, and
the public version drafts for a human to send; in production the defined cases replied
automatically. Dockerised, CI on every push, 59 tests.

TypeScript, Fastify, OpenAI, Zod, Vitest, Railway.

### [dev-sync](https://github.com/Raz-Gits/dev-sync)

How I move work between a Mac and a Windows PC. One command parks everything, including
half-finished work, and pushes; one command on the other machine puts it back exactly as
it was. Secrets travel encrypted with sops and age, with each machine holding its own
private key, and a read-only monitor flags any repo with an unsealed or stale secret.
Packaged as Claude Code skills.

Bash, sops, age, Git.

### [claude-seo-skill](https://github.com/Raz-Gits/claude-seo-skill)

A Claude Code SEO audit skill that I packaged and use. The skill is
[Bhanunamikaze/Agentic-SEO-Skill](https://github.com/Bhanunamikaze/Agentic-SEO-Skill),
which builds on [AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo),
both MIT, included unchanged; my part is the packaging and the README. Thirty-three
scripts check the actual page, headers, sitemap and schema; nine specialist subagents
run in parallel over their own domains; and a final verifier removes duplicates and
anything a measurement contradicts before the report is written. GitHub repository
SEO is its own lane.

Python. The GitHub scripts and the verifier use only the standard library; the website
checks need `requests` and `beautifulsoup4`, and the visual checks need Playwright. No
required API keys.

## What I spend most of my time on

**Outbound infrastructure.** Scrapers feeding an eight-provider enrichment and
verification waterfall. Self-hosted n8n handled delivery across three client
workspaces, with every send, reply and bounce logged so the data decided which
campaigns kept running. Moving to verified-only sending took bounce rates from double
digits down to under one percent.

**Web and lead systems** for an interstate moving company: a React and TypeScript site
with a prerender pipeline that fails the build on SEO regressions, multi-step quote
funnels with SMS verification and bot protection, per-channel attribution into the
CRM, and abandonment capture that turns a silent drop-off into a follow-up.

**The unglamorous half.** Append-only ledgers so a retry cannot contact the same
person twice, alerts that fire loudly instead of logging quietly, report-only as the
default mode for anything that sends, secret scanning on every commit, and deletion
tooling that permanently removes a person's data on request to meet CAN-SPAM, GDPR and
CCPA requirements.

## Stack

TypeScript, Python, React, Astro, Node, PostgreSQL and Supabase, n8n, Docker, Railway,
GitHub Actions. I develop with Claude Code daily and treat what it writes the way I
would treat a junior engineer's code: reviewed, tested, and run in report-only mode
before it touches anything real.

B.S. Information Technology, University of Central Florida, December 2026.

[linkedin.com/in/raz-sela-56a846255](https://www.linkedin.com/in/raz-sela-56a846255)
