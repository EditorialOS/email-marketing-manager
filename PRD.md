# PRD — Email Marketing Manager v1.0

  **Status:** Shipped · v1.0.0 · [Changelog](CHANGELOG.md)
  **Owner:** Roger Gurbani

  ---

  ## Problem

  Newsletter knowledge doesn't compound. What subject-line patterns open, which CTAs convert per segment, what timing works — this lives in the head of whoever runs the newsletter, and it walks out the door when they do. Most teams never surface it deliberately at all. Each issue starts closer to zero than it should, and AI drafting tools reset to zero every session by design.

  ## Users

  - **Newsletter operators** (solo or small team) producing on a weekly/biweekly cadence
  - **Marketing teams** running segmented sends who can't afford per-segment copywriting time
  - **Agencies** producing newsletters for clients where institutional knowledge must survive staff changes

  ## What v1 does

  - Drafts the next issue from real documents: brand guide, personas, past newsletters, performance history — read from a connected Drive folder
  - Generates **segment variants** differentiated by audience type, not surface swaps
  - Applies the **substitution test** to body copy: if a paragraph would work for any brand, it gets revised
  - Produces a **performance prediction with rationale** on every draft, grounded in the account's own baselines
  - Closes the loop via `/track`: logs actuals, compares to prediction, extracts learnings, and writes them back to Drive (`newsletter-learnings.md`, `newsletter-baselines.md`) — the next `/create` reads them before drafting
  - Stores all accumulated knowledge as plain markdown any team member can read, audit, and correct

  ## What v1 explicitly does NOT do

  - **Does not send.** Drafts are delivered for human approval; the send happens on your email platform. The human gate before send is a feature, not a missing integration.
  - **Does not pull metrics automatically.** `/track` takes reported results; live platform sync is a connector-level extension, not core.
  - **Does not disaggregate performance by segment.** v1 tracks issue-level actuals; segment-level disaggregation is scoped for v1.1.
  - **Does not A/B test.** It generates subject-line options and predicts; running the test is the platform's job.
  - **Does not fine-tune on your sends.** Learnings are stored as readable, correctable markdown — if the system learns a wrong pattern, you edit the file.

  ## Success criteria

  - The learning loop demonstrably changes output: a draft produced after N tracked issues differs from a cold-start draft in ways traceable to lines in `newsletter-learnings.md` <!-- ⚠️ RAJ: run this comparison once on a test brand and describe one concrete example here — this is the whole product thesis in one sentence. -->
  - Segment variants pass a differentiation check: variants differ in angle and emphasis, not just greeting
  - Every `/create` includes a prediction with stated rationale referencing prior baselines (or explicitly states no baseline exists yet)
  - Prediction calibration improves across tracked issues <!-- ⚠️ RAJ: if you have even 3–5 tracked issues on a test account, state prediction vs. actual here. Honest early numbers beat no numbers. -->

  ## v1.1 roadmap

  - Segment-level performance disaggregation in `/track`

  ## Decision log

  - **Learning files over fine-tuning** — transparent, correctable, and portable; wrong patterns are a text edit, not a retraining run
  - **Prediction required on every draft** — a prediction creates accountability; `/track` comparing prediction to actual is what makes learnings specific
  - **Human gate before send** — the system optimizes the draft, not the decision to publish
  