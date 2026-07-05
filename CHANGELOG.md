# Changelog

  All notable changes to Email Marketing Manager are documented here.
  Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/). Versioning follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

  ## [Unreleased]

  ### Planned
  - Segment-level performance disaggregation in `/track`

  ## [1.0.0] — 2026-07-05

  ### Added
  - 4 commands: `/setup`, `/run`, `/create`, `/track`
  - 3 skills: `client-context`, `email-strategist`, `performance-learning`
  - Persistent learning loop: actuals → learnings → baselines → next draft
  - Segment variant generation by audience type on every `/create`
  - Performance prediction with rationale on every `/create`
  - Learning files written back to Drive as plain markdown: `newsletter-log.md`, `newsletter-learnings.md`, `newsletter-baselines.md`
  - Graceful degradation without connectors documented in `CONNECTORS.md`

  [Unreleased]: https://github.com/EditorialOS/email-marketing-manager/compare/v1.0.0...HEAD
  [1.0.0]: https://github.com/EditorialOS/email-marketing-manager/releases/tag/v1.0.0
  