# Connectors

Email Marketing Manager is tool-agnostic — it describes workflows in terms of categories rather than specific products. When you see a `~~placeholder` in a command or skill, it refers to a category of tool, not a specific one.

## Connector Categories

| Category | Placeholder | What It Does | Example Tools |
|----------|------------|--------------|---------------|
| Documents + Images | `~~docs` | Source of truth for everything — brand guide, audience personas, past newsletters, performance data, and images | Google Drive, Notion, Dropbox |
| Email | `~~email` | Newsletter platform — subscriber data, send metrics, draft posting, scheduling | Beehiiv, Mailchimp, ConvertKit, Klaviyo |

## How Connectors Enhance Commands

| Command | Works standalone? | Enhanced by |
|---------|:-:|---|
| `/setup` | — | `~~docs` (required — this is how client context loads) |
| `/run` | ✅ works with whatever context is available | `~~docs` (reads standing orders, learning files, topic queue) |
| `/create` | ✅ describe brand and audience | `~~docs` (reads brand guide, personas, past newsletters, images), `~~email` (posts draft to platform) |
| `/track` | ✅ paste results manually | `~~email` (pulls real send metrics automatically) |

## The Images Pattern

Images for newsletters live in your Google Drive folder — typically in an `images/` subfolder. This replaces the need for a separate asset management tool. When `/create` runs, it reads available images from Drive and selects ones that match the newsletter topic and angle.

No Cloudinary. No separate image platform. Your Drive folder has your brand docs AND your images. One folder, everything the newsletter needs.

## Learning Files

The `/track` command writes three files back to your Drive folder:

- `newsletter-log.md` — record of every newsletter sent
- `newsletter-learnings.md` — cumulative insights from tracked results
- `newsletter-baselines.md` — current performance baselines per segment

These are plain markdown. You can read them, edit them, share them. The system's intelligence is transparent — not hidden in a database.

## The Drive Protocol pattern

One Google Drive folder per client. Every command reads from it. `/track` writes back to it. That folder becomes the persistent memory for the system. It compounds over time instead of resetting each session.

## Configuring Connectors

Edit `.mcp.json` to point at your specific tools. The plugin gracefully degrades when tools are unavailable — it notes what's missing and works with what you provide directly.

The core connector is `~~docs` (Google Drive). This is what makes the system client-aware — your documents, your images, your learning history. Without it, you can still paste context and get newsletters, but you'll repeat yourself every time and the learning loop won't persist.
