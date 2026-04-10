---
name: yt-script-pipeline
description: End-to-end YouTube video script pipeline — research, write, edit, and fact-check scripts for any brand or channel. Covers video scripts, topic research, keyword analysis, titles, thumbnails, descriptions, tags, editorial review, fact-checking, and competitor analysis. Use this skill whenever the user asks about YouTube content creation, video scripting, channel strategy, video SEO, or any aspect of YouTube production workflow. Reads brand config from CLAUDE.md. Requires DataForSEO + YouTube Data API credentials.
---

# YouTube Video Script Pipeline

> End-to-end pipeline: **Research → Write → Edit → Fact-Check** for every YouTube video.
> Works across any brand or project — reads all brand-specific config from the project's CLAUDE.md.

---

## STEP 0: Read CLAUDE.md First (MANDATORY)

**Before starting ANY task**, read the project's `CLAUDE.md` file. This is the master knowledge base for the brand. You need:

1. **Brand overview** — company name, tagline, core promise, key selling points
2. **Product catalog** — categories, product file paths, pricing tiers
3. **Target audience** — primary, secondary, tertiary segments with pain points, motivations, buying behavior
4. **Competitor landscape** — top competitors with metrics and positioning
5. **YouTube channel analysis** — subscribers, video count, performance metrics, paid vs organic gap, content theme performance, optimal formats
6. **Keyword research database** — golden opportunities (high volume + low competition), seasonal trends
7. **Tone & voice guidelines** — brand voice, do's and don'ts
8. **Content strategy** — content pillars, upload schedule
9. **API keys** — DataForSEO credentials + YouTube Data API key and Channel ID
10. **Production context** — speaker name, setting, greeting format, reference script, brand sign-off, jargon ban list
11. **Script rule overrides** — any project-specific overrides to the universal rules

**Do NOT skip this step.** Every script decision must be informed by the data in CLAUDE.md.

---

## When to Use This Skill

Activate when the user asks for:
- Video script writing (Shorts or long-form)
- Video topic research or keyword analysis
- Title options, thumbnail concepts, or packaging
- Video descriptions, tags, or timestamps
- Editorial review or quality check of a script
- Fact-checking a script or content piece
- Competitor channel analysis
- Community post drafts or pinned comments
- Any YouTube content creation task

---

## Required CLAUDE.md Sections

The skill expects these sections in each project's CLAUDE.md. If any are missing, prompt the user to add them.

| Section | Purpose | Required? |
|---------|---------|-----------|
| `## Brand Overview` | Company name, tagline, positioning, key selling points | Yes |
| `## Product Catalog` | Product categories, file paths, pricing tiers | Yes |
| `## Target Audience` | Primary/secondary/tertiary with demographics, pain points | Yes |
| `## Competitor Landscape` | Top competitors with metrics | Yes |
| `## YouTube Channel Analysis` | Channel metrics, benchmarks, content theme performance | Yes |
| `## Keyword Research Database` | Golden opportunities, seasonal trends | Yes |
| `## Tone & Voice Guidelines` | Brand voice, do's and don'ts | Yes |
| `## Content Strategy` | Content pillars, upload schedule | Yes |
| `## API Keys` | DataForSEO + YouTube API credentials | Yes |
| `## Production Context` | Speaker, setting, greeting, sign-off, jargon ban list | Yes |
| `## Script Rule Overrides` | Override any universal rule | Optional |

---

## Required API Credentials

This skill needs two API services. Store credentials in CLAUDE.md under `## API Keys`.

### DataForSEO API
- **What it does:** Keyword research, search volume, competition data, keyword difficulty, domain analysis
- **How to get it:** Sign up at dataforseo.com
- **Credentials needed:** Username (email) + Password
- **Auth method:** Basic Auth (base64 encode "username:password")
- **Base URL:** `https://api.dataforseo.com/v3/`
- **Key endpoints:**
  - `/keywords_data/google/search_volume/live` — search volume for keywords
  - `/keywords_data/google/keywords_for_keywords/live` — related keyword suggestions
  - `/serp/youtube/organic/live` — YouTube SERP results
- **Cost:** Pay-per-use (~$0.01-0.05 per request)
- **CLAUDE.md config needed:** Username, Password, Location code (e.g., 2356 for India, 2840 for USA)

### YouTube Data API v3
- **What it does:** Channel analytics, video metrics, competitor channel analysis, packaging research
- **How to get it:** Google Cloud Console → Enable YouTube Data API v3 → Create API Key
- **Credentials needed:** API Key + Channel ID + Uploads Playlist ID
- **Cost:** Free tier (10,000 quota units/day)
- **CLAUDE.md config needed:** API Key, Channel ID, Uploads Playlist ID

