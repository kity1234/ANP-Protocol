# Governance

ANP is maintained by a single author at this stage (v0.1). This document explains how decisions are made today, and how that is expected to change as the project matures.

## Current model: benevolent maintainer, open critique

- **Serge Olivier KITT** is the sole maintainer and has final say on merges to `main`.
- This is not meant to last. It reflects where the project actually is — an early draft, not a mature standard — not a claim to permanent authority over it.
- Anyone can open an issue or a pull request. No prior approval is needed to propose a change, only to merge one.

## How decisions get made

- **Editorial / wording changes** (typos, clarity, translation): reviewed and merged directly, no discussion required.
- **Structural changes** (a layer's role, a new mechanism, a naming change): must go through an issue first, open for at least a few days, before any pull request is merged. This gives people time to weigh in rather than discovering a change after the fact.
- **Disputed or high-stakes changes** (especially anything touching Layer 4's semantic model, Layer 0's verification mechanisms, or Layer T's governance principles): the maintainer will summarize the discussion publicly before deciding, and will explain the reasoning behind the final call — even when it doesn't follow the majority of comments.

## What happens as the project grows

If ANP attracts a sustained group of active contributors, the intent is to move toward a **working-group model**: informal groups organized around specific layers (e.g. a Layer 4 semantic-alignment group, a Layer 0 verification group), each able to propose changes to their area with lighter friction than a single maintainer reviewing everything alone.

A formal governance body (steering committee, foundation, or similar) is not being set up preemptively. Setting one up before there's a real community to govern would be governance theater, not governance.

## What this project will not do

- It will not accept funding or partnership terms that require closed-sourcing any part of the protocol specification.
- It will not grant any single company or organization veto power over the direction of a layer in exchange for funding or endorsement.

## Versioning

Substantive changes to the model are logged in the whitepaper's version history section (see `docs/ANP_whitepaper_draft_EN.md`), not silently merged without a trace.
