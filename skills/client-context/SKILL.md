---
name: client-context
description: Reads the client's Google Drive folder and builds structured newsletter context. Extracts brand voice, audience segments, past newsletter patterns, performance data, and available images. Called automatically at the start of every command. Shared architecture with Editorial OS — same Drive folder, different lens.
---

# Client Context — Newsletter Intelligence

## Purpose

Read the client's real documents and build the context layer that makes every newsletter client-specific instead of generic. This is the skill that replaces prompt templates and SOPs — the documents ARE the config.

A prompt playbook says "upload your brand assets." This skill reads them automatically, extracts structured intelligence, and carries that intelligence across every command without the user repeating themselves.

## When This Activates

Every `/create` and `/track` command starts here. Load context silently — do not narrate the loading process to the user. Show a one-line status header and move to the command's work.

Never say "I'm loading your context" or "Let me read your documents." Just read them and show the status header. The user sees the result, not the process.

## Priority Documents

Read the ~~docs folder. Look for these document types in priority order:

| Priority | Document Type | What to Extract | If Missing |
|:--------:|--------------|-----------------|------------|
| 1 | Brand guide / style guide | Voice attributes, tone rules, vocabulary (use/avoid), formatting preferences, greeting/sign-off patterns | Ask for 2-3 adjectives describing brand voice + one example email |
| 2 | Audience personas | Segment names, pain points, content preferences, email behavior patterns, segment sizes | Ask how many segments and one sentence about each |
| 3 | Past newsletters | Subject lines used, angles tried, formats that worked, hooks that opened well, typical length, greeting style, sign-off style, image usage patterns | First newsletter will be baseline — no history to reference |
| 4 | Performance data / reports | Open rates, click rates, best send times, segment-level metrics, seasonal patterns, A/B test results | Use industry benchmarks, state they're benchmarks |
| 5 | Images folder | Available images — product shots, headshots, lifestyle photos, logos, campaign assets. Inventory what exists with filenames and rough descriptions | Newsletter will be text-only. Suggest what images would strengthen output. |
| 6 | Content strategy / marketing plan | Newsletter goals, brand positioning, competitive context, seasonal priorities, content pillars | Ask for primary goal of newsletter program |
| 7 | Newsletter learning files | newsletter-log.md, newsletter-learnings.md, newsletter-baselines.md — written by /track | No learning history. First newsletter establishes baseline. |

## Document Recognition

Documents don't always have clean titles. Use content to identify type:

| Content Signals | Document Type |
|----------------|---------------|
| Voice attributes, tone descriptions, word lists, "our brand sounds like" | Brand guide |
| Demographic details, segment names, pain points, "our audience" | Audience personas |
| Subject lines, email body text, send dates, greeting/sign-off patterns | Past newsletters |
| Open rates, click rates, subscriber counts, "performance" | Performance data |
| Image files (.jpg, .png, .gif, .webp) in a subfolder | Images folder |
| Goals, pillars, competitive mentions, calendar, "strategy" | Content strategy |
| "Newsletter:" entries with dates and metrics, chronological | Newsletter log (from /track) |
| Categorized learnings about angles, segments, timing | Newsletter learnings (from /track) |
| Baseline metrics per segment, angle effectiveness matrix | Newsletter baselines (from /track) |

### Ambiguous Documents

If a document serves multiple purposes (e.g., a brand guide that includes audience personas, or a strategy doc with performance data embedded), extract all relevant information. Don't force documents into single categories.

If two documents contain conflicting information:
- For voice: past newsletters are ground truth. They show how the brand actually sounds, not how it aspires to sound.
- For segments: the personas doc is ground truth. Past newsletters may serve segments inconsistently.
- For performance: newsletter-baselines.md (from /track) is ground truth if it exists. Manual performance docs may be outdated or selectively reported.
- For goals: the most recent document wins. A 2026 strategy doc overrides a 2025 marketing plan.

If a document's purpose is genuinely unclear, note what was found and how it was used. Don't discard ambiguous documents — extract what's useful and flag uncertainty.

## Context Assembly

After reading, assemble structured context in this order:

### Brand Voice

| Dimension | Where to Find It | Fallback |
|-----------|------------------|----------|
| Core attributes | Brand guide ("our voice is...") | Ask for 2-3 adjectives |
| Newsletter tone | Past newsletters (actual voice used) | Default to brand guide attributes |
| Vocabulary — use | Brand guide word list | No default — write naturally |
| Vocabulary — avoid | Brand guide banned words | Avoid generic AI language: "unlock, unleash, leverage, dive into, game-changer" |
| Greeting style | Past newsletters (first line pattern) | No greeting — open cold |
| Sign-off style | Past newsletters (closing pattern) | "— [brand name or person name]" |
| Emoji usage | Past newsletters (are emojis present?) | No emojis |
| Punctuation | Past newsletters (em dashes, Oxford commas, exclamation points) | Standard punctuation, no exclamation points |

