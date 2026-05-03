# Drive Protocol

Drive Protocol is the persistent memory layer behind Editorial OS.

## Principle

One Google Drive folder per client.
Every specialist reads from it.
Learning specialists write back to it.
That folder becomes the shared operating memory for the system.

## Why this matters

Most AI workflows are still too stateless.

A person restates context, gets an output, gives feedback, and then has to manually carry the useful learning forward into the next task. That is fragile, repetitive, and hard to scale.

Drive Protocol fixes that by making memory explicit, shared, and transparent.

## What lives in the folder

Shared client memory can include:
- brand guide
- audience personas
- content strategy
- past outputs
- images
- analytics exports
- competitive research
- specialist logs
- learning files
- baseline files

## Design rules

- The documents are the config.
- Shared memory should be human-readable.
- The client should be able to inspect and edit what the system learns.
- Specialists should read from the same folder rather than recreating context in isolation.
- Learning files should be written back in markdown so they compound over time.

## Email Marketing Manager example

For Email Marketing Manager, Drive Protocol powers the learning loop.

The specialist reads:
- brand voice,
- audience segments,
- past newsletters,
- image inventory,
- and prior learning files.

Then it writes back:
- newsletter-log.md
- newsletter-learnings.md
- newsletter-baselines.md
- dated draft records

That means `/run`, `/create`, and `/track` all improve as the folder gets richer.

## Transparency is a feature

The system should not hide memory in a black box.

A client should be able to open the folder and understand:
- what the specialist saw,
- what it produced,
- what it learned,
- and why the next recommendation changed.

That transparency makes the system more trustworthy and more useful over time.