---

## Workflow: 4 Phases

Every video goes through these 4 phases in sequence.

| Phase | Purpose | When to Use |
|-------|---------|-------------|
| 1. Research | Topic research, keyword analysis, competitor check | Before choosing a topic |
| 2. Write | Script, titles, thumbnails, description, tags | Before writing any content |
| 3. Edit | 5-checkpoint editorial review and scoring | Before delivering content |
| 4. Fact-Check | Verify every claim, product mention, instruction | Before delivering content |

---

# PHASE 1: RESEARCH

> **Role:** Topic researcher, keyword analyst, competitor monitor, performance analyst.

## 1.1 Topic Research

Find video topics backed by search volume data using the DataForSEO API. Cross-reference with YouTube search trends. Prioritize by: search volume, competition level, keyword difficulty, relevance to the brand's products.

**Topic Brief Output Format:**
```
## Topic: [Title Idea]
- **Target Keyword:** [primary keyword]
- **Monthly Search Volume:** [number]
- **Keyword Difficulty:** [score]
- **Competition:** [LOW/MEDIUM/HIGH]
- **Content Pillar:** [from CLAUDE.md content pillars]
- **Recommended Format:** [Short 16-30s / Long 3-5min / Tutorial 1-3min]
- **Framework:** [AIDA / PAS / HSO / Listicle / Tutorial]
- **Product Tie-in:** [relevant brand product, if any]
- **Why This Topic:** [rationale based on data]
- **Competitor Coverage:** [who has covered this, their view counts]
```

## 1.2 Competitor Monitoring

Track competitor YouTube channels listed in CLAUDE.md `## Competitor Landscape`. Use the YouTube Data API v3 for channel/video data. Monitor for: new video topics, high-performing content, engagement patterns, content gaps.

**Competitor Report Format:**
```
## Competitor: [Channel Name]
- **Recent High-Performer:** [video title] — [views] in [timeframe]
- **Topic:** [what it covers]
- **Our Opportunity:** [how the brand can cover this better/differently]
- **Product Angle:** [relevant brand product]
```

## 1.3 Performance Analysis

Use the YouTube Data API v3 with the channel ID from CLAUDE.md. Pull: views, likes, comments, watch time, CTR, retention data. Compare against channel benchmarks from CLAUDE.md `## YouTube Channel Analysis`. Identify what topics/formats/lengths perform best. Flag videos with promotion signatures (high views, near-zero engagement).

**Performance Report Format:**
```
## YouTube Performance Report — [Period]

### Key Metrics
| Metric | This Period | Previous Period | Change |
|--------|-----------|----------------|--------|
| Total Views | ... | ... | +/-% |
| Avg Views/Video | ... | ... | +/-% |
| Like Rate | ... | ... | +/-% |
| Comment Rate | ... | ... | +/-% |

### Top 5 Performers
[table with title, views, likes, comments, duration]

### Bottom 5 Performers
[table — analyze WHY they underperformed]

### Recommendations
[3-5 actionable items based on data]
```

## 1.4 Backlog Optimization

Audit existing videos for: missing tags, missing/incomplete descriptions, videos not in any playlist, videos that could be re-optimized (good content, bad titles/thumbnails). Prioritize by: views potential, keyword opportunity, effort required.

**Backlog Audit Format:**
```
## Video: [Title]
- **Current Views:** [number]
- **Issues Found:**
  - [ ] No tags
  - [ ] No timestamps/chapters
  - [ ] Description too short
  - [ ] Not in any playlist
  - [ ] Title not SEO-optimized
- **Recommended Fix:** [specific actions]
- **Target Keyword:** [what this video should rank for]
- **Suggested New Title:** [optimized version]
- **Priority:** [HIGH/MEDIUM/LOW]
```

## Research Rules

1. **Always lead with data.** Never suggest topics without search volume or competitive analysis.
2. **Cite sources.** State whether data is from DataForSEO, YouTube API, or the keyword database in CLAUDE.md.
3. **Think about the funnel.** Topics should either build audience (top-of-funnel) or drive product sales (bottom-of-funnel).
4. **Flag seasonal timing.** If a topic is time-sensitive, state the optimal publish window.
5. **Reference the product catalog.** When a topic connects to a brand product, name the specific product and link to its file.
6. **Track what's been covered.** Before suggesting a topic, check if the channel already made a video on it (use YouTube API).
7. **Always use odd-numbered listicles.** 3, 5, 7, 9 — never 4, 6, 8, 10.
8. **Proactively cross-reference the product catalog.** When researching any topic, check EVERY item against the product catalog. If the brand sells something relevant, include it in the topic brief.

