---
name: client-context
description: Reads the client's Box folder and Cloudinary library and builds structured newsletter context. Extracts brand voice, audience segments, past newsletter patterns, performance data, and available images. Called automatically at the start of every command. Shared architecture with Editorial OS — same document folder, different lens.
---

# Client Context — Newsletter Intelligence

## Purpose

Read the client's real documents and build the context layer that makes every newsletter client-specific instead of generic. This is the skill that replaces prompt templates and SOPs — the documents ARE the config.

A prompt playbook says "upload your brand assets." This skill reads them automatically, extracts structured intelligence, and carries that intelligence across every command without the user repeating themselves.

## When This Activates

Every `/email-marketing-manager:create` and `/email-marketing-manager:track` command starts here. Load context silently — do not narrate the loading process to the user. Show a one-line status header and move to the command's work.

Never say "I'm loading your context" or "Let me read your documents." Just read them and show the status header. The user sees the result, not the process.

## Priority Documents

Read the client's Box folder. Look for these document types in priority order:

| Priority | Document Type | What to Extract | If Missing |
|:--------:|--------------|-----------------|------------|
| 1 | Brand guide / style guide | Voice attributes, tone rules, vocabulary (use/avoid), formatting preferences, greeting/sign-off patterns | Ask for 2-3 adjectives describing brand voice + one example email |
| 2 | Audience personas | Segment names, pain points, content preferences, email behavior patterns, segment sizes | Ask how many segments and one sentence about each |
| 3 | Past newsletters | Subject lines used, angles tried, formats that worked, hooks that opened well, typical length, greeting style, sign-off style, image usage patterns | First newsletter will be baseline — no history to reference |
| 4 | Performance data / reports | Open rates, click rates, best send times, segment-level metrics, seasonal patterns, A/B test results | Use industry benchmarks, state they're benchmarks |
| 5 | Content strategy / marketing plan | Newsletter goals, brand positioning, competitive context, seasonal priorities, content pillars | Ask for primary goal of newsletter program |
| 6 | Newsletter learning files | newsletter-log.md, newsletter-learnings.md, newsletter-baselines.md — written by /email-marketing-manager:track | No learning history. First newsletter establishes baseline. |

### Box MCP Tools

Use the Box MCP tools to read client documents:

- `search_files_keyword` — find documents by name or content keyword (brand guide, personas, newsletters)
- `list_folder_content_by_folder_id` — list everything in the client's folder
- `get_file_content` — read document text (supports .md, .txt, .docx, .pdf)
- `get_file_details` — check file metadata, modification dates

**Reading order:** List the client folder first to see what's there. Then read documents in priority order. Don't read every file — read what the priority table says matters.

## Image Library — Cloudinary

Images do NOT live in the document folder. They live in Cloudinary.

When context loads, query Cloudinary for the client's available assets:

- `search-assets` — find images by tag, folder, or metadata
- `get-asset-details` — get dimensions, format, delivery URL for a specific asset
- `list-images` — browse the image library

Build the image inventory:

| Field | Source |
|-------|--------|
| Asset ID | Cloudinary `public_id` |
| Delivery URL | Cloudinary CDN URL |
| Dimensions | `width` × `height` from asset details |
| Format | jpg, png, webp |
| Tags | Cloudinary tags (product, lifestyle, headshot, etc.) |
| Created | Upload date |

This inventory becomes the **closed candidate list** that the email-strategist skill selects from. The drafting step may only reference images that appear in this list.

### Image-performance correlation

If newsletter learning files exist, cross-reference:
- Which asset IDs appeared in high-performing newsletters?
- Which image categories (by tag) correlated with higher engagement?
- Which images have been used recently? (Avoid hero reuse within 3 newsletters.)

## Document Recognition

Documents don't always have clean titles. Use content to identify type:

| Content Signals | Document Type |
|----------------|---------------|
| Voice attributes, tone descriptions, word lists, "our brand sounds like" | Brand guide |
| Demographic details, segment names, pain points, "our audience" | Audience personas |
| Subject lines, email body text, send dates, greeting/sign-off patterns | Past newsletters |
| Open rates, click rates, subscriber counts, "performance" | Performance data |
| Goals, pillars, competitive mentions, calendar, "strategy" | Content strategy |
| "Newsletter:" entries with dates and metrics, chronological | Newsletter log (from /email-marketing-manager:track) |
| Categorized learnings about angles, segments, timing | Newsletter learnings (from /email-marketing-manager:track) |
| Baseline metrics per segment, angle effectiveness matrix | Newsletter baselines (from /email-marketing-manager:track) |

### Ambiguous Documents

If a document serves multiple purposes (e.g., a brand guide that includes audience personas), extract all relevant information. Don't force documents into single categories.

If two documents contain conflicting information:
- For voice: past newsletters are ground truth. They show how the brand actually sounds, not how it aspires to sound.
- For segments: the personas doc is ground truth.
- For performance: newsletter-baselines.md (from /email-marketing-manager:track) is ground truth if it exists.
- For goals: the most recent document wins.

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
- **Segment-specific learnings** — from newsletter-learnings.md if it exists
- **Engagement tier** — if data exists: highly engaged, occasional, dormant

### Newsletter History

