---
description: Inspect current context — standing orders, topic queue, learning files, and gaps — then decide the next best action for the newsletter workflow. The operator command that makes the specialist feel like a teammate.
argument-hint: No argument needed — reads state automatically
---

# /run

Inspect current context and decide the next best action for the newsletter workflow.

## Purpose

`/run` is the operator command.

It makes Email Marketing Manager feel like a teammate instead of a static prompt by checking the current state before doing work.

## What it reads

- standing orders
- topic queue
- brand and audience context
- prior newsletter records
- newsletter learnings
- newsletter baselines
- any missing inputs that would block a strong draft

## What it decides

Based on the current state, `/run` should decide whether to:
- proceed to `/create`
- request a missing input
- prepare for `/track`
- surface a decision the human needs to make

## Output

The output should be short and operational:
- current status
- next recommended action
- reason for that action
- what is missing, if anything
- what file or queue item informed the recommendation

## Why it matters

`/run` is what connects the command surface to the learning loop.

It ensures the specialist is acting on the latest memory, standing orders, and workflow state instead of blindly producing another draft.
