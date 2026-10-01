---
description: "Inspect standing orders, the topic queue, learning files, connector state, and gaps, then recommend the next newsletter action."
argument-hint: "No arguments"
---

# /email-marketing-manager:run

Inspect current context and decide the next best action for the newsletter workflow.

## Purpose

`/email-marketing-manager:run` is the operator command.

It makes Email Marketing Manager feel like a teammate instead of a static prompt by checking the current state before doing work.

## What it reads

- standing orders (from Box folder)
- topic queue
- brand and audience context (from Box)
- Cloudinary image library status
- prior newsletter records
- newsletter learnings
- newsletter baselines
- Beehiiv connection status
- any missing inputs that would block a strong draft

## What it decides

Based on the current state, `/email-marketing-manager:run` should decide whether to:
- proceed to `/email-marketing-manager:create`
- request a missing input
- prepare for `/email-marketing-manager:track`
- surface a decision the human needs to make

## Output

The output should be short and operational:
- current status
- next recommended action
- reason for that action
- what is missing, if anything
- what file or queue item informed the recommendation

## Why it matters

`/email-marketing-manager:run` is what connects the command surface to the learning loop.

It ensures the specialist is acting on the latest memory, standing orders, and workflow state instead of blindly producing another draft.
