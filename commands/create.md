---
description: "Draft a complete newsletter from Box context, verified Cloudinary assets, and performance history; run the editorial gate; and post an approved draft to Beehiiv."
argument-hint: "Topic: spring sale | Segment: past customers"
---

# /email-marketing-manager:create

One command. Full newsletter. Built from your documents, not a prompt template.

## Trigger

Use when you want to draft a newsletter, email update, or any email send. Works with a topic, an angle, or just a goal.

## Inputs

- **Topic or description** — what the newsletter is about (required — even one sentence works)
- **Target segment** — optional. If not specified, creates variants for all configured segments.
- **Goal** — optional. Default: engagement. Alternatives: clicks, conversions, retention.
- **Tone override** — optional. Default uses brand voice from Box documents.
- **Images** — optional. Default selects from Cloudinary library. User can specify "no images" or name specific asset IDs.

---

## Step 1 — Load Context

Use client-context skill. Show one-line status header.

If 🟢 Configured: load brand guide, audience personas, past newsletters, and performance learnings from Box. Query Cloudinary for available images. Show what was found.

If ⚪ No client: ask for brand name, audience description, and one example of a past newsletter. State that output is directional without full context.

---

## Step 2 — Check Newsletter History

Read past newsletters from Box and from `newsletter-log.md` if it exists from prior `/email-marketing-manager:track` runs.

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

## Step 4 — Select Images (Cloudinary Closed List)

Query Cloudinary for available assets matching the newsletter topic. Use `search-assets` with relevant tags, keywords, or folder paths. Build the **closed candidate list**.

**THE RULE: Every asset ID you cite must appear in the closed candidate list. An ID that is not in the list does not exist.**

From the candidate list, select images by role:

| Role | What to select | Criteria |
|------|---------------|----------|
| Hero (1200×600, 2:1) | One strong image | High visual impact, relevant to angle, not used in last 3 newsletters |
| Section (1200×675, 16:9) | 0-2 supporting | Adds information text doesn't convey, breaks up long copy |
| Item (600×600, 1:1) | As needed | Product shots, headshots, thumbnails |

For each selected image, produce the manifest entry:

```
Asset ID: [cloudinary public_id]
Placement: [hero / section / item]
Delivery URL: [CDN URL]
Native: [width × height]
Rationale: [why this image for this placement]
Alt text: [confirmed description or ALT PENDING]
```

If Cloudinary is not connected or returns no matching assets: produce the newsletter without images. Suggest what kind of image would strengthen the piece. Never construct URLs by hand.

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
- **Image placement** — where each selected image appears, with alt text from manifest
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
- "After you run `/email-marketing-manager:track` on this newsletter, the next prediction will use real data."

---

## Step 9 — Editorial Gate

Score the newsletter across five gates. Each gate scores 1–5.

| Gate | What It Tests | 5 (pass) | 3-4 (soft fail) | 1-2 (hard fail) |
|------|--------------|----------|-----------------|-----------------|
| **Voice** | Does it sound like this brand? | Indistinguishable from past newsletters | Recognizable but drifted | Generic or wrong tone |
| **Angle** | Is the hook earned and specific? | Connects to real pain point, not a repeat | Decent hook but vague connection | Repeat angle or no pain point |
| **Structure** | Does the architecture match the goal? | Goal-appropriate flow, right length | Flow works but loose | Wrong structure for goal |
| **Image integrity** | Are all images from the closed list with valid alt text? | All IDs verified, alt text confirmed | IDs verified, some ALT PENDING | Any unverified ID or fabricated alt |
| **Segment fit** | Do variants feel written for each segment? | Each opening references segment-specific pain | Variants exist but feel like find-replace | Missing variants or generic |

### Verdicts

- **APPROVED** — all five gates score 5/5. Ready for Beehiiv.
- **REVISE** — any gate scores 3 or 4. Fix the failing gates and re-score. Do not post to Beehiiv until all gates clear.
- **KILL** — any gate scores 1 or 2. The draft has a structural problem. Restart from Step 3 with a different angle or approach.

State each gate's score and a one-line reason. If REVISE: fix the issues and re-run the gate. If KILL: explain what failed and restart.

---

## Step 10 — Post Draft and Save Record

If APPROVED and Beehiiv is connected: post the newsletter as a **draft only** via the Beehiiv API. Never auto-send. Note the draft ID and link if available.

If Beehiiv is not connected: present full newsletter copy formatted for easy paste into Beehiiv.

Save newsletter record to Box:
- Newsletter topic/title
- Date created
- Angle type
- Segments targeted
- Subject line
- Images used (Cloudinary asset IDs)
- Predicted open rate + confidence
- Goal
- Editorial gate scores

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

IMAGE MANIFEST
Hero: [asset_id] — [delivery URL] — [alt text]
Section: [asset_id] — [delivery URL] — [alt text] (if applicable)
(All images verified against Cloudinary closed list)

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

EDITORIAL GATE
Voice:          [score]/5 — [reason]
Angle:          [score]/5 — [reason]
Structure:      [score]/5 — [reason]
Image integrity: [score]/5 — [reason]
Segment fit:    [score]/5 — [reason]

VERDICT: [APPROVED / REVISE / KILL]

---

NEWSLETTER RECORD
Saved to: [Box folder path]
Draft posted to: Beehiiv (draft ID: [id]) or "not connected — copy above"

After this newsletter sends, run /email-marketing-manager:track to log results.
Every tracked newsletter makes the next one smarter.
```