---

# PHASE 2: WRITE

> **Role:** Script writer, title creator, thumbnail concept designer, description & metadata writer, community content writer.

## 2.1 Script Writing Frameworks

**AIDA (Attention-Interest-Desire-Action)**
- Best for: Product demos, kit unboxings, promotional content
- Structure:
  1. **Attention** (2-5 sec): Bold visual hook or surprising statement
  2. **Interest** (30 sec): Present the problem or opportunity
  3. **Desire** (1-2 min): Show the solution working, demonstrate results
  4. **Action** (10 sec): Clear CTA

**PAS (Problem-Agitate-Solution)**
- Best for: Problem-solving content, troubleshooting, "why X is happening" videos
- Structure:
  1. **Problem** (10-15 sec): State it clearly
  2. **Agitate** (30-45 sec): Amplify the pain, show consequences
  3. **Solution** (1-2 min): Present the fix with demonstration

**HSO (Hook-Story-Offer)**
- Best for: Longer educational videos (3-5 min), personal/relatable stories
- Structure:
  1. **Hook** (5-10 sec): Attention-grabbing opening
  2. **Story** (2-3 min): Relatable journey with teaching moments
  3. **Offer** (30-60 sec): Product/tip as natural resolution

**Listicle/Countdown**
- Best for: Tips videos, "Top 3/5/7/9" content (always ODD numbers)
- Structure:
  1. **Hook** (5-10 sec): Promise the number and value
  2. **Items** (30-60 sec each): Each with mini-story/visual
  3. **Bonus + CTA** (15-30 sec)

**Tutorial/How-To**
- Best for: Step-by-step guides, care instructions, setup guides
- Structure:
  1. **End result first** (10 sec): Show what they'll achieve
  2. **Materials needed** (15-30 sec)
  3. **Step-by-step** (2-3 min)
  4. **Final result** (15 sec)
  5. **Tips + CTA** (30 sec)

## 2.2 Script Output Format

```
## VIDEO SCRIPT

**Title:** [Working title]
**Format:** [Short 16-30s / Long 3-5min / Tutorial 1-3min]
**Framework:** [AIDA / PAS / HSO / Listicle / Tutorial]
**Target Keyword:** [primary keyword]
**Product Tie-in:** [brand product, if any]

---

### HOOK (0:00 - 0:XX)
[Visual direction]
[Dialogue/voiceover]

### SECTION 1: [Name] (0:XX - X:XX)
[Visual direction]
[Dialogue/voiceover]

### SECTION 2: [Name] (X:XX - X:XX)
[Visual direction]
[Dialogue/voiceover]

### CTA (X:XX - X:XX)
[Visual direction]
[Dialogue/voiceover]

---

**PRODUCT MENTION:** [How and when the product is mentioned — must feel natural]
**B-ROLL SUGGESTIONS:** [Visual shots needed]
**ENGAGEMENT PROMPT:** [Question to ask viewers]
```

## 2.3 Video Format Guidelines

| Format | Word Count | Duration | Use |
|--------|-----------|----------|-----|
| Shorts | 50-80 words | 16-30 seconds | Quick tips, one idea, one payoff |
| Long-form | 500-800 words | 3-5 minutes | Educational, problem-solving, listicles |
| Tutorial | 150-450 words | 1-3 minutes | Step-by-step guides |

Speaking rate target: ~150 words/min.

**Performance insight:** 16-30 second shorts and 3-5 minute long-form videos tend to perform best. Avoid 31-60 second shorts — they underperform both formats.

## 2.4 Title Generation

Generate **5 title options** per video, ranked by priority.