- **Last 5-10 newsletters** — subject lines, angles, send times, performance
- **Angle inventory** — what hooks have been used? Categorize by type
- **Repeat check** — which angles were used in the last 4 newsletters? Off-limits for next /email-marketing-manager:create.
- **Best performers** — top 3 newsletters by open rate and by click rate. What did they have in common?
- **Worst performers** — bottom 3, with hypotheses on why
- **Seasonal patterns** — do certain months or seasons drive different performance?
- **Image usage history** — which newsletters used images? Did image newsletters outperform text-only? Which Cloudinary asset categories correlated with higher engagement?
- **Length patterns** — average word count of top performers vs. worst performers

### Performance Baselines

- **Overall** — average open rate, click rate, unsubscribe rate
- **By segment** — baseline metrics per segment
- **By day/time** — which send windows perform best?
- **By angle type** — do certain hooks outperform?
- **By format** — long vs. short, image vs. text-only, single-CTA vs. multi-CTA
- **Trend** — improving, declining, or flat over the last 5-10 newsletters?
- **Newsletter count** — determines prediction confidence

| Tracked Count | Confidence | Baseline Reliability |
|:---:|:---:|---|
| 0 | Baseline | Industry benchmarks only |
| 1-2 | Low | Directional. Wide variance expected. |
| 3-7 | Medium | Segment-level patterns emerging. |
| 8-15 | High | Reliable predictions. Cross-variable patterns visible. |
| 16+ | Very High | Full intelligence. Confident recommendations. |

### Learning History (from /email-marketing-manager:track)

- **Cumulative learnings** — every specific fact recorded by past /email-marketing-manager:track runs
- **Confidence level** — based on newsletter count
- **Last updated** — when was the most recent /email-marketing-manager:track run?
- **Stale data flag** — if last /email-marketing-manager:track was 60+ days ago, note it
- **Learning count** — how many individual learnings recorded?
- **Learning categories present** — which categories have data?

## Freshness Checks

| Condition | Action |
|-----------|--------|
| Performance data > 90 days old | Note: "Baselines are from [date] — recent results may differ." |
| Past newsletters > 6 months old with nothing recent | Note: "Newsletter history is stale — first /email-marketing-manager:create establishes new patterns." |
| Cloudinary library unchanged for 90+ days | Note: "Image library hasn't been updated recently. Consider adding fresh visuals." |
| Learning files last updated 60+ days ago | Note: "Learning data is aging. Run /email-marketing-manager:track on recent sends to refresh." |
| Brand guide last modified > 1 year ago | Note: "Brand guide may be outdated. If voice has evolved, consider updating." |

## Connector Awareness

| Connector | If Available | If Unavailable |
|-----------|-------------|----------------|
| Box | Read all documents automatically. Write learning files back. Full context. | Ask user to paste brand context and describe audience. Learning loop won't persist between sessions. |
| Cloudinary | Query image library. Build verified closed candidate list. Image-performance correlation. | No verified images. Newsletter will be text-only. Suggest what images would strengthen output. |
| Beehiiv | Pull real send metrics for /email-marketing-manager:track. Post drafts for /email-marketing-manager:create. Subscriber counts for segment sizing. | User pastes metrics manually. Copies newsletter to paste into Beehiiv. Still works — just manual. |

### Degradation Behavior

The plugin works at every level of connectivity:

| Level | What's Connected | System Capability |
|:---:|---|---|
| Full | Cloudinary + Box + Beehiiv | Complete: verified images, reads context, posts drafts, pulls metrics, learning loop persists |
| Docs + Images | Cloudinary + Box | Strong: verified images, reads context, writes newsletters, saves records. Manual metrics, manual draft posting. |
| Docs only | Box | Moderate: reads context, no verified images. Manual metrics, manual draft posting. |
| Manual | Nothing | Functional: user pastes brand context and examples. No persistent learning. No verified images. |

Never block a command because connectors are missing. Degrade gracefully. State what's missing and what it costs — then do the best work possible with what's available.

## Status Header

Show one line at the top of every command output:

- 🟢 `Config: Connected — [list of document types found] — [N] Cloudinary images available — Beehiiv active` (full context)
- 🟡 `Config: Partial — [what's found], missing [what's not]` (some connectors active)
- ⚪ `Config: Manual — provide brand context and audience details` (no connectors)

## Cross-Plugin Compatibility

This skill follows the same architecture as Editorial OS's client-context skill. If a user has both plugins installed pointing at the same Box folder, the same documents serve both — Editorial OS reads them for content strategy, Email Marketing Manager reads them for newsletters. One folder, multiple plugins, no duplication.

### Shared vs. Plugin-Specific Files

| File | Shared (both plugins read) | Plugin-specific |
|------|:---:|:---:|
| Brand guide | ✅ | |
| Audience personas | ✅ | |
| Content strategy | ✅ | |
| Past newsletters | | ✅ Email Marketing Manager |
| newsletter-log.md | | ✅ Written by /email-marketing-manager:track |
| newsletter-learnings.md | | ✅ Written by /email-marketing-manager:track |
| newsletter-baselines.md | | ✅ Written by /email-marketing-manager:track |

The newsletter-specific files are written by /email-marketing-manager:track and read by this skill. They live alongside the brand documents in the same Box folder. The user can read and edit them — transparency is a feature.
