# Connectors

Email Marketing Manager uses three connectors — one for each job in the newsletter pipeline.

## Connector Stack

| Connector | Job | MCP Server | What It Does |
|-----------|-----|------------|--------------|
| **Cloudinary** | Images | `cloudinary` | Image library for newsletter assets. The `/email-marketing-manager:create` command queries Cloudinary for available images and selects from a verified candidate list — no hallucinated filenames, no broken URLs. |
| **Box** | Client documents | `box` | Source of truth for brand guide, audience personas, past newsletters, performance data, and learning files. One Box folder per client. |
| **Beehiiv** | Email platform | `beehiiv` | Newsletter ESP — posts drafts on paid plans, pulls send metrics, and provides subscriber data. Closes the loop between `/email-marketing-manager:create` and `/email-marketing-manager:track`. |

## How Connectors Enhance Commands

| Command | Works standalone? | Enhanced by |
|---------|:-:|---|
| `/email-marketing-manager:setup` | — | **Box** (required — this is how client context loads) |
| `/email-marketing-manager:run` | ✅ works with whatever context is available | **Box** (reads standing orders, learning files, topic queue) |
| `/email-marketing-manager:create` | ✅ describe brand and audience | **Cloudinary** (verified image selection), **Box** (reads brand guide, personas, past newsletters), **Beehiiv** (posts draft to platform) |
| `/email-marketing-manager:track` | ✅ paste results manually | **Beehiiv** (pulls real send metrics automatically), **Box** (writes learning files) |

## The Closed-List Image Pattern

Images come from Cloudinary — not from a document folder, not from a URL you guess at.

Before the newsletter is drafted, the system queries Cloudinary for available assets matching the newsletter's topic and context. It returns a **closed candidate list**: asset IDs, delivery URLs, dimensions, format, and metadata. The drafting step may only reference images from this list. An ID not in the list does not exist.

This pattern prevents the single most common failure in AI image selection: hallucinating an asset that looks plausible but doesn't exist, producing a broken newsletter.

### Image roles

| Role | Dimensions | Aspect | Use |
|------|-----------|--------|-----|
| Hero | 1200 × 600 | 2:1 | Top of newsletter, full width |
| Section | 1200 × 675 | 16:9 | Section dividers, inline features |
| Item | 600 × 600 | 1:1 | Product shots, headshots, thumbnails |
| Divider | — | — | Decorative separator |

### Alt text rule

Every image gets alt text. If nobody has visually confirmed what the image shows, mark it `ALT PENDING`. A plausible guess at alt text is a fabrication — treat it as one.

## Learning Files

The `/email-marketing-manager:track` command writes three files back to your Box folder:

- `newsletter-log.md` — record of every newsletter sent
- `newsletter-learnings.md` — cumulative insights from tracked results
- `newsletter-baselines.md` — current performance baselines per segment

These are plain markdown. You can read them, edit them, share them. The system's intelligence is transparent — not hidden in a database.

## The Box Protocol

One Box folder per client. Every command reads from it. `/email-marketing-manager:track` writes back to it. That folder becomes the persistent memory for the system. It compounds over time instead of resetting each session.

### Folder structure that works best

```
Your Brand Folder/
├── brand-guide.md         (or .pdf, .docx — any format)
├── audience-personas.md
├── past-newsletters/      ← examples of what you've sent before
├── performance/           ← open rates, click rates, any data you have
├── newsletter-log.md      ← written by /email-marketing-manager:track
├── newsletter-learnings.md
└── newsletter-baselines.md
```

Images live in Cloudinary, not in the document folder. One system per job.

## Authorizing Connectors

The plugin ships Anthropic-compatible remote MCP definitions in `.mcp.json`. After installation, run `/mcp` in Claude and complete OAuth for Cloudinary, Box, and Beehiiv. Do not place API keys or access tokens in this repository.

Beehiiv exposes read access on all plans, while creating or editing drafts through its MCP server requires a paid Beehiiv plan. If write access is unavailable, the plugin returns paste-ready newsletter copy instead.

The plugin gracefully degrades when a connector is unavailable: it states what is missing and works with what the user provides directly.

### Degradation Behavior

| Level | What's Connected | System Capability |
|:---:|---|---|
| Full | Cloudinary + Box + Beehiiv | Complete: verified images, full context, posts drafts, pulls metrics, learning loop persists |
| Docs + Images | Cloudinary + Box | Strong: verified images, full context, saves records. User pastes metrics for /email-marketing-manager:track, copies draft to ESP. |
| Docs only | Box | Moderate: full context, no verified images (suggest what images would help), manual metrics, manual draft posting. |
| Manual | Nothing | Functional: user pastes brand context and past examples. Newsletter quality depends on what's provided. No persistent learning. No verified images. |

Never block a command because connectors are missing. Degrade gracefully. State what's missing and what it costs — then do the best work possible with what's available.
