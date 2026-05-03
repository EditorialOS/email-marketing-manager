---
name: email-strategist
description: Newsletter creation methodology. Determines angle, selects images from Drive, writes client-specific copy with segment variants, and sizes output to real audience data. Used by /create. The strategic layer that prompt templates skip.
---

# Email Strategist — Newsletter Creation Methodology

## Purpose

Turn a topic into a complete, client-specific newsletter draft. This skill encodes the strategic decisions that happen BEFORE writing — the layer that separates a branded newsletter from generic AI copy.

## Core Principle

The model doesn't matter. The context matters. A mediocre model with perfect client context produces better newsletters than the best model with a generic prompt. This skill ensures every decision is grounded in the client's real documents.

## The Anti-SOP Approach

Traditional AI email workflow (what prompt playbooks sell):
1. Create a project in Claude
2. Upload brand assets manually
3. Upload a "strategy PDF" (someone's lead magnet)
4. Paste a master prompt with fill-in-the-blank variables
5. Generate copy
6. Edit manually
7. Repeat from scratch next time — nothing learned

Email Marketing Manager approach:
1. Drive folder exists with your documents (already done)
2. `/create Topic: "spring sale"` (one command)
3. Newsletter produced — with images from your folder, segment variants based on your personas, angle selected based on what hasn't been used recently
4. `/track` after it sends — real data recorded
5. Next `/create` uses those learnings automatically

The difference: no SOP to follow. No prompt to write. No manual upload. No PDF strategy framework from a stranger. No starting from scratch. The skill does the strategic thinking the SOP skips entirely.

## Angle Selection

Before writing a single word, determine the angle. An angle is not the topic — it's the specific entry point into the topic that will resonate with this audience at this moment.

### Angle Quality Test

Every angle must pass three checks:

1. **Not a repeat.** Check newsletter history. If this exact angle type was used in the last 4 newsletters, find a different entry point. Repetition kills open rates. If no history exists, any angle is valid.

2. **Connects to a real pain point.** Check audience personas. The hook must address something a specific segment actually cares about — not what the brand wants to say. Map the angle to a segment pain point explicitly: "This curiosity-gap angle targets the leads segment's concern about [specific pain point from personas doc]."

3. **Native to brand voice.** If the brand guide says "approachable and warm," a confrontational contrarian hook is a mismatch. If the brand is "operationally honest," hype-driven urgency doesn't fit. The angle must feel natural in the brand's voice.

### Angle Types

| Type | When to Use | Best For | Open Rate Impact |
|------|------------|----------|:----------------:|
| Problem-first | Audience is problem-aware but solution-unaware | Establishing authority | Above average |
| Curiosity gap | Audience is engaged but needs a reason to open NOW | Maximizing opens | Highest |
| Contrarian | Audience holds a common assumption you can challenge | Standing out in inbox | High but variable |
| Personal/story | Brand has a named person or founder voice | Building relationship | Above average |
| Urgency | Time-bound offer or seasonal moment | Driving action | High for conversions |
| Social proof | Evidence of results or community | Reducing skepticism | Average |
| Educational | Audience values learning and respects expertise | Building trust over time | Steady |
| Direct value | Audience wants utility, not entertainment | High click-through | Average opens, high clicks |

**Default rule:** Select the angle type that best matches the brand voice. If the brand voice doc says "operationally honest," don't default to urgency or hype. If it says "warm and personal," don't default to educational lecture.

**History-aware selection:** If learning data shows that contrarian angles consistently outperform for this brand's audience, weight toward contrarian — but don't use it more than 2 out of every 4 newsletters.

**When data conflicts with instinct:** Trust the data. If the performance-learning data says educational angles underperform for this audience despite the brand guide favoring educational tone, note the tension: "Your brand guide favors educational tone, but tracked data shows educational angles underperform. This newsletter uses [alternative] — if you disagree, override with a tone instruction."

## Image Selection from Drive

### How It Works

Images live in the client's Drive folder, typically in an images/ subfolder. The client-context skill inventories available images at load time. This skill selects images that match the newsletter.

### Selection Logic

1. **Topic match** — select images related to the newsletter topic. Product newsletter → product shots. People-focused newsletter → headshots or team photos. Seasonal newsletter → seasonal imagery.

2. **Placement pattern** — match the brand's past newsletter image usage:
   - If past newsletters use hero images: select one strong hero
   - If past newsletters use inline images: select 1-2 supporting images
   - If past newsletters are text-only: don't force images. Note availability for future use.

3. **Hero image criteria:**
   - High visual impact
   - Relevant to the angle (not just the topic)
   - Hasn't been used in the last 3 newsletters
   - Works at email width (landscape or square preferred for hero)

4. **Supporting image criteria:**
   - Adds information the text doesn't convey
   - Breaks up long text blocks (for newsletters > 400 words)
   - Consistent style with the brand (don't mix illustration and photography)

### When Images Aren't Available

If the images/ folder is empty or doesn't exist:
- Produce the newsletter without images
- At the end, suggest: "No images found in your Drive folder. Adding a few product shots or lifestyle images to [folder]/images/ would strengthen future newsletters."
- Never generate placeholder images or suggest stock photo sites

### Image Output Format

For each selected image:
```
Image: [filename]
Placement: [hero / inline after paragraph N / footer]
Alt text: [descriptive alt text for accessibility]
```

## Writing the Newsletter

### Subject Line Rules

- Under 50 characters — renders fully on every device
- No ALL CAPS words (except brand name if that's the style)
- No spam triggers: free, urgent, act now, limited time, exclusive offer, don't miss
- Preview text complements — never repeats the subject line
- One curiosity mechanism per subject line — don't stack hooks
- Match the brand's subject line patterns from history (questions? statements? numbers?)

### Body Copy Structure

Adapt to newsletter goal:

**Engagement goal (newsletter, relationship building):**
Hook (1-2 sentences) → Story or observation → Insight that earns trust → Soft CTA (reply, read more, think about this)

**Click goal (driving to page, product, article):**
Hook (1 sentence) → Problem or opportunity → Why clicking matters → Direct CTA with specific destination

**Conversion goal (purchase, signup, booking):**
Hook → Problem → Solution (the product) → Proof (numbers, testimonials, specifics) → Objection handling → CTA with reason to act now

**Retention goal (keeping existing customers):**
Personal hook → What's new or what's coming → Insider value they can't get elsewhere → Appreciation + CTA

### Voice Application

Read the brand voice from client-context. Apply through:

- **Sentence structure** — formal brands use longer, compound sentences. Casual brands use fragments. Match past newsletters.
- **Vocabulary** — use the brand's word list. If the guide says "avoid: synergy, leverage, game-changer" those words do not appear. Ever.
- **Punctuation** — em dashes, Oxford commas, exclamation points (or absence). Match the guide.
- **Greeting/sign-off** — match past newsletter patterns exactly. If past newsletters start with "Hey [first_name]," use that. If they open cold with no greeting, don't add one.
- **Length** — match past newsletter lengths unless performance data suggests change. If the brand sends 300-word newsletters, don't produce 800 words.
- **Personality markers** — does the brand use "I" or "we"? Do they ask questions? Do they use parenthetical asides? Match the personality, not just the vocabulary.

### The Substitution Test

After writing, check: could this newsletter have been sent by a different brand? Read the body without the brand name. If it sounds generic — if swapping in a competitor's name would still work — the voice application failed. Rewrite the opening and CTA.

This test is pass/fail. Don't narrate success. If it passes, move on. If it fails, fix it.

## Segment Variants

### What Changes Per Segment

| Element | Changes? | How |
|---------|:--------:|-----|
| Subject line | Yes | Different hook targeting segment's primary concern |
| Preview text | Yes | Complements adjusted subject line |
| Opening (first 2-3 sentences) | Yes | Rewritten for this segment's entry point |
| Core body copy | No | Value proposition stays the same |
| Images | Sometimes | Only if segment context demands different imagery |
| CTA | Yes | Same action, framed for this segment's motivation |
| Length | Sometimes | If persona data shows segment prefers shorter/longer |

### What Does NOT Change

- Brand voice — consistent across all variants
- Core message — the newsletter is about one thing
- Offer details — if there's a specific offer, identical across variants
- Proof points — same evidence, possibly different emphasis
- Image style — consistent visual identity

### Variant Quality Test

Each variant must feel written FOR that segment — not like a find-and-replace.

Bad: "As a valued customer..." (could be anyone)
Good: "Last month you browsed our spring collection but didn't buy — here's why that might have been smart." (specific behavior)

Bad: "Great news for our subscribers!" (generic)
Good: "You told us you care about ingredients. So we changed ours." (specific to a feedback-active segment)

If a variant doesn't pass this test, rewrite the opening. The segment pain point from the personas doc should be recognizable in the first sentence.

## Newsletter Record

Every newsletter must be saved as a record:

```
Newsletter: [title/topic]
Date: [created date]
Angle: [type] — [specific hook]
Segments targeted: [list]
Subject line (primary): [text]
Images used: [filenames or "none"]
Predicted open rate: [X%] ([confidence])
Goal: [engagement/clicks/conversions/retention]
```

This record accumulates in the Drive folder. By newsletter 5, the system has meaningful history. By newsletter 10, predictions are calibrated to this specific brand and audience. By newsletter 20, the system knows things about the audience that the brand's own team may not have noticed.

## Performance Benchmarks (Defaults)

Use only when no client-specific data exists. Always state these are benchmarks:

| Metric | B2C | B2B | Creator/Newsletter |
|--------|:---:|:---:|:------------------:|
| Open rate | 18-22% | 20-25% | 25-35% |
| Click rate | 2-3% | 2-4% | 3-5% |
| Unsubscribe rate | <0.3% | <0.2% | <0.1% |
| Best send time | Tue-Thu 10am | Tue-Wed 9am | Tue-Fri 8-10am |
| Avg length | 200-400 words | 300-500 words | 400-800 words |

After the first /track run, benchmarks are replaced with real data. Never use benchmarks when real data exists. Never present benchmarks as predictions.
