# Changelog

All notable changes to Email Marketing Manager are documented here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and versioning follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned

- Segment-level performance disaggregation in `/email-marketing-manager:track`

## [2.0.1] — 2026-09-30

### Fixed

- Conformed the package to Anthropic's current plugin manifest, command frontmatter, skill discovery, and MCP schemas.
- Added complete manifest attribution, repository, license, discovery keywords, and JSON Schema metadata.
- Removed unsupported MCP server keys and retained the official OAuth endpoints for Cloudinary, Box, and Beehiiv.
- Corrected invalid command YAML frontmatter that previously caused Claude to discard command metadata.
- Documented canonical namespaced commands and added strict Anthropic plugin validation in CI.

## [2.0.0] — 2026-09-30

### Added

- Cloudinary closed-list asset selection with verified public IDs, delivery URLs, and dimensions.
- Five-gate editorial review: Voice, Angle, Structure, Image Integrity, and Segment Fit.
- Beehiiv draft creation and metric retrieval.
- Box-backed client context and persistent learning files.
- Graceful degradation from the full connector stack to a fully manual workflow.

## [1.0.0] — 2026-07-05

### Added

- Four commands: `/email-marketing-manager:setup`, `/email-marketing-manager:run`, `/email-marketing-manager:create`, and `/email-marketing-manager:track`.
- Three skills: `client-context`, `email-strategist`, and `performance-learning`.
- Persistent learning loop: actuals → learnings → baselines → next draft.
- Segment variants and performance predictions.

[Unreleased]: https://github.com/EditorialOS/email-marketing-manager/compare/v2.0.1...HEAD
[2.0.1]: https://github.com/EditorialOS/email-marketing-manager/compare/v2.0.0...v2.0.1
[2.0.0]: https://github.com/EditorialOS/email-marketing-manager/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/EditorialOS/email-marketing-manager/releases/tag/v1.0.0