**Critical rule:** If past newsletters exist, they define the newsletter voice — not the brand guide. The brand guide describes intent. Past newsletters show reality. When they conflict, match reality.

**Voice extraction method:** Read the 3 most recent newsletters. Identify:
1. Average sentence length (short fragments = casual, compound sentences = formal)
2. First-person usage ("I" = personal brand, "we" = company voice, neither = editorial)
3. Question frequency (questions in every newsletter = conversational, no questions = declarative)
4. Paragraph length (1-2 sentences = scannable, 3-5 = traditional)
5. Opening pattern (hook, greeting, question, statement — which does this brand use?)
6. Closing pattern (CTA only, personal sign-off, P.S. section, multiple CTAs)

These six signals define the voice more accurately than any adjective list.

### Audience Segments

For each segment:
- **Name and description** — who they are in one sentence
- **Email behavior** — how they engage (quick scanners vs. deep readers, mobile vs. desktop, reply behavior)
- **Pain points** — what problems does this brand solve for them? Ranked by urgency.
- **Content preferences** — what hooks resonate? What length works? What CTAs convert?
- **Segment size** — if available, approximate subscriber count per segment
- **Segment-specific learnings** — from newsletter-learnings.md if it exists. What has /track recorded about this segment's behavior?
- **Engagement tier** — if data exists, categorize: highly engaged (opens most newsletters), occasional (opens some), dormant (rarely opens)

**Segment intelligence depth by data availability:**

| Data Available | Segment Intelligence Level |
|:---:|---|
| Personas doc only | Basic — pain points, preferences, demographics. Enough for initial variants. |
| Personas + past newsletters | Moderate — can see which segments were targeted historically, what language was used |
| Personas + past newsletters + learning files | Deep — knows which angles work per segment, optimal length, CTA preferences, timing |
| All above + ~~email metrics | Full — real open/click per segment, behavioral patterns, trend data |

### Newsletter History

- **Last 5-10 newsletters** — subject lines, angles, send times, performance
- **Angle inventory** — what hooks have been used? Categorize by type:

| Angle Type | Last Used | Times Used | Avg Performance |
|-----------|-----------|:----------:|:---------------:|
| Problem-first | [date] | [N] | [vs. baseline] |
| Curiosity gap | [date] | [N] | [vs. baseline] |
| Contrarian | [date] | [N] | [vs. baseline] |
| Personal/story | [date] | [N] | [vs. baseline] |
| Urgency | [date] | [N] | [vs. baseline] |
| Social proof | [date] | [N] | [vs. baseline] |
| Educational | [date] | [N] | [vs. baseline] |
| Direct value | [date] | [N] | [vs. baseline] |

- **Repeat check** — which angles were used in the last 4 newsletters? These are off-limits for the next /create.
- **Best performers** — top 3 newsletters by open rate and by click rate. What did they have in common? (Angle type? Length? Image usage? Send time?)
- **Worst performers** — bottom 3, with hypotheses on why. What should be avoided?
- **Seasonal patterns** — do certain months, events, or seasons drive different performance?
- **Image usage history** — which newsletters used images? Did image newsletters outperform text-only? Which image types correlated with higher engagement?
- **Length patterns** — average word count of top performers vs. worst performers. Is there a sweet spot?

### Performance Baselines

- **Overall** — average open rate, click rate, unsubscribe rate across all newsletters
- **By segment** — baseline metrics per segment (from newsletter-baselines.md or manual data)
- **By day/time** — which send windows perform best?
- **By angle type** — do certain hooks outperform? Ranked by open rate and by click rate.
- **By format** — long vs. short, image vs. text-only, single-CTA vs. multi-CTA
- **Trend** — are metrics improving, declining, or flat over the last 5-10 newsletters?
- **Newsletter count** — how many newsletters have been tracked? This determines prediction confidence:

| Tracked Count | Confidence | Baseline Reliability |
|:---:|:---:|---|
| 0 | Baseline | Industry benchmarks only |
| 1-2 | Low | Directional. Wide variance expected. |
| 3-7 | Medium | Segment-level patterns emerging. Angle preferences detectable. |
| 8-15 | High | Reliable predictions. Cross-variable patterns visible. |
| 16+ | Very High | Full intelligence. Confident recommendations. |

### Image Library

- **Available images** — filenames, rough descriptions, categories:

