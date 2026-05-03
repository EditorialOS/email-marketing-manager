---
description: Draft a complete newsletter from your real documents. Reads your brand guide, audience personas, past newsletters, images, and performance learnings from Google Drive. Produces subject line, body copy, CTA, image selections, segment-specific variants, and a performance prediction. Posts the draft to your email platform.
argument-hint: "Topic: spring sale" or "Topic: product launch, Segment: past customers"
---

# /create

One command. Full newsletter. Built from your documents, not a prompt template.

## Trigger

Use when you want to draft a newsletter, email update, or any email send. Works with a topic, an angle, or just a goal.

## Inputs

- **Topic or description** — what the newsletter is about (required — even one sentence works)
- **Target segment** — optional. If not specified, creates variants for all configured segments.
- **Goal** — optional. Default: engagement. Alternatives: clicks, conversions, retention.
- **Tone override** — optional. Default uses brand voice from Drive documents.
- **Images** — optional. Default selects from Drive images folder. User can specify "no images" or name specific files.

---

## Step 1 — Load Context

Use client-context skill. Show one-line status header.

If 🟢 Configured: load brand guide, audience personas, past newsletters, performance learnings, and available images from `~~docs`. Show what was found.

If ⚪ No client: ask for brand name, audience description, and one example of a past newsletter. State that output is directional without full context.

---

## Step 2 — Check Newsletter History

Read past newsletters from Drive and from `newsletter-log.md` if it exists from prior `/track` runs.

- What topics have been covered recently? Avoid repeats within the last 4 issues.
- What angles have been used? Don't reuse the same hook type back-to-back.
- What performed well? Lean toward patterns that worked.
- What performed badly? Note it — don't repeat what underperformed.

If no history exists (first newsletter): skip this step. State it's the first draft.

---

## Step 3 — Select Angle

An angle is not the topic — it's the specific entry point that will resonate with this audience right now.

Every angle must pass three checks:
1. **Not a repeat** — hasn't been used in last 4 newsletters
2. **Connects to real pain point** — mapped to a segment's actual concern from the personas doc
3. **Native to brand voice** — the hook style matches the brand guide's tone

State the selected angle and why it was chosen. If multiple angles are viable, present the top pick with one alternative.

---

## Step 4 — Select Images

Read the `~~docs` images subfolder for available images.

- Match images to the newsletter topic and angle
- Select 1–3 images (one hero, optionally 1–2 supporting)
- For each selected image: state the filename and where it should appear (header, inline, footer)

If no images folder exists or it's empty: note it and produce the newsletter without images. Suggest what kind of image would strengthen the piece.

---

## Step 5 — Write the Newsletter

For the primary segment, produce:

- **Subject line** — under 50 characters. No spam triggers. Optimized for open rate.
- **Preview text** — complements subject line, under 65 characters. Creates a two-part hook.
- **Body copy** — in the brand's voice. Structure adapts to goal:
  - Engagement: Hook → story/observation → insight → soft CTA
  - Clicks: Hook → problem/opportunity → value of clicking → direct CTA
  - Conversions: Hook → problem → solution → proof → CTA with urgency
  - Retention: Personal hook → what's new → insider value → appreciation CTA
- **Image placement** — where each selected image appears, with alt text
- **CTA** — specific, action-oriented, single focus

Apply voice rules from brand guide: sentence structure, vocabulary, punctuation, greeting/sign-off, length.

---

## Step 6 — Substitution Test

Read the body copy without the brand name. Could this newsletter have been sent by a competitor?

If it sounds generic — if swapping in another brand name wouldn't change anything — the voice application failed. Rewrite the opening and CTA with more brand-specific language and note what was changed.

If it passes: move on. Don't narrate success.

---

## Step 7 — Generate Segment Variants

For each additional configured segment:

| Element | Changes? | How |
|---------|----------|-----|
| Subject line | Yes | Different hook based on segment's primary concern |
| Preview text | Yes | Complements the adjusted subject line |
| Opening (first 2–3 sentences) | Yes | Rewritten for this segment's entry point |
| Core body copy | No | Value proposition stays the same |
| Image selection | Sometimes | Same images unless segment context demands different |
| CTA | Yes | Same action, framed for this segment's motivation |

Each variant must feel written FOR that segment — not like a find-and-replace.

---

## Step 8 — Performance Prediction

If performance history exists:
- Predict open rate and click rate based on similar past newsletters
- State confidence level: Very High (16+), High (8–15), Medium (3–7), Low (1–2), Baseline (0)
- Note what's similar and different vs. reference newsletters

If no history:
- Use industry benchmarks. State they're benchmarks, not predictions.
- "After you run `/track` on this newsletter, the next prediction will use real data."

---

## Step 9 — Post Draft and Save Record

Post to `~~email` if connected as a **draft only**. Never auto-send. Note the draft link if available.

If not connected: present full newsletter copy formatted for easy paste.

Save newsletter record to `~~docs`:
- Newsletter topic/title
- Date created
- Angle type
- Segments targeted
- Subject line
- Images used
- Predicted open rate + confidence
- Goal

---

## Output Format

```
EMAIL MARKETING MANAGER
[Config status header]
Generated: [Date]

---

NEWSLETTER: [Topic]
ANGLE: [The specific hook — one sentence]
GOAL: [What this newsletter is trying to achieve]
TIMING: [Recommended send day/time + reasoning]

---

IMAGES SELECTED
Hero: [filename] — [placement + alt text]
Supporting: [filename] — [placement + alt text] (if applicable)

---

PRIMARY VERSION — [Segment name]
Subject: [subject line] ([char count])
Preview: [preview text] ([char count])
[Full newsletter body copy with image placement markers]
CTA: [call to action]

---

SEGMENT VARIANT — [Segment name]
Subject: [adjusted subject line] ([char count])
Preview: [adjusted preview text]
[Adjusted opening — 2–3 sentences]
[Note: body continues from primary version after the opening]
CTA: [adjusted CTA]

[Repeat for each segment]

---

PERFORMANCE PREDICTION
Predicted open rate: [X%] ([confidence level])
Predicted click rate: [X%] ([confidence level])
Based on: [reference newsletters or industry benchmarks]
What's different this time: [what's new vs. past data]

---

NEWSLETTER RECORD
Saved to: [location in ~~docs]
Draft posted to: [email platform] or "not connected — copy above"

After this newsletter sends, run /track to log results.
Every tracked newsletter makes the next one smarter.

---

QUALITY GATES
✓ Brand voice applied from [source document or direct input]
✓ All configured segments served with variants
✓ Subject line under 50 chars, preview text under 65 chars
✓ Images selected from Drive or flagged as unavailable
✓ CTA is single-focus and action-oriented
✓ Angle checked against history — not a repeat
✓ Substitution test passed
✓ Performance prediction stated with honest confidence level
```