**Title Rules:**
- Maximum 60 characters (won't get truncated)
- Include the target keyword naturally
- Use proven patterns: Questions, Numbers, THIS/STOP hooks, How-to
- Create curiosity gap — promise a specific benefit or revelation
- Avoid clickbait that can't be delivered on

**Title Output Format:**
```
## TITLE OPTIONS (ranked)

1. [Title] — [why this works]
2. [Title] — [why this works]
3. [Title] — [why this works]
4. [Title] — [why this works]
5. [Title] — [why this works]

**Recommended:** #[X] because [reasoning]
**Target Keyword:** [keyword] | **Search Vol:** [number]
```

## 2.5 Thumbnail Concepts

Create **2-3 thumbnail concepts** per video.

**Thumbnail Brief Format:**
```
## THUMBNAIL CONCEPT [#]

**Layout:** [Split screen / Before-After / Close-up / Text-heavy / Reaction]
**Primary Image:** [What the main visual should be]
**Text Overlay:** [Max 4-5 words, large and readable]
**Text Color/Style:** [Color, outline, font style]
**Emotion/Expression:** [If a person is shown]
**Color Scheme:** [Background and accent colors]
**Contrast Element:** [What creates visual pop]

**Why This Works:** [Brief rationale]
```

**Thumbnail Rules:**
1. Maximum 4-5 words of text — readable at mobile size
2. High contrast — must pop in a feed
3. One clear focal point
4. Before/after patterns are proven performers
5. Show results — transformations, solved problems
6. Thumbnail and title should complement, not repeat

## 2.6 Description & Metadata

**Description Template (for ALL videos):**
```
[2-3 sentence content summary with primary keyword naturally included]

[If applicable: "Products featured in this video:"]
[Product name + link to product page]

---

TIMESTAMPS:
0:00 — [Chapter title]
0:XX — [Chapter title]
X:XX — [Chapter title]

---

Shop [Brand Name]:
[Brand website URL]
[Marketplace links if applicable]

Follow us:
[Social media links from CLAUDE.md]

---

#[hashtag1] #[hashtag2] #[hashtag3] #[hashtag4] #[hashtag5]
```

**Tags (generate 15-20 per video):**
- First 3 tags: exact target keyword, brand name, broad category
- Next 5 tags: keyword variations and long-tail versions
- Next 5 tags: related topics the video touches
- Final 5 tags: broad discovery tags
- Always include the brand name and brand handle

## 2.7 Community Content

**Pinned Comment (write for every video):**
```
[Engagement question related to the video topic]
[Optional: bonus tip not covered in the video]
[Optional: link to related video or product]
```

**Community Post Types:**
- **Poll:** "What should we cover next?" with 4 options
- **Behind-the-scenes:** What's coming next on the channel
- **Quick tip:** One actionable tip with a photo
- **Product spotlight:** New arrival or back-in-stock announcement
- **Seasonal:** Tie to seasonal trends from keyword data

## 2.8 CTA Templates

Every CTA follows this pattern:
1. **Wrap-up line** — summarize the video value
2. **Product mention** — brief, soft ("check out our...")
3. **Engagement ask** — like, subscribe, bell, comment prompt
4. **Sign-off** — warm, personal (use brand sign-off from CLAUDE.md `## Production Context`)

**CTA by Video Type:**

**Educational / Tips:**
"And if this video helped, give it a thumbs up, hit subscribe, and tap the bell for more tips from [Brand Name]. If there's a tip that's worked for you — share it in the comments! Until then, [brand sign-off]!"

**Product / Showcase:**
"If you enjoyed this video, give it a thumbs up, subscribe, and ring the bell for more from [Brand Name]. I'll see you in the next one — until then, [brand sign-off]!"

**Listicle:**
"If this was helpful, hit that like button so more people can find this video. Tell me in the comments which one you're trying first! Don't forget to subscribe and ring the bell — I'll see you in the next one. [Brand sign-off]!"

**Problem-Solution:**
"If this helped, smash that like button and share this with a friend who needs it. Subscribe and hit the bell so you don't miss the next fix. Until next time — take care, and [brand sign-off]!"

**Seasonal / Gifting:**
"If you enjoyed this video, give it a thumbs up, subscribe, and ring the bell for more from [Brand Name]. Thanks for watching — and [brand sign-off]!"

**How-To / Tutorial:**
"And if this made things easier for you, give it a thumbs up and subscribe for more step-by-step guides from [Brand Name]. Drop a comment if you have questions — I'll see you in the next one. [Brand sign-off]!"

**CTA Rules:**
- Always end with the brand sign-off from CLAUDE.md `## Production Context`
- Always include like + subscribe + bell
- Always include a specific comment prompt tied to the video topic (not generic)
- Keep it warm and personal — grateful tone, never pushy
- Mention the brand name once in the CTA
- Brief features only — never list product specs
- If a product was mentioned in the body, CTA must include a brief reminder pointing to the description link

## 2.9 Brand Voice

Read tone & voice guidelines from CLAUDE.md `## Tone & Voice Guidelines`. Apply consistently across all content.

**Universal voice principles (all projects):**
- **Friendly expert** — knowledgeable but never condescending
- **Encouraging coach** — "you can do this" energy for beginners
- Use relatable analogies for complex concepts
- Celebrate small milestones
- Conversational language — if it sounds like a textbook, rewrite it
- Actionable, step-by-step instructions
- Address common fears naturally
- Sensory language where appropriate

**Universal DON'Ts:**
- Don't be overly salesy or pushy about products
- Don't use jargon (check jargon ban list in CLAUDE.md `## Production Context` if one exists)
- Don't be preachy about the brand's values
- Don't assume prior knowledge from the audience
- Don't use generic filler content
- Don't over-promise results

---

# PHASE 3: EDIT

> **Role:** Chief editor and SEO reviewer. Reviews all content before production.

## 3.1 Five-Checkpoint Review

Each checkpoint scored /10. Below 7 on any = revision required.

### Checkpoint 1: Hook & Engagement Quality (/10)

**Script Hook (first 3 seconds):**
- [ ] Creates immediate curiosity, shock, or relatability?
- [ ] Avoids generic openings ("Hey guys", "Welcome back", "In today's video")?
- [ ] Connects to a real pain point or desire?
- [ ] **Directly matches the video's topic** — not tangentially related?
- [ ] Free of multiplier promises ("double", "triple", "10x")?

**Engagement Elements:**
- [ ] Specific engagement prompt (not generic "like and subscribe")?
- [ ] Question viewers can answer in comments?
- [ ] Reason to watch till the end?

### Checkpoint 2: Brand Voice & Tone (/10)

**Voice Check:**
- [ ] Friendly expert tone — knowledgeable but not condescending?
- [ ] Encouraging, not preachy?
- [ ] Simple language (no unexplained jargon)?
- [ ] Relatable analogies for complex concepts?
- [ ] Celebrates small wins?
- [ ] Addresses beginner fears naturally?

**Product Mention Check:**
- [ ] Maximum TWO product mentions (1 body + 1 brief CTA reminder)?
- [ ] Product mention feels natural, not like an ad break?
- [ ] Product name matches the product file EXACTLY (no invented attributes)?
- [ ] Care/usage instructions match the product's "How to Use" word-for-word?
- [ ] Product is currently in stock?
- [ ] CTA mention is brief features only — no specs?
- [ ] CTA includes reminder pointing to description link (if product in body)?
- [ ] No pricing in script?
- [ ] No DIY hacks/home remedies as alternatives to brand products?
- [ ] No active ingredients named as generic alternatives?

### Checkpoint 3: Content Structure & Flow (/10)

- [ ] Framework correctly applied (AIDA/PAS/HSO/Listicle/Tutorial)?
- [ ] Each section has clear purpose and smooth transitions?
- [ ] Information ordered logically (problem before solution)?
- [ ] Video length matches format (Shorts: 50-80 words, Long: 500-800 words)?
- [ ] No filler — every sentence adds value?
- [ ] CTA at end (not middle) and feels natural?
- [ ] Visual/B-roll directions included?
- [ ] Speaking pace natural (~150 words/min)?
- [ ] Dialogue sounds spoken, not written?
- [ ] Every list item has spoken numbered transition?
- [ ] Natural transitions between sections (no abrupt jumps)?
- [ ] Max 7 text overlays, all inside visual direction blocks?
- [ ] All items cross-referenced against brand product catalog?
- [ ] All supporting sections consistent with final script?

### Checkpoint 4: SEO Optimization (/10)

**Title:** Under 60 chars? Keyword included? Proven pattern? Curiosity gap?
**Description:** Keyword in first 2 sentences? Timestamps? Product links? 5+ hashtags? 150+ words?
**Tags:** 15-20 provided? First tag = target keyword? Brand name included?
**Thumbnail:** 4-5 words max? Readable at mobile? High contrast? Complements title?

### Checkpoint 5: Accuracy & Completeness (/10)

- [ ] All advice correct and verifiable for the brand's domain?
- [ ] Product names match product file EXACTLY?
- [ ] Care instructions match product's "How to Use" word-for-word?
- [ ] No misleading claims about results or timelines?
- [ ] No internal contradictions?
- [ ] Scientific/technical claims internally consistent?
- [ ] No overstated measurements?
- [ ] Statistics have sources?
- [ ] All deliverables present (script + titles + thumbnail + description + tags)?
- [ ] Video assigned to a content pillar?
- [ ] Target keyword specified?
- [ ] Playlist assignment suggested?

## 3.2 Red Flags (ANY = REJECT)

- More than 2 product mentions
- Spec-heavy CTAs
- Jargon the target audience wouldn't understand (check ban list in CLAUDE.md)
- DIY hacks or home remedies as alternatives to brand products
- Pricing in scripts
- Product attributes not in the product file
- Care instructions contradicting product's "How to Use"
- Contradictions between "do" and "don't" sections
- Even-numbered listicles (4, 6, 8, 10)
- Multiplier promises ("double", "triple", "10x")
- Active ingredients named as generic alternatives
- Over-promising results ("guaranteed", "works overnight")

## 3.3 Editorial Review Output Format

```
## EDITORIAL REVIEW

**Content:** [Video title / content being reviewed]
**Reviewed:** [Date]
**Verdict:** APPROVED / NEEDS REVISION / REJECTED

### Scores
| Checkpoint | Score | Status |
|-----------|-------|--------|
| Hook & Engagement | /10 | Pass/Fail |
| Brand Voice & Tone | /10 | Pass/Fail |
| Structure & Flow | /10 | Pass/Fail |
| SEO Optimization | /10 | Pass/Fail |
| Accuracy & Completeness | /10 | Pass/Fail |
| **OVERALL** | **XX/50** | **[Verdict]** |

### What Works Well
- [Specific positive callouts]

### Required Revisions
1. **[Issue]** — [What's wrong] → [How to fix it]

### Suggestions (optional improvements)
- [Nice-to-have improvements]

### SEO Notes
- **Target Keyword:** [keyword] — [properly used?]
- **Title Recommendation:** [if needed]
- **Missing Tags:** [if any]
- **Description Gaps:** [if any]
```

## 3.4 Scoring Guide

| Score | Meaning |
|-------|---------|
| 45-50 | Exceptional — publish immediately |
| 38-44 | Strong — approved with minor optional tweaks |
| 30-37 | Needs revision — fix issues, then re-review |
| Below 30 | Rejected — fundamental issues, rewrite |

## 3.5 Common Issues to Watch For

**Script:** Weak hooks, hook doesn't match topic, multiplier promises, info dumps without visual directions, salesy tone, spec-heavy CTAs, missing CTA product link reminder, no engagement loop, wrong format length, missing numbered transitions, abrupt section jumps, too many text overlays, jargon, invented product attributes, contradictions, stale supporting sections, missing product tie-ins.

**Title:** Too long (>60 chars), no keyword, clickbait without payoff, generic.

**Thumbnail:** Too much text (>4-5 words), low contrast, repeats the title, no focal point.

**SEO:** No tags, thin description, wrong keyword targeting, no playlist assignment.

---

# PHASE 4: FACT-CHECK

> **Role:** Verifies all claims, product information, competitor data, and technical statements before production.

## 4.1 What Gets Fact-Checked

### Product Claims
Every product mention must be verified against the product files at the catalog path in CLAUDE.md.

**Check:**
- [ ] Product name is exact (not paraphrased)
- [ ] Price is current (if mentioned — though pricing in scripts should be avoided)
- [ ] Product is in stock
- [ ] "What's included" matches the product file
- [ ] Benefits match the product description
- [ ] No claims that aren't in the product file
- [ ] Specific certifications (organic, non-GMO, etc.) actually apply to this product

### Domain-Specific Claims
All advice must be accurate and appropriate for the target audience's context (geography, climate, skill level, etc. as defined in CLAUDE.md).

Verify against: industry standards, peer-reviewed sources, official guidelines, the brand's own product documentation.

### Competitor Claims
**Check:** Competitor name and positioning correct? Funding/revenue sourced? Subscriber counts current? Comparisons fair? No defamatory statements?

### Scientific/Technical Claims
**Check:** Technical terms used accurately? Claims consistent with brand documentation? No internal contradictions?

### Statistical Claims
**Check:** YouTube stats match API data? Search volume sourced from DataForSEO? Growth percentages calculated correctly? Customer/review counts match current data?

## 4.2 Red Flag Claims (Always Flag)

- **Guaranteed results** — outcomes can't be guaranteed
- **"Kills/fixes/cures ALL"** — no product addresses every variant
- **"100% [absolute claim]"** — rarely accurate
- **"Works overnight/instantly"** — most results take time
- **"No maintenance needed"** — nearly everything requires upkeep
- **Medical/health claims** — requires citations
- **"The best product"** — subjective and potentially misleading
- **Pricing claims** — "cheapest" requires evidence

## 4.3 Verification Status Definitions

| Status | Meaning | Action |
|--------|---------|--------|
| **VERIFIED** | Factually accurate with reliable source | Approved |
| **INCORRECT** | Factually wrong | Must be corrected |
| **MISLEADING** | Technically true but could be misinterpreted | Needs rewording |
| **UNVERIFIED** | Cannot confirm or deny | Add qualifier or remove |
| **OUTDATED** | Was true but may no longer be | Needs updated data |

## 4.4 Standard Qualifiers

When a claim can't be fully verified, use qualifiers instead of absolutes:

| Instead of... | Use... |
|---------------|--------|
| "This will [guarantee result]" | "This can help [expected outcome]" |
| "[Fixes] all [problems]" | "Effective against common [problems] like [examples]" |
| "Guaranteed results" | "Designed to give you the best chance of success" |
| "100% [absolute]" | "Made with [specific attribute]" |
| "Results in days" | "Most users notice improvement within [realistic timeframe]" |
| "The best product" | "One of the most effective options for [audience]" |

## 4.5 Verification Discipline

These rules exist because of real errors in past scripts. They are critical.

1. **NEVER rubber-stamp claims as VERIFIED without actually checking the source.** Product attribute claims → open and read the product file, then compare word-for-word.
2. **Product file is the ONLY source of truth for product attributes.** If the script says something the product file doesn't → flag as INCORRECT.
3. **Scientific/technical claims must be internally consistent.** A substance can't be both "unavailable" and cause "toxicity" simultaneously. If two claims contradict → flag BOTH.
4. **Care instructions must match the product's "How to Use" exactly.** If the product says one thing and the script says another → flag as INCORRECT.
5. **Cross-section contradiction check.** Compare all "do" advice against all "don't" advice. If they contradict → flag both.
6. **Supporting section consistency.** Verify description, timestamps, and editorial review reference the SAME claims as the final script. If any were revised but supporting sections weren't updated → flag as INCONSISTENT.

## 4.6 Fact-Check Output Format

```
## FACT-CHECK REPORT

**Content:** [Video title / content being reviewed]
**Checked:** [Date]
**Verdict:** VERIFIED / NEEDS CORRECTIONS / FLAGGED

### Claims Reviewed

| # | Claim | Status | Notes |
|---|-------|--------|-------|
| 1 | "[exact claim from content]" | VERIFIED/INCORRECT/UNVERIFIED/MISLEADING | [explanation] |

### Product Mentions
| Product | Name Correct | In Stock | Description Accurate |
|---------|-------------|----------|---------------------|
| [product] | Yes/No | Yes/No | Yes/No |

### Issues Found
1. **[INCORRECT]** "[claim]" → **Correction:** [accurate version]
2. **[MISLEADING]** "[claim]" → **Suggested Rewrite:** [more accurate phrasing]

### Approved Claims
- [Claims that passed verification]

### Recommended Disclaimers
- [Any disclaimers to add]
```

---

# UNIVERSAL SCRIPT RULES

These 24 rules are universal defaults. They apply to ALL projects unless overridden in CLAUDE.md `## Script Rule Overrides`.

### Product Rules (1-9)

1. **Read the product file BEFORE writing.** Match every descriptor word-for-word. If the file doesn't say it, don't claim it.
2. **Max 2 product mentions per script** — 1 in body + 1 brief reminder in CTA.
3. **CTA = brief features, not specs.** Never list detailed specifications in the CTA.
4. **CTA must remind about product link.** If product was mentioned in body, CTA must point to the description link.
5. **Care/usage instructions must match the product's "How to Use" exactly.** Don't import general advice that contradicts the product.
6. **No pricing in scripts.** Never mention specific price amounts.
7. **No DIY hacks or home remedies as alternatives to the brand's products.** Always direct viewers to brand products.
8. **No active ingredients named as generic alternatives.** Describe what a good product DOES, not what's in it. Let the CTA name the brand product.
9. **Proactively cross-reference the product catalog.** Check EVERY item in the script against the product catalog. If the brand sells something relevant, recommend mentioning it.

### Script Writing Rules (10-20)

10. **Hook must directly match the video's topic.** Not tangentially related statements.
11. **No multiplier promises.** Never say "double", "triple", "10x." Use "way more" or "a lot more."
12. **Every list item needs a spoken numbered transition.** "Number one", "Next up — number two", etc. Never skip.
13. **Always use odd-numbered listicles.** 3, 5, 7, 9 — never 4, 6, 8, 10.
14. **No jargon.** Read every line out loud. If it sounds like a textbook or uses words the target audience wouldn't know, rewrite it. Check the jargon ban list in CLAUDE.md `## Production Context` if one exists.
15. **Natural transitions between every section.** Use bridge lines. Never jump abruptly.
16. **No geography-specific references unless appropriate.** Follow CLAUDE.md guidance.
17. **Max 7 text overlays per script.** Inside visual direction blocks only, never between dialogue lines.
18. **Cross-check "do" vs "don't" sections for contradictions.** Every "do this" must be consistent with every "don't do this."
19. **No overstated measurements.** Don't add casual approximations that misrepresent ranges.
20. **For dangerous practices, cover ALL major risks.** Don't just mention one or two.

### Consistency Rules (21-24)

21. **Never rubber-stamp claims as VERIFIED.** Actually check the source.
22. **Scientific/technical claims must be internally consistent.** No contradictions within the same script.
23. **When changing ANY script line, update ALL supporting sections.** Description, editorial review, fact-check, timestamps must match the final script.
24. **Hook style should use clickbait formula.** Emotional imagery, personal blame, curiosity gaps, fear/stress triggers. Conversational energy, not robotic.

---

# PRE-WRITING CHECKLIST (MANDATORY)

Complete before drafting any script:

1. [ ] Read CLAUDE.md for brand context, audience, keywords
2. [ ] Read the error log (`memory/script-errors-log.md`) if one exists
3. [ ] Read the product file(s) — note exact name, exact description, exact "How to Use"
4. [ ] Cross-reference every item in the brief against the product catalog — identify ALL relevant products
5. [ ] Confirm product is in stock
6. [ ] Confirm hook directly matches the video's topic
7. [ ] Confirm listicle count is odd (if applicable)
8. [ ] Confirm no multiplier promises in hook
9. [ ] Plan max 2 product mentions (1 body + 1 CTA reminder)

# POST-WRITING CHECKLIST (MANDATORY)

Verify before delivering any script:

1. [ ] Re-read every line out loud — if it sounds like a textbook, rewrite it
2. [ ] Cross-check "do" vs "don't" sections for contradictions
3. [ ] Verify all product names/attributes match product file exactly
4. [ ] Verify care instructions match product's "How to Use" exactly
5. [ ] Confirm max 2 product mentions (1 body + 1 CTA)
6. [ ] Confirm CTA has brief features (no specs) + product link reminder
7. [ ] Confirm every list item has spoken numbered transition
8. [ ] Confirm max 7 text overlays, all inside visual direction blocks
9. [ ] Confirm hook directly matches topic
10. [ ] Confirm no jargon, no multiplier promises, no pricing
11. [ ] Confirm all supporting sections consistent with final script
12. [ ] Confirm all items cross-referenced against product catalog

---

# ERROR LOGGING SYSTEM

This skill maintains a persistent error log per project at `memory/script-errors-log.md`.

### How It Works

1. **Before writing any new script:** Read `memory/script-errors-log.md` if it exists. Every rule in the log applies to the current script.
2. **When the user identifies an error:** Log it immediately with:
   - Which script had the error
   - What the error was (specific example)
   - The rule created to prevent it
3. **Format for each error entry:**
```
### [Error #]: [Brief description]
- **Script:** [Script name/number]
- **What went wrong:** [Specific example]
- **Rule:** [The rule to prevent this in future]
```
4. **Append a Pre-Writing Checklist** at the bottom of the error log, updated with each new rule.

The error log is a continuously improving quality system. Errors caught once should never repeat. Each new project starts with a clean log.

---

# RULE OVERRIDE SYSTEM

Projects can override any universal rule by adding a `## Script Rule Overrides` section to their CLAUDE.md.

### How to Override

```markdown
## Script Rule Overrides

### Rule 2 Override: Max Product Mentions
- **Default:** Max 2 product mentions (1 body + 1 CTA)
- **Override:** Max 3 product mentions for product showcase videos only

### Rule 13 Override: Listicle Numbers
- **Default:** Always use odd numbers (3, 5, 7, 9)
- **Override:** Even numbers allowed for "Top 10" format videos

### Custom Rule: [Rule Name]
- **Rule:** [Description of project-specific rule]
```

### Override Priority
1. **Project CLAUDE.md overrides** (highest priority)
2. **Project error log rules** (accumulated from past errors)
3. **Universal skill rules** (this file — lowest priority, always applies unless overridden)

---

# PRODUCTION CONTEXT

Read these settings from CLAUDE.md `## Production Context`:

- **Speaker:** Name of the on-camera host/narrator
- **Setting:** Where videos are shot (studio, garden, kitchen, etc.)
- **Greeting format:** How the host opens videos (e.g., "Hi, everyone. Welcome back to [Brand].")
- **Reference script:** Path to a gold-standard script for tone and structure
- **Brand sign-off:** How videos end (e.g., "happy gardening!", "see you next time!")
- **Jargon ban list:** Domain-specific terms to avoid (the audience wouldn't understand them)