| Category | Examples | Typical Use |
|----------|---------|------------|
| Product | Product shots, packaging, features | Product launch newsletters, sales |
| Lifestyle | People using product, aspirational scenes | Brand building, storytelling |
| Headshot | Founder, team, spokesperson | Personal newsletters, about-us |
| Logo | Brand marks, icons | Headers, footers |
| Illustration | Custom graphics, diagrams | Educational newsletters |
| Seasonal | Holiday, seasonal imagery | Timely newsletters |

- **Image-performance correlation** — from learning files: which image categories appeared in high-performing newsletters?
- **Freshness** — when were images last added? If unchanged for 90+ days, flag: "Image library hasn't been updated. Consider adding fresh visuals."
- **Reuse tracking** — which images have been used recently? Avoid using the same hero image within 3 newsletters.
- **Format notes** — flag images that may not work well in email (very large files, unusual formats, portrait orientation for hero placement)

### Learning History (from /track)

- **Cumulative learnings** — every specific fact recorded by past /track runs
- **Confidence level** — based on newsletter count
- **Last updated** — when was the most recent /track run?
- **Stale data flag** — if last /track was 60+ days ago, note: "Learning data is aging — recent sends may show different patterns."
- **Learning count** — how many individual learnings have been recorded? More learnings = richer context for /create decisions.
- **Learning categories present** — which categories have data? (Angles, segments, timing, images, subject lines, CTAs). Missing categories = gaps in intelligence.

## Freshness Checks

| Condition | Action |
|-----------|--------|
| Performance data > 90 days old | Note: "Baselines are from [date] — recent results may differ." |
| Past newsletters > 6 months old with nothing recent | Note: "Newsletter history is stale — first /create establishes new patterns." |
| Images folder unchanged for 90+ days | Note: "Image library hasn't been updated recently. Consider adding fresh visuals." |
| Learning files last updated 60+ days ago | Note: "Learning data is aging. Run /track on recent sends to refresh." |
| Brand guide last modified > 1 year ago | Note: "Brand guide may be outdated. If voice has evolved, consider updating." |
| Audience personas with no segment-level performance data | Note: "Segment definitions exist but no tracked performance per segment. Run /track to build segment intelligence." |

## Connector Awareness

| Connector | If Available | If Unavailable |
|-----------|-------------|----------------|
| ~~docs | Read all documents + images automatically. Write learning files back. Full context. | Ask user to paste brand context and describe images available. Learning loop won't persist between sessions. |
| ~~email | Pull real send metrics for /track. Post drafts for /create. Subscriber counts for segment sizing. | User pastes metrics manually. Copies newsletter to paste into email platform. Still works — just manual. |

### Degradation Behavior

The plugin works at every level of connectivity:

| Level | What's Connected | System Capability |
|:---:|---|---|
| Full | ~~docs + ~~email | Complete: reads context, writes newsletters, posts drafts, pulls metrics, learning loop persists |
| Docs only | ~~docs | Strong: reads context, writes newsletters, saves records. User pastes metrics for /track. |
| Manual | Nothing | Functional: user pastes brand context and past examples. Newsletter quality depends on what's provided. No persistent learning. |

Never block a command because connectors are missing. Degrade gracefully. State what's missing and what it costs — then do the best work possible with what's available.

## Status Header

Show one line at the top of every command output:

- 🟢 `Config: Connected — [list of document types found] — [N] images available` (full context)
- 🟡 `Config: Partial — [what's found], missing [what's not]` (some docs found)
- ⚪ `Config: Manual — provide brand context and audience details` (no ~~docs)

## Cross-Plugin Compatibility

This skill follows the same architecture as Editorial OS's client-context skill. If a user has both plugins installed pointing at the same Drive folder, the same documents serve both — Editorial OS reads them for content strategy, Email Marketing Manager reads them for newsletters. One folder, multiple plugins, no duplication.

### Shared vs. Plugin-Specific Files

| File | Shared (both plugins read) | Plugin-specific |
|------|:---:|:---:|
| Brand guide | ✅ | |
| Audience personas | ✅ | |
| Content strategy | ✅ | |
| Past newsletters | | ✅ Email Marketing Manager |
| Images folder | | ✅ Email Marketing Manager |
| newsletter-log.md | | ✅ Written by /track |
| newsletter-learnings.md | | ✅ Written by /track |
| newsletter-baselines.md | | ✅ Written by /track |

The newsletter-specific files are written by /track and read by this skill. They live alongside the brand documents in the same Drive folder. The user can read and edit them — transparency is a feature.

## Teammate Protocol Compatibility

This skill works identically in both modes:

**Plugin mode (Cowork):** Reads from ~~docs (Google Drive via MCP). User triggers /create and /track manually.

**Teammate mode (OpenClaw VPS):** Reads from workspace/ (synced from Google Drive by runtime.py). Cron job triggers automatically per standing orders.

Same skill. Same document reading logic. Same context assembly. Different trigger, different file path, same output quality.
