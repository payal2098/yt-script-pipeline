# YouTube Script Pipeline Skill

An end-to-end YouTube video script production skill for Claude Code. Handles the full pipeline from topic research to fact-checking — works with any brand or channel.

## What It Does

This skill runs a 4-phase pipeline for every YouTube video:

1. **Research** — Topic research backed by keyword data (DataForSEO API), competitor analysis (YouTube Data API), content calendar planning, performance analysis, and backlog optimization.
2. **Write** — Script writing using 5 proven frameworks (AIDA, PAS, HSO, Listicle, Tutorial), plus titles, thumbnails, descriptions, tags, timestamps, and CTA templates.
3. **Edit** — 5-checkpoint editorial review scored out of 50 (Hook & Engagement, Brand Voice, Structure & Flow, SEO Optimization, Accuracy & Completeness).
4. **Fact-Check** — Verifies every claim against product files, domain knowledge, competitor data, and scientific sources. Flags contradictions and over-promises.

## Features

- **Brand-agnostic** — works for any business. Reads all brand config from the project's `CLAUDE.md`.
- **24 universal quality rules** — battle-tested rules derived from 15+ scripts worth of error analysis. Covers product mentions, jargon, hooks, listicle formatting, fact-check discipline, and more.
- **Rule override system** — any rule can be overridden per-project via `CLAUDE.md`.
- **Auto error logging** — maintains a `memory/script-errors-log.md` per project. Errors caught once never repeat.
- **Data-backed packaging** — generates 5 title options, 2-3 thumbnail concepts, SEO-optimized descriptions, and 15-20 tags per video.
- **Supports Shorts + Long-form** — optimized templates for both 16-30 second Shorts and 3-5 minute videos.

## Required API Credentials

This skill requires two APIs. Store credentials in your project's `CLAUDE.md` under `## API Keys`.

### DataForSEO API

| Field | Details |
|-------|---------|
| **Purpose** | Keyword research, search volume, competition, keyword difficulty |
| **Sign up** | [dataforseo.com](https://dataforseo.com) |
| **Credentials** | Username (email) + Password |
| **Auth** | Basic Auth (base64 encoded) |
| **Cost** | Pay-per-use (~$0.01-0.05/request) |

### YouTube Data API v3

| Field | Details |
|-------|---------|
| **Purpose** | Channel analytics, video metrics, competitor analysis |
| **Sign up** | [Google Cloud Console](https://console.cloud.google.com) |
| **Credentials** | API Key + Channel ID + Uploads Playlist ID |
| **Cost** | Free (10,000 quota units/day) |

## Setup

### 1. Install the skill

Copy the `yt-script-pipeline/` folder into your project directory.

### 2. Add required sections to your project's CLAUDE.md

The skill expects these sections in your `CLAUDE.md`:

| Section | Purpose |
|---------|---------|
| `## Brand Overview` | Company name, tagline, positioning, key selling points |
| `## Product Catalog` | Product categories, file paths, pricing tiers |
| `## Target Audience` | Demographics, pain points, motivations |
| `## Competitor Landscape` | Top competitors with metrics |
| `## YouTube Channel Analysis` | Channel metrics, content theme performance |
| `## Keyword Research Database` | Golden keyword opportunities, seasonal trends |
| `## Tone & Voice Guidelines` | Brand voice, do's and don'ts |
| `## Content Strategy` | Content pillars, upload schedule |
| `## API Keys` | DataForSEO + YouTube API credentials |
| `## Production Context` | Speaker, setting, greeting, sign-off, jargon ban list |
| `## Script Rule Overrides` | *(Optional)* Override any universal rule |

### 3. Use it

Just ask Claude to write a YouTube script, research a topic, or review existing content. The skill triggers automatically.

**Example prompts:**
- "Write a YouTube script about [topic]"
- "Research video topics for our channel"
- "Review this script before we publish"
- "Create a content calendar for next month"
- "Fact-check this script"

## Universal Rules (24 total)

The skill enforces 24 quality rules by default. Key highlights:

- Max 2 product mentions per script (1 body + 1 CTA)
- Odd-numbered listicles only (3, 5, 7, 9)
- Hook must directly match the video topic
- No multiplier promises ("double", "triple")
- No jargon — if it sounds like a textbook, rewrite it
- Product names must match product files word-for-word
- Care instructions must match product "How to Use" exactly
- Cross-check "do" vs "don't" sections for contradictions
- Every claim must be actually verified — never rubber-stamped

Override any rule in your `CLAUDE.md`:

```markdown
## Script Rule Overrides

### Rule 2 Override: Max Product Mentions
- **Default:** Max 2 product mentions
- **Override:** Max 3 for product showcase videos
```

## License

MIT
