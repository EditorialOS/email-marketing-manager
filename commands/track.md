---
description: Log newsletter results and update the learning memory. Every tracked newsletter makes the next /create smarter — better predictions, better angles, better timing. The learning loop is the product.
argument-hint: "Newsletter: spring sale" or paste results directly
---

# /track

Log results. Learn from them. Next newsletter gets smarter.

## Trigger

Use after a newsletter has sent and results are available (typically 48+ hours after send). Works with newsletter name, pasted metrics, or automatic pull from `~~email`.

## Inputs

- **Newsletter name or topic** — which newsletter to track (required)
- **Results** — optional if `~~email` is connected (pulls automatically). Otherwise: open rate, click rate, and any other metrics available.
- **Notes** — optional. Anything observed: "subject line A won the A/B test", "got 3 direct replies", "unsubscribe spike from the leads segment"

---

## Step 1 — Gather Results

If `~~email` connected: pull actual send metrics — open rate, click rate, unsubscribe rate, reply count, send count, segment breakdown if available.

If not connected: ask for the numbers. Accept whatever is available — even partial data is useful. Don't block on missing metrics.

---

## Step 2 — Compare to Prediction

Pull the prediction from the newsletter record saved during `/create`.

- If prediction existed: compare actual vs. predicted. Calculate variance.
  - Within 10%: accurate. Note what held.
  - Over 10% above: outperformed. Identify what was different.
  - Over 10% below: underperformed. Identify what was different.
- If no prediction existed (first newsletter): establish baseline.

---

## Step 3 — Analyze What Worked

Break down by:

- **Subject line performance** — did the open rate suggest the subject worked? If A/B test ran, which won and why?
- **Angle effectiveness** — how did the core hook perform vs. past hooks?
- **Segment differences** — which segments engaged more or less?
- **Timing** — did the send time/day perform as expected?
- **Image impact** — if images were used, did they correlate with higher engagement?
- **CTA performance** — click rate tells you if the ask landed

Be specific. Not "the newsletter did well" but "the contrarian angle drove 23% above baseline in the subscribers segment, likely because of the seasonal urgency in the opening."

---

## Step 4 — Extract Learnings

Generate 3–5 specific, reusable learnings. Each must include: the specific variable, the metric, the segment (if applicable), and comparison to baseline.

**Good:** "Contrarian angle = 5.2% open rate in subscribers segment (23% above baseline)"
**Bad:** "Contrarian angles seem to work well"

**Good:** "Wednesday 10am send = highest open rate across 3 newsletters"
**Bad:** "Midweek sends are good"

**Good:** "Leads segment unsubscribes 2× when newsletter exceeds 400 words"
**Bad:** "Keep newsletters shorter for some segments"

---

## Step 5 — Save Learnings to Drive

Write learnings to `~~docs` folder. Three files, all plain markdown:

**newsletter-log.md** — append this newsletter's record:
```
## [Newsletter title] — [Date sent]
Angle: [type]
Subject: [text]
Segments: [list]
Images: [filenames used or "none"]
Open rate: [X%] (predicted: [Y%])
Click rate: [X%] (predicted: [Y%])
Learning: [1-line summary of key finding]
```

**newsletter-learnings.md** — append new learnings, organized by category:
- Angle effectiveness
- Segment insights
- Timing patterns
- Subject line patterns
- Image impact
- CTA patterns

**newsletter-baselines.md** — update current baselines:
- Overall averages (open, click, unsubscribe)
- Per-segment baselines
- Best/worst performing angles
- Best send windows
- Newsletter count (affects confidence level for next prediction)

If `~~docs` not connected: display all learnings formatted for copy-paste. Instruct the user to save them in their Drive folder so the next `/create` can read them.

---

## Output Format

```
EMAIL MARKETING MANAGER — NEWSLETTER RESULTS

Newsletter: [Title/topic]
Sent: [Date/time]
Duration: [Days since send]

---

RESULTS

Open rate:        [X%]  [vs. predicted X% — ✅ accurate / ⬆ above / ⬇ below]
Click rate:       [X%]  [vs. predicted X% — ✅ / ⬆ / ⬇]
Unsubscribe rate: [X%]
Replies:          [N]
Total sent:       [N]

By segment:
- [Segment 1]: [open%] / [click%]  [vs. segment baseline]
- [Segment 2]: [open%] / [click%]  [vs. segment baseline]

---

WHAT WORKED

✅ [Specific finding with metric]
✅ [Specific finding with metric]

WHAT DIDN'T

⬇ [Specific finding with metric]

IMAGE IMPACT

[Comparison of image vs. no-image newsletters if data exists]

---

LEARNINGS RECORDED

→ "[Learning 1 — specific, metric, segment, comparison]"
→ "[Learning 2]"
→ "[Learning 3]"

Saved to: [location in ~~docs]

---

PREDICTION ACCURACY

This newsletter: predicted [X%] → actual [X%] = [variance]
Overall accuracy (all newsletters): [avg variance across N newsletters]
Confidence for next newsletter: [Baseline / Low / Medium / High / Very High] ([N] tracked)

---

NEXT NEWSLETTER RECOMMENDATIONS

Based on what this newsletter taught:
- [Recommendation 1 — specific angle, segment, timing, or image choice]
- [Recommendation 2]

Ready? Run /create and these learnings apply automatically.

---

QUALITY GATES
✓ Results compared to prediction with variance calculated
✓ Learnings are specific (metric + segment + comparison)
✓ Segment-level breakdown included
✓ Image impact assessed
✓ Performance memory updated in Drive
✓ Newsletter count incremented ([N] total tracked)
✓ Next /create will reference these learnings
```
