---
name: performance-learning
description: Tracks newsletter results, extracts specific learnings, and feeds them back into future newsletters. Every /track makes the next /create smarter. This is the learning loop — the feature that separates this system from prompt templates and SOPs. Same skill powers both the Cowork plugin and the autonomous Teammate Protocol.
---

# Performance Learning — The Feedback Loop

## Purpose

Turn newsletter results into reusable intelligence. Not "this newsletter did well" but "this specific angle drove 23% above baseline in this specific segment on this day of week with images from the product collection." The learning loop is the reason this system gets better over time while prompt templates stay static.

## Why This Matters

A prompt playbook produces the same quality output on newsletter 1 and newsletter 100. An SOP produces consistent quality but never improves. This system produces better output on newsletter 5 than newsletter 1, and better on newsletter 20 than newsletter 5. The difference is this skill — it turns every send into training data for the next one.

No other approach does this. Not prompt templates. Not SOPs. Not "upload your brand assets and use this master prompt." Those systems are static. This one compounds.

## The Learning Loop

```
/create (Newsletter 1) → sends → /track (results logged)
                                         ↓
                                learnings extracted
                                         ↓
/create (Newsletter 2) → reads learnings → smarter draft → sends → /track
                                                                       ↓
                                                              more learnings
                                                                       ↓
/create (Newsletter 3) → reads deeper history → even smarter → sends → /track
```

