# PRD — Email Marketing Manager v2.0

**Status:** Shipped · v2.0.1 · [Changelog](CHANGELOG.md)
**Owner:** Roger Gurbani

## Problem

Newsletter knowledge rarely compounds. Subject-line patterns, segment response, timing, angles, image performance, and CTA behavior live in an operator's head or in disconnected analytics. Generic drafting tools also invent asset names and reset their context every session.

## Users

- Newsletter operators producing on a weekly or biweekly cadence
- Marketing teams running segmented sends
- Agencies that need client knowledge to survive staff changes

## What v2 does

- Reads brand guides, personas, past newsletters, performance history, and learning files from Box.
- Queries Cloudinary before drafting and constructs a closed candidate list containing verified asset IDs, delivery URLs, dimensions, format, and metadata.
- Prohibits the draft from citing any image outside the current candidate list.
- Generates segment variants differentiated by audience needs, not surface-level swaps.
- Applies the substitution test so generic copy is revised before review.
- Produces a performance prediction with rationale grounded in the account's baselines.
- Scores Voice, Angle, Structure, Image Integrity, and Segment Fit from 1–5.
- Requires 5/5 on every editorial gate before a draft can post to Beehiiv.
- Posts drafts to Beehiiv but never publishes or sends them.
- Pulls Beehiiv metrics when connected and accepts manual results otherwise.
- Writes transparent, editable learning files back to Box so the next draft uses accumulated evidence.

## Editorial gate outcomes

- **APPROVED:** all five gates score 5/5.
- **REVISE:** any gate scores 3–4; fix the failing gate and score again.
- **KILL:** any gate scores 1–2; restart from a different angle.

## What v2 explicitly does not do

- **Does not send.** Publishing and sending remain human actions in Beehiiv.
- **Does not invent assets.** If Cloudinary is unavailable or returns no match, the output is text-only.
- **Does not bypass the editorial gate.** A non-approved draft cannot post to Beehiiv.
- **Does not promise unavailable segment metrics.** Segment-level learning depends on the data Beehiiv or the user provides.
- **Does not fine-tune on sends.** Learnings remain readable and correctable Markdown.

## Success criteria

- Every cited image appears in the current Cloudinary candidate list with a verified delivery URL and dimensions.
- No Beehiiv draft is created until every editorial gate scores 5/5.
- Segment variants differ in angle and emphasis, not only greeting or vocabulary.
- Every `/email-marketing-manager:create` includes a prediction with evidence or explicitly states that no baseline exists.
- A later draft can trace material choices to prior entries in `newsletter-learnings.md` or `newsletter-baselines.md`.
- The plugin remains usable with any subset of connectors, including fully manual mode.

## Decision log

- **Closed-list assets over generated references:** image integrity is deterministic and auditable.
- **Five hard gates over a checklist:** approval has an unambiguous threshold.
- **Learning files over fine-tuning:** accumulated knowledge stays transparent and portable.
- **Draft-only Beehiiv writes:** the system improves the work without taking away the human send decision.
