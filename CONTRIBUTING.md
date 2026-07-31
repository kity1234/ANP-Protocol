# Contributing to SANP

SANP is a working draft, not a finished standard. It's published specifically to be challenged, tested, and improved by people who know things the author doesn't. If you're reading this, you're not too early and you don't need permission to disagree.

## What kind of contributions are useful right now

At this stage (v0.1), the most valuable contributions are **critical**, not additive:

- **Structural critique** — does this model violate a robustness or security principle that made the internet work? Say so, and cite the precedent if you can.
- **Prior art** — if a paper, protocol (MCP, A2A, or others), or research direction already solves something ANP treats as an open problem (especially Layer 4's cross-model semantic alignment), point us to it. Duplicating existing work under a new name helps no one.
- **Falsifiability** — if you can describe a concrete scenario where a layer breaks, that's worth more than a paragraph of praise.
- **Implementation feasibility** — Layer 3 (Interaction) is the most mature and the first candidate for a proof of concept. If you'd prototype it differently, open an issue.

## How to contribute

1. **Open an issue first** for anything structural — a change to a layer's role, a new mechanism, a naming change. This keeps discussion visible and avoids duplicated effort.
2. **Pull requests** are welcome for the whitepaper and README (typos, clarity, translations) without prior discussion. For anything touching the architecture itself, please open an issue first.
3. **Disagreement is not required to be polite about being technical.** Bluntness is fine. Personal attacks are not.

## What this project is not (yet)

It is not an implemented protocol, not a company, and not a claim of authority over how AI systems should communicate. Treat it as a proposal for a conversation the field hasn't fully had yet.

## Versioning

Substantive changes to the model (new layers, removed mechanisms, changed semantics) should be logged in the whitepaper's version history section, not silently merged.
