---
description: "Pull or accept newsletter results, compare them with the prediction, and write reusable performance learnings back to Box."
argument-hint: "Newsletter: spring sale | Results: optional"
---

# /email-marketing-manager:track

Log results. Learn from them. Next newsletter gets smarter.

## Trigger

Use after a newsletter has sent and results are available (typically 48+ hours after send). Works with newsletter name, pasted metrics, or automatic pull from Beehiiv.

## Inputs

- **Newsletter name or topic** — which newsletter to track (required)
- **Results** — optional if Beehiiv is connected (pulls automatically). Otherwise: open rate, click rate, and any other metrics available.
- **Notes** — optional. Anything observed: "subject line A won the A/B test", "got 3 direct replies", "unsubscribe spike from the leads segment"

---

## Step 1 — Gather Results

If Beehiiv connected: pull actual send metrics — open rate, click rate, unsubscribe rate, reply count, send count, segment breakdown if available. Use the Beehiiv API to find the post by title or ID and read its analytics.

If not connected: ask for the numbers. Accept whatever is available — even partial data is useful. Don't block on missing metrics.

---

## Step 2 — Compare to Prediction

Pull the prediction from the newsletter record saved during `/email-marketing-manager:create` (from `newsletter-log.md` in Box).

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
- **Image impact** — if Cloudinary images were used, did they correlate with higher engagement? Note asset IDs for future reference.
- **CTA performance** — click rate tells you if the ask landed

Be specific. Not "the newsletter did well" but "the contrarian angle drove 23% above baseline in the subscribers segment, likely because of the seasonal urgency in the opening."

---

## Step 4 — Extract Learnings

Generate 3–5 specific, reusable learnings. Each must include: the specific variable, the metric, the segment (if applicable), and comparison to baseline.

**Good:** "Contrarian angle = 5.2% open rate in subscribers segment (23% above baseline)"
**Bad:** "Contrarian angles seem to work well"

**Good:** "Wednesday 10am send = highest open rate across 3 newsletters"
**Bad:** "Midweek sends are good"

**Good:** "Product hero image (asset: product-spring-2026) = +15% click rate vs. text-only"
**Bad:** "Images help"

---

## Step 5 — Save Learnings to Box

Write learnings to the client's Box folder. Three files, all plain markdown:

**newsletter-log.md** — append this newsletter's record:
```
## [Newsletter title] — [Date sent]
Angle: [type]
Subject: [text]
Segments: [list]
Images: [Cloudinary asset IDs used or "none"]
Open rate: [X%] (predicted: [Y%])
Click rate: [X%] (predicted: [Y%])
Editorial gate scores: [V/A/S/I/S]
Learning: [1-line summary of key finding]
```

**newsletter-learnings.md** — append new learnings, organized by category:
- Angle effectiveness
- Segment insights
- Timing patterns
- Subject line patterns
- Image impact (with Cloudinary asset IDs for reference)
- CTA patterns

**newsletter-baselines.md** — update current baselines:
- Overall averages (open, click, unsubscribe)
- Per-segment baselines
- Best/worst performing angles
- Best send windows
- Newsletter count (affects confidence level for next prediction)

Use Box MCP tools to read existing files, update them, and write back. If files don't exist yet, create them.

If Box not connected: display all learnings formatted for copy-paste. Instruct the user to save them in their Box folder so the next `/email-marketing-manager:create` can read them.

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

[Which Cloudinary assets appeared and their correlation with engagement]

---

LEARNINGS RECORDED

→ "[Learning 1 — specific, metric, segment, comparison]"
→ "[Learning 2]"
→ "[Learning 3]"

Saved to: [Box folder path]

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

Ready? Run /email-marketing-manager:create and these learnings apply automatically.
```
