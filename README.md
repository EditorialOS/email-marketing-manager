# Email Marketing Manager

**v2.0** · **Docs:** [PRD](PRD.md) · [Changelog](CHANGELOG.md)

Draft newsletters from your real documents — brand guide, audience personas, past issues, and performance data. Not a template library — a production system that reads your Box folder, selects verified images from Cloudinary, writes client-specific copy with segment variants, scores output through a 5-gate editorial review, posts drafts to Beehiiv, and learns from every send.

## What It Does

Most newsletter tools give you a blank editor and a send button. The strategy — what angle to take, which segments to vary, what subject line to test, why last week's issue underperformed — lives in the marketer's head. When that person leaves, the knowledge leaves with them.

This plugin externalizes that knowledge. Every `/create` reads your brand context and past performance. Every `/track` extracts specific learnings and writes them back to Box. Every subsequent `/create` reads those learnings and gets smarter. The institutional knowledge compounds in plain markdown files that any team member can read, and any future run can apply.

### The workflow

1. System reads your Box folder (brand guide, audience, past newsletters, learnings)
2. System queries Cloudinary for verified newsletter images (closed candidate list — no hallucinated URLs)
3. System drafts newsletter with subject line, body copy, CTA, image selections, and segment variants
4. Editorial gate scores the draft across 5 dimensions (voice, angle, structure, image integrity, segment fit)
5. You review the draft — approve, edit, adjust
6. Draft posts to Beehiiv (or you copy-paste if not connected)
7. Track results after 48 hours — learnings feed back into the next draft

### The learning loop

Every `/create` generates a newsletter with a performance prediction. Every `/track` logs results and extracts specific learnings — which subject line patterns drive opens, which CTAs drive clicks, which segments respond to which angles. Every subsequent `/create` reads those learnings and applies them.

By issue 10, the system knows things about your newsletter performance that your team may not have noticed, because it cross-references every variable (subject line pattern × segment × send time × angle) without forgetting.

No email template tool does this.

## Commands

### /setup
Connect your Box folder, Cloudinary library, and Beehiiv account. Three questions, 60 seconds. Optional — `/create` also works without it.

```
/setup
```

### /run
Inspect the current state — standing orders, topic queue, learning files, and gaps — then decide the next best action. The operator command that makes the system feel like a teammate.

```
/run
```

### /create
Draft the next newsletter. Queries Cloudinary for images, produces subject line, preview text, body copy, CTA, image manifest, segment-specific variants, performance prediction, and editorial gate scores.

```
/create Topic: spring sale
/create Topic: product launch, Segment: past customers
/create Topic: weekly roundup
```

### /track
Log results and update the learning memory. Pulls metrics from Beehiiv automatically, or accepts manual input. Every tracked newsletter makes the next `/create` smarter.

```
/track Newsletter: spring sale
/track Newsletter: spring sale, Notes: "subject line A won the A/B test"
```

## Install

```
/plugin marketplace add EditorialOS/editorial-os
/plugin install email-marketing-manager@editorialos
```

## Connector Stack

| Connector | Job | What It Does |
|-----------|-----|--------------|
| **Cloudinary** | Images | Verified image selection via closed candidate list — no broken URLs |
| **Box** | Documents | Brand guide, personas, past newsletters, learning files |
| **Beehiiv** | Email | Post drafts, pull send metrics, subscriber data |

See [CONNECTORS.md](CONNECTORS.md) for degradation behavior at each level.

## Example Usage

**Example 1:** Run `/setup` to connect your Box folder and Cloudinary library. The system scans for your brand guide, audience personas, past newsletters — then confirms what it found and how many Cloudinary images are available.

**Example 2:** Run `/create Topic: spring product launch` to draft a full newsletter with subject line options, body copy, CTA, verified Cloudinary image selections, and segment-specific variants. The editorial gate scores the draft before it posts.

**Example 3:** Run `/track Newsletter: spring product launch` after 48 hours. The system pulls metrics from Beehiiv, compares actual open and click rates to its prediction, extracts learnings, and saves them to Box.

**Example 4:** Run `/create Topic: customer spotlight` for the next issue. This time, the system reads learnings from the tracked spring launch — avoiding the subject line pattern that underperformed and leaning into the CTA style that drove clicks.

**Example 5:** Run `/run` to inspect the current state. The system checks your topic queue, standing orders, learning files, and context documents, then recommends the next best action.

## The Weekly Loop

**Monday** — Run `/track`. Compare actual performance against the prior prediction. Extract learnings and update baselines.

**Tuesday** — Run `/run`. Inspect standing orders, queue, and current context to choose the next best action.

**Drafting** — Run `/create`. Draft the newsletter, generate segment variants, score through editorial gate, predict performance, and save the record.

**Human gate** — Approve draft, subject line, and send in Beehiiv.

## Skills

- **client-context** — Reads your Box folder and Cloudinary library and builds structured newsletter context: brand voice, audience segments, content history, verified image inventory, and performance data.
- **email-strategist** — Newsletter content creation methodology: angle selection, Cloudinary closed-list image selection, subject line writing, body copy structure by goal, segment variant generation, and the substitution test.
- **performance-learning** — The learning loop engine. Tracks newsletter results, extracts specific learnings, updates baselines, and feeds intelligence back into future predictions.

## Folder Structure

```
Box — Client Brand Folder/
├── brand-guide.md
├── audience-personas.md
├── past-newsletters/
├── performance/
├── newsletter-log.md          ← written by /track
├── newsletter-learnings.md    ← written by /track
└── newsletter-baselines.md    ← written by /track

Cloudinary — your image library
├── organized by folder, tag, or campaign
└── (images queried at /create time, not stored in Box)
```

## Part of Editorial OS

Built from 20 years of editorial operations across WIRED, Amazon, Sunset, and the Los Angeles Times.

## License

Apache 2.0 — see [LICENSE](LICENSE).
