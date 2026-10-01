# Document Protocol

Document Protocol is the persistent memory layer behind Editorial OS.

## Principle

One Box folder per client.
Every specialist reads from it.
Learning specialists write back to it.
That folder becomes the shared operating memory for the system.

Images live in Cloudinary — one system per job.
Newsletter operations run through Beehiiv.

## Why this matters

Most AI workflows are still too stateless.

A person restates context, gets an output, gives feedback, and then has to manually carry the useful learning forward into the next task. That is fragile, repetitive, and hard to scale.

Document Protocol fixes that by making memory explicit, shared, and transparent.

## What lives in the Box folder

Shared client memory can include:
- brand guide
- audience personas
- content strategy
- past outputs
- analytics exports
- competitive research
- specialist logs
- learning files
- baseline files

Images live in Cloudinary, not in the document folder.

## Design rules

- The documents are the config.
- Shared memory should be human-readable.
- The client should be able to inspect and edit what the system learns.
- Specialists should read from the same folder rather than recreating context in isolation.
- Learning files should be written back in markdown so they compound over time.

## Email Marketing Manager example

For Email Marketing Manager, Document Protocol powers the learning loop.

The specialist reads from Box:
- brand voice,
- audience segments,
- past newsletters,
- and prior learning files.

It reads from Cloudinary:
- image inventory (verified candidate list)

Then it writes back to Box:
- newsletter-log.md
- newsletter-learnings.md
- newsletter-baselines.md
- dated draft records

And it posts to Beehiiv:
- newsletter drafts (never auto-sent)

That means `/email-marketing-manager:run`, `/email-marketing-manager:create`, and `/email-marketing-manager:track` all improve as the folder gets richer.

## Transparency is a feature

The system should not hide memory in a black box.

A client should be able to open the folder and understand:
- what the specialist saw,
- what it produced,
- what it learned,
- and why the next recommendation changed.

That transparency makes the system more trustworthy and more useful over time.
