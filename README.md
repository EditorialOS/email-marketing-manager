# Email Marketing Manager

**Docs:** [PRD](PRD.md) · [Changelog](CHANGELOG.md)

Draft newsletters from your real documents — brand guide, audience personas, past issues, and performance data. Not a template library — a production system that reads your Google Drive folder, writes client-specific copy with segment variants, predicts performance, and learns from every send.

## What It Does

Most newsletter tools give you a blank editor and a send button. The strategy — what angle to take, which segments to vary, what subject line to test, why last week's issue underperformed — lives in the marketer's head. When that person leaves, the knowledge leaves with them.

This plugin externalizes that knowledge. Every `/create` reads your brand context and past performance. Every `/track` extracts specific learnings and writes them back to Drive. Every subsequent `/create` reads those learnings and gets smarter. The institutional knowledge compounds in plain markdown files that any team member can read, and any future run can apply.

### The workflow

1. System reads your Google Drive folder (brand guide, audience, past newsletters, learnings)
2. System drafts newsletter with subject line, body copy, CTA, image selections, and segment variants
3. You review the draft — approve, edit, adjust
4. Send via your email platform
5. Track results after 48 hours — learnings feed back into the next draft

Content in, newsletter out, human quality gate, send.

### The learning loop

Every `/create` generates a newsletter with a performance prediction. Every `/track` logs results and extracts specific learnings — which subject line patterns drive opens, which CTAs drive clicks, which segments respond to which angles. Every subsequent `/create` reads those learnings and applies them.

By issue 10, the system knows things about your newsletter performance that your team may not have noticed, because it cross-references every variable (subject line pattern × segment × send time × angle) without forgetting.

No email template tool does this.

## Commands

### /setup
Connect your Google Drive folder and establish newsletter context. Three questions, 60 seconds. Optional — `/create` also works without it.

```
/setup
```

### /run
Inspect the current state — standing orders, topic queue, learning files, and gaps — then decide the next best action. The operator command that makes the system feel like a teammate.

```
/run
```

### /create
Draft the next newsletter. Produces subject line, preview text, body copy, CTA, image selections, segment-specific variants, and a performance prediction.

```
/create Topic: spring sale
/create Topic: product launch, Segment: past customers
/create Topic: weekly roundup
```

### /track
Log results and update the learning memory. Every tracked newsletter makes the next `/create` smarter — better predictions, better angles, better timing.

```
/track Newsletter: spring sale
/track Newsletter: spring sale, Notes: "subject line A won the A/B test"
```

## Install

```
/plugin marketplace add EditorialOS/email-marketing-manager
/plugin install email-marketing-manager@email-marketing-manager
```

## Example Usage

**Example 1:** Run `/setup` to connect your Google Drive folder. The system scans for your brand guide, audience personas, past newsletters, and images — then confirms what it found and what's missing.

**Example 2:** Run `/create Topic: spring product launch` to draft a full newsletter with subject line options, body copy, CTA, image selections from your Drive folder, and segment-specific variants for new vs. returning customers.

**Example 3:** Run `/track Newsletter: spring product launch` after 48 hours with your email platform's results. The system compares actual open and click rates to its prediction, extracts learnings about what worked, and saves them to Drive.

**Example 4:** Run `/create Topic: customer spotlight` for the next issue. This time, the system reads learnings from the tracked spring launch — avoiding the subject line pattern that underperformed and leaning into the CTA style that drove clicks.

**Example 5:** Run `/run` to inspect the current state. The system checks your topic queue, standing orders, learning files, and context documents, then recommends the next best action — draft, track, or surface a decision you need to make.

## The Weekly Loop

**Monday** — Run `/track`. Compare actual performance against the prior prediction. Extract learnings and update baselines.

**Tuesday** — Run `/run`. Inspect standing orders, queue, and current context to choose the next best action.

**Drafting** — Run `/create`. Draft the newsletter, generate segment variants, predict performance, and save the record.

**Human gate** — Approve draft, subject line, and send.

## Skills

- **client-context** — Reads your Google Drive folder and builds structured newsletter context: brand voice, audience segments, content history, image inventory, and performance data. Called automatically at the start of every command.
- **email-strategist** — Newsletter content creation methodology: angle selection, subject line writing, body copy structure by goal, segment variant generation, and the substitution test that catches generic voice.
- **performance-learning** — The learning loop engine. Tracks newsletter results, extracts specific learnings, updates baselines, and feeds intelligence back into future predictions.

## Drive Protocol

Same Drive folder serves [Editorial OS](https://github.com/EditorialOS/editorial-os) (content strategy), [Pinterest Marketing Strategist](https://github.com/EditorialOS/pinterest-marketing-strategist) (Pinterest pins), and this plugin (newsletters). Shared: brand guide, audience personas, content strategy. Newsletter-specific: newsletter-log.md, newsletter-learnings.md, newsletter-baselines.md.

```
Client Brand Folder/
├── brand-guide.md
├── audience-personas.md
├── past-newsletters/
├── images/
├── performance/
├── newsletter-log.md          ← written by /track
├── newsletter-learnings.md    ← written by /track
└── newsletter-baselines.md    ← written by /track
```

## Connectors

- **Google Drive** (required) — reads brand context and learning files
- **Email platform** (optional) — post drafts, pull send metrics automatically
- **Google Calendar** (optional) — seasonal timing and send cadence alignment

See [CONNECTORS.md](CONNECTORS.md) for degradation behavior at each level.

## Autonomous Mode

The same skills run autonomously via standing orders on Perplexity Computer or OpenClaw VPS. Plugin = manual. Teammate = autonomous. Same skills, same output, same learning loop.

## Part of Editorial OS

Built from 20 years of editorial operations across WIRED, Amazon, Sunset, and the Los Angeles Times.

## License

Apache 2.0 — see [LICENSE](LICENSE).