Each cycle through the loop adds:
- More accurate performance predictions
- Better angle selection (knows what's been tried and what worked)
- Better image selection (knows which images correlated with higher engagement)
- Segment-specific insights (knows which segments respond to what)
- Timing optimization (knows when this audience opens)
- Voice calibration (knows which tonal choices drove engagement)
- Length optimization (knows the sweet spot for this audience)

## Confidence Levels

Prediction accuracy correlates directly with tracked newsletter count:

| Newsletters Tracked | Confidence Level | What the System Can Predict |
|:-------------------:|:----------------:|---------------------------|
| 0 | Baseline | Industry benchmarks only. States they're estimates. |
| 1-2 | Low | Directional predictions. Wide confidence interval. "Could range from X% to Y%." |
| 3-7 | Medium | Segment-level predictions. Angle type effectiveness. Best send windows. Image impact patterns beginning. |
| 8-15 | High | Specific angle predictions. Segment × timing × angle interactions. Image type correlation. Subject line pattern analysis. |
| 16+ | Very High | Pattern-level predictions. Can identify which untried angles are likely to outperform based on similarity to proven patterns. Can recommend specific images based on engagement history. |

Always state the confidence level. Never present a Low confidence prediction as reliable. Honesty about uncertainty is more valuable than false precision.

## Learning Format

Every learning must be:

### Specific
Bad: "Urgency works well"
Good: "Urgency angle = 5.8% open rate in leads segment (31% above segment baseline of 4.4%)"

### Comparative
Bad: "Tuesday sends had good open rates"
Good: "Tuesday 10am = 5.2% open vs. Thursday 10am = 4.1% (27% difference, consistent across 3 newsletters)"

### Segment-attributed
Bad: "Personal stories drive engagement"
Good: "Personal/story angle = 3.2x reply rate in subscribers segment, but 0.8x in leads segment (leads prefer direct-value angle)"

### Time-stamped
Bad: "Spring themes perform well"
Good: "Spring themes: 5.2% open (March 2026, 2 newsletters). Winter themes: 4.8% (January 2026, 3 newsletters). Seasonal uplift = ~8%."

### Image-aware (when data exists)
Bad: "Images help"
Good: "Product hero image = +15% click rate vs. text-only newsletters (4 comparisons). Lifestyle images = no significant difference (2 comparisons — insufficient data)."

## What to Track

### Per Newsletter
- Open rate (overall + per segment)
- Click rate (overall + per segment)
- Unsubscribe rate (overall + per segment)
- Reply count (if available)
- A/B test results (if applicable — which subject line won)
- Angle type used
- Send day and time
- Newsletter goal
- Word count
- Images used (filenames + placement)
- Whether images were used at all (for image vs. text-only comparison)

### Cumulative (Updated After Each /track)

**Angle effectiveness matrix:**

| Angle Type | Overall | Segment A | Segment B | Segment C | Sample Size |
|-----------|:-------:|:---------:|:---------:|:---------:|:-----------:|
| Problem-first | +12% | +18% | +8% | +5% | 4 |
| Curiosity gap | +8% | +5% | +15% | +3% | 3 |
| Contrarian | +22% | +30% | +10% | +12% | 2 |
| Personal/story | +15% | +8% | +25% | +5% | 5 |

**Send time effectiveness:**
- Open rate by day × time window, with sample size per cell
- Minimum 3 data points before treating a pattern as reliable

**Subject line patterns:**
- Character count correlation with open rate
- Question vs. statement performance
- Number inclusion impact
- Preview text pairing patterns

**Image impact:**
- Image vs. text-only newsletter comparison (open rate, click rate)
- Hero image vs. no-hero comparison
- Image category effectiveness (product, lifestyle, headshot, illustration)
- Specific image reuse impact (does the same image lose effectiveness on repeat?)

**Segment baselines:**
- Current average open/click per segment, updated with each newsletter
- Segment-specific angle preferences
- Segment-specific length preferences
- Segment-specific CTA preferences

**Trend line:**
- Are overall metrics improving, declining, or flat?
- Moving average over last 5 newsletters vs. lifetime average
- Flag if recent performance diverges significantly from historical average

## Prediction Engine

When /create requests a prediction:

### Step 1 — Find Similar Newsletters
Search newsletter history for closest matches on:
- Same angle type
- Same target segment(s)
- Similar seasonal timing (within ±30 days of year)
- Same newsletter goal
- Similar image usage pattern (image vs. text-only)

### Step 2 — Calculate Base Prediction
- 3+ similar newsletters: use their average performance
- 1-2 similar: use their performance, widen confidence interval
- 0 similar: use angle effectiveness matrix + segment baselines. State prediction is extrapolated.

### Step 3 — Apply Adjustments
- **Recency** — if angle type hasn't been used in 60+ days, note the gap
- **Fatigue** — if angle type used in 3 of last 5 newsletters, apply -5-10% fatigue discount. Note: "This angle has been used frequently. Consider switching for freshness."
- **Seasonality** — if seasonal data exists, apply modifier
- **Image effect** — if this newsletter includes images and past data shows image newsletters outperform, factor that in. If no image and past data shows image newsletters do better, note: "Adding an image from your Drive folder could improve click-through based on past data."
- **List growth/shrink** — if subscriber count has changed significantly, note potential impact on rates

### Step 4 — State Prediction Honestly
Format: "[X%] open rate ([confidence level], based on [N] similar newsletters)"

If high uncertainty: "Predicted 4.8% open rate, but confidence is Low — this is the first curiosity-gap angle for the leads segment. Could range from 3.5% to 6.2%."

Never round to make predictions look cleaner. "4.83%" is more honest than "~5%."

## Handling Bad Newsletters

When a newsletter underperforms (>10% below prediction or baseline):

1. **Don't blame the audience.** The newsletter made choices — identify which choice didn't land.
2. **Check the variables systematically:**
   - Subject line — was it too long? Too vague? Wrong angle for the segment?
   - Angle — did it miss the pain point? Was it a repeat?
   - Timing — wrong day? Wrong time? Competing with a holiday or event?
   - Length — too long for this segment? Too short to deliver value?
   - Images — wrong image? Image slowed load time? No image when audience expects one?
   - CTA — too aggressive? Too soft? Wrong framing for segment motivation?
3. **Record the negative learning** with same specificity as positive ones.
4. **Don't overcorrect.** One bad newsletter doesn't invalidate a pattern from 5 good ones. Note the outlier, weight it appropriately.

## Memory Architecture

Performance data lives in the ~~docs folder as plain markdown. Same Drive folder, same documents, fully transparent.

### Files Written by /track

**newsletter-log.md** — chronological record of every newsletter created and tracked. One entry per newsletter with date, angle, subject, segments, images, metrics, and one-line learning summary.

**newsletter-learnings.md** — cumulative learnings organized by category: angle effectiveness, segment insights, timing patterns, subject line patterns, image impact, CTA patterns. Updated with each /track run. New learnings append; they never overwrite.

**newsletter-baselines.md** — current state: overall averages, per-segment baselines, angle effectiveness matrix, best send windows, newsletter count, confidence level, last updated date.

### Why Plain Markdown

- The user can open these files and read exactly what the system knows
- The user can edit them — correct a learning, add context, remove an outlier
- No database, no schema, no hidden state
- Same format works in a Cowork plugin (reads from Drive) and a Teammate Protocol deployment (reads from workspace/)
- Human-readable AND machine-readable

### File Lifecycle

| Newsletter Count | Files Present | System Capability |
|:---:|---|---|
| 0 | None | Uses brand docs only. Industry benchmarks. |
| 1 | newsletter-log (1 entry) | One reference point. Directional predictions. |
| 3-5 | log + learnings + baselines | Real segment data. Angle comparison starting. Image impact data emerging. |
| 8-15 | All files, substantive | Reliable predictions. Pattern detection. Seasonal awareness. Image recommendations. |
| 16+ | All files, deep | Full intelligence. Segment × angle × timing × image interactions. Confident recommendations. |

## Teammate Protocol Compatibility

This skill is designed to work in two modes:

**Plugin mode (Cowork):** User manually runs `/create` and `/track`. Skill reads from and writes to ~~docs (Google Drive).

**Teammate mode (OpenClaw VPS):** Cron job fires `runtime.py`. Skill reads from and writes to `workspace/` (synced from Google Drive). Standing orders determine when to draft and when to review performance.

Same skill file. Same methodology. Same learning files. Different trigger mechanism. The intelligence is in the skill, not in the trigger.

```
Teammate standing_orders.md:

RECURRING TASKS

Weekly
- Task: Draft weekly newsletter
  Day: Tuesday
  Skill: email-strategist

- Task: Review last newsletter's performance
  Day: Monday
  Skill: performance-learning

Monthly
- Task: Refresh segment baselines
  Day: First Monday
  Skill: performance-learning
```

The plugin is the manual version. The teammate is the autonomous version. Both produce the same quality because they run the same skills.

## The Compounding Advantage

This is the most defensible feature in the system:

- A prompt template produces identical quality on day 1 and day 365
- An SOP produces consistent quality but never improves
- This system produces better quality with every tracked newsletter

By newsletter 10, the system knows things about the brand's email performance that the brand's own team may not have noticed — because it cross-references every variable systematically, without forgetting, without optimism bias, without getting bored of the data.

That intelligence lives in the client's Drive folder. It's their data, producing their results, getting smarter on their behalf. They can read it, edit it, take it with them.

No prompt playbook does this. No SOP does this. No "master prompt" does this. This is the product.
