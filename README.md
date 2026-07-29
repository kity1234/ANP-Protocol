# ANP — Artificial Network Protocol
### A layered model for interoperability, distributed reasoning, and governance in artificial intelligence

![Status: Draft v0.1](https://img.shields.io/badge/status-draft-orange)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen)

---

## In one sentence

**ANP is a conceptual model that treats AI-to-AI communication as a distinct architectural problem** — one that classic network protocols were never designed to solve, because they route bits, not meaning.

---

## Why this project exists

The current AI ecosystem is growing without a shared architectural grammar. OpenAI, Google, Anthropic, the open-source community, and national labs are each building their own interconnection protocols — MCP, A2A, proprietary formats — with no unifying framework to reason about the whole.

Classic network models like OSI and TCP/IP solved interoperability by staying deliberately blind to content: a router doesn't need to understand an email to deliver it. AI breaks that assumption. Routing a request to the right model, or letting two independently trained systems exchange intent, requires interpreting meaning — something OSI was never built to do.

> ANP is not a transport protocol. It's a proposal for **distributed cognition**.

This is a working draft, not a finished standard. It's published to invite scrutiny, not to claim authority.

---

## Documentation

- **Whitepaper (EN):** [`docs/ANP_whitepaper_draft_EN.md`](docs/ANP_whitepaper_draft_EN.md)
- **Whitepaper (FR):** [`docs/ANP_whitepaper_draft.md`](docs/ANP_whitepaper_draft.md)
- **Architecture diagram:** [`docs/diagrams/anp_layers.svg`](docs/diagrams/anp_layers.svg)
- **Governance:** [`GOVERNANCE.md`](GOVERNANCE.md) · **Contributing:** [`CONTRIBUTING.md`](CONTRIBUTING.md)

---

## Architecture overview: 6 layers + 1 transversal layer

| Layer | Name | Core role |
|---|---|---|
| **0** | Thermodynamic & Energy | Computation budget and sobriety by design. Each request carries a FLOPs/energy quota that shapes reasoning depth. |
| **1** | Infrastructure & Compute | Hardware standardization (GPU, TPU) and tensor exchange formats, building on existing work like ONNX. |
| **2** | Cognitive Routing | Routes by *competence* (a vector embedding), not by fixed address. Each model publishes a competence certificate. |
| **3** | Interaction & Tool Calls | How agents talk to the outside world — APIs, other models, physical systems. This is where protocols like MCP naturally fit. |
| **4** | Shared Semantics & Context | Interoperability of meaning via latent-space anchors. Includes a fallback mechanism: semantic mismatch triggers re-routing back to layer 2. |
| **5** | Persistent Memory | Splits episodic memory (session-bound context ticket) from semantic memory (a persistent, slower-updating world embedding). |
| **T** | Governance & Verification *(transversal)* | Ethics, alignment, traceability, and trust — embedded across every layer rather than bolted on at the edge. |

---

## What's genuinely new here

Two design choices stand out:

- **Layer 2 + Layer 0 together**: requests are routed by meaning rather than address, *and* constrained by an explicit energy budget — coupling semantic routing with physical cost in a way we haven't seen formalized elsewhere.
- **Layer 4 is not passive**: if a model's response doesn't match the original intent vector, the layer triggers an automatic re-route rather than silently passing along a bad answer. The network is designed to self-correct.

---

## The central open problem: declarative vs. verifiable

> A system can *declare* a property — budget, competence, alignment — without that declaration being independently verifiable.

ANP doesn't claim to solve this. It proposes combining four complementary mechanisms, each insufficient alone:

1. **Hardware attestation** (TPM/SGX-style enclaves) — proves execution integrity, not competence.
2. **Independent third-party certification** — periodic audits, similar in spirit to existing dangerous-capability evaluators.
3. **Continuous reputation** — self-correcting over time, but leaves a window of exploitation before drift is detected.
4. **Zero-knowledge proofs** — an active research area, particularly relevant for verifying layer 0's declared budget without exposing the underlying computation.

---

## Known limitations

A model that claimed to have no limitations would be less credible, not more.

- **Layer 4** rests on a research hypothesis — cross-model latent space alignment — that isn't solved at general scale today.
- The **arbitration mechanism** for genuine disagreement between models deliberating in parallel is sketched, not formalized.
- The **trust and verification** section (above) surveys existing approaches rather than proposing an original, complete solution.

---

## Roadmap

- [x] Conceptual model formulated (v0.1)
- [ ] Cross-check against existing academic literature (multi-agent protocols, MCP/A2A specs, cross-model alignment research)
- [ ] Open public discussion (issues, forum)
- [ ] Proof-of-concept implementation limited to Layer 3 (Interaction) — the most mature layer

---

## Contributing

This isn't a closed proposal — it's a starting point for critique.

- **Network architects**: tell us where this violates the robustness principles that made the internet work.
- **AI researchers**: tell us whether Layer 4 (Semantics) is a dead end or a viable direction.
- **ML engineers**: tell us which layer you'd actually start prototyping tomorrow.
- **Skeptics**: tell us why this is unnecessary or risky.

Open an issue or submit a pull request — disagreement is welcome and expected at this stage.

---

## Support this project

ANP is developed independently, without institutional or corporate backing. If you'd like to help fund the next step — a proof-of-concept implementation limited to Layer 3 (Interaction), which requires compute resources — here's how:

- **Bitcoin:** 1EDrde4DHf1p8Vm34Rmax1SRzXNZiooRf7
- **Open Collective:** [https://opencollective.com/anp-protocol](https://opencollective.com/anp-protocol) — full transparency on funds in and out
- **GitHub Sponsors:** not yet available for this maintainer's region

No pressure, no tiers, no perks — just a way to support independent work if it's useful to you.

---

## License & Author

- **Author:** Serge Olivier KITT
- **Initial draft:** July 2026
- **License:** Code under MIT (`LICENSE`) — Written content (whitepaper, README) under CC BY 4.0 (`LICENSE-DOCS`)
