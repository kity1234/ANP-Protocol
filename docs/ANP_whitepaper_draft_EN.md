# SANP — Semantic Artificial Network Protocol
### A layered model for interoperability, distributed reasoning, and governance in artificial intelligence

**Document status:** Working draft (v0.1) — open proposal for discussion and critique
**Author:** Serge Olivier KITT
**Date:** July 2026
**License:** CC BY 4.0 — see `LICENSE-DOCS`

---

## Abstract

The current AI ecosystem is developing without a shared architectural grammar: every major actor (OpenAI, Google, Anthropic, the open-source community, national labs) is building its own interconnection protocols — MCP, A2A, proprietary formats — with no unifying framework to reason about the whole. This document proposes **SANP (Semantic Artificial Network Protocol)**, a conceptual layered model inspired by the OSI model but fundamentally adapted to the specific properties of AI: the probabilistic nature of these systems, the need to route by *meaning* rather than by address, and the requirement for ethical governance to be built in rather than added afterward.

ANP does not claim to solve every open problem in the field. It proposes a structure to name them clearly, and explicitly identifies the areas that remain active research rather than solved engineering.

---

## 1. Why a new model?

The OSI model (1984) and TCP/IP made internet interoperability possible by separating responsibilities into independent layers, each blind to the content of its neighbors. This principle — content-blindness — is what let the network carry an email as easily as a video without ever needing to "understand" what it was carrying.

AI structurally breaks with this principle. An AI system must **understand content** to function: routing a request to the right model requires interpreting its meaning, not just reading an address. ANP starts from this observation: this is not a *transport* model, it is a model of **distributed cognition**. The analogy with OSI remains pedagogically useful, but it should not be stretched beyond its actual relevance.

---

## 2. General architecture

ANP consists of **six numbered layers (0 to 5)** and **one transversal governance layer** that runs through all of them. This architectural choice — six layers rather than an arbitrarily reduced number — reflects the real complexity of the problem rather than a surface-level simplification.

| Layer | Name | Role | Closest OSI equivalent |
|---|---|---|---|
| 0 | Thermodynamic & Energy | Compute budget and sobriety | Absent from OSI |
| 1 | Infrastructure & Compute | Hardware, interconnection | Physical + Data Link |
| 2 | Cognitive Routing | Route by competence | Network |
| 3 | Interaction & Tool Calls | Agents ↔ outside world | Transport |
| 4 | Shared Semantics & Context | Interoperability of meaning | Absent from OSI |
| 5 | Persistent Memory | Conversation continuity | Absent from OSI |
| T | Governance & Verification | Ethics, alignment, trust | Transversal cryptography (TLS) |

---

## 3. Layer details

### Layer 0 — Thermodynamic & Energy

**Role.** Constrain the physical cost of computation. Every request carries an explicit budget (FLOPs, energy, carbon footprint). The model adapts the depth of its reasoning to this budget: a fast answer when the budget is low, a full tree-structured reasoning process when the budget is high.

**Open problem.** Nothing currently prevents an actor from declaring a false budget. A robust solution requires either a cryptographic proof of computation (see §5) or a trusted third party auditing actual consumption.

### Layer 1 — Infrastructure & Compute

**Role.** Standardize hardware interconnection (GPU, TPU, accelerators) independently of manufacturer. Defines a maximum admissible latency and a tensor exchange format, building on existing standards like ONNX.

**Status.** This is the layer closest to current state of the art — it formalizes more than it invents.

### Layer 2 — Cognitive Routing

**Role.** Direct a request to the most competent model, not to a fixed address. Each model publishes a **competence certificate**: an embedding vector summarizing its areas of expertise. The network routes by semantic similarity between the request and available certificates.

**Technical note.** This mechanism relies on continuous vector embeddings, where distance between two points reflects proximity of meaning — not on cryptographic hash functions, whose desired property (the avalanche effect) would be counterproductive here.

**Open problem.** A self-declared competence certificate is not proof of actual competence. See §5.

### Layer 3 — Interaction & Tool Calls

**Role.** Manage how an AI agent interacts with the outside world: APIs, databases, other agents, physical systems. This is the layer where existing protocols such as MCP (Model Context Protocol) naturally fit. It handles connection negotiation, execution timing, and error handling.

**Status.** The most mature layer — it builds on standards already seeing real industry adoption.

### Layer 4 — Shared Semantics & Context

**Role.** Allow models trained independently — on different data, architectures, and sometimes languages — to communicate intent without ambiguity. Rather than exchanging raw text, systems would exchange a **latent-space anchor**: a vector representation of intent, generated by an intermediate translator model.

**Open problem — the most critical in the model.** There is currently no guarantee that two independently trained models share a compatible latent-space geometry, even when facing the same idea. Research techniques exist (Procrustes alignment, canonical correlation analysis, cross-model contrastive learning) but none constitutes a proven general solution today. This layer formalizes a sound intuition, not a solved problem.

**Fallback procedure (inter-layer self-correction).** Layer 4 also acts as a consistency check on Layer 2's routing: if the initial intent vector doesn't match the response actually produced by the selected model, Layer 4 emits an explicit signal ("semantic mismatch detected") and sends the request back to Layer 2 for re-routing to a different model. This mechanism makes the protocol self-correcting rather than strictly sequential: a routing error is not silently propagated to the user, it triggers a new attempt. A maximum number of re-routing attempts should be defined to avoid infinite loops in cases of persistent ambiguity.

### Layer 5 — Persistent Memory

**Role.** Ensure conversational continuity beyond a single isolated session. This layer distinguishes two memory flows, by analogy with the cognitive distinction between episodic and semantic memory:

- **Episodic memory** — the "context ticket" proper: a compressed, volatile summary of history specific to a given session or user, allowing a system to never re-ask a question already addressed.
- **Semantic memory** — a persistent "world embedding," updated in the background, representing general knowledge accumulated independently of any particular conversation. Unlike the episodic ticket, this flow is not session-specific and evolves at a different pace.

This distinction enriches the layer without adding architectural complexity: both flows share the same transport mechanism but follow different rules for lifespan, granularity, and confidentiality.

**Point of caution.** The question of encryption and key custody for both flows directly intersects with the data sovereignty issues addressed by the transversal layer — the two should not be designed independently (see §4, "Local right to erasure").

---

## 4. The transversal layer — Governance & Verification

Unlike a peripheral firewall that would inspect requests at the network's edge, the governance layer is designed to be **intrinsic**: embedded in the headers of every packet, across every layer, rather than added as a single bypassable barrier. This choice addresses a known weakness of peripheral filtering systems in AI safety: a filter placed only at the edge can be circumvented through rephrasing, precisely because it lacks the same depth of understanding as the system it is meant to protect. Alignment must therefore be carried both by the training of the models themselves (Layer 2 and beyond) and by this transversal safety net — not by the latter alone.

**Local right to erasure (optional track, oriented toward regulatory compliance).** In a future iteration of the standard, the governance layer could require that the episodic memory context ticket (Layer 5) be encryptable with a key held exclusively by the end user, not the model provider. This principle, distinct from provider-managed persistent semantic memory, would offer a guarantee of effective deletion of conversational data — a compliance argument particularly relevant with respect to regulatory frameworks such as the European GDPR.

---

## 5. The central problem: declarative vs. verifiable

The structural weakness shared by Layers 0, 2, and T is the following: **a system can declare a property (budget, competence, alignment) without that declaration being verifiable by construction.** This is the same challenge that TLS and certificate authorities partially solved for secure communications. ANP proposes treating this question as a standalone axis rather than an implementation detail, by combining four complementary mechanisms — none sufficient on its own:

1. **Cryptographic hardware attestation** (inspired by secure enclaves such as TPM, SGX, SEV) — guarantees execution integrity of a model, without guaranteeing its competence or alignment.
2. **Independent third-party certification**, periodic, from a body not affiliated with major actors — modeled on dangerous-capability evaluators already active in the field (for example, METR). Weakness: certification is a point-in-time snapshot; a model can drift afterward.
3. **Continuous reputation from observation**, self-correcting over time as real-world performance diverges from declarations. Weakness: leaves a window of exploitation before detection.
4. **Zero-knowledge proofs**, an active research field allowing proof that a computation respected a constraint without exposing the computation itself — particularly relevant for verifying Layer 0's declared budget.

None of these four mechanisms alone solves the problem of distributed trust in AI. Their combination, and the explicit acknowledgment of their respective limits, is proposed here as a direction for work rather than a settled solution.

---

## 6. Acknowledged limitations of this document

This whitepaper is a proposed structure, not a finalized, implementable-as-is protocol. Three limitations deserve to be named directly:

- Layer 4 (semantics) relies on a research hypothesis not yet validated at general scale.
- The arbitration mechanism for disagreement between models deliberating in parallel (particularly relevant as an extension of Layer 2) remains to be formalized.
- The governance of trust (§5) identifies existing approaches rather than an original, complete solution.

A model that claimed to have none of these limitations would be less credible, not more.

---

## 7. Proposed next steps

- Cross-check this model against existing literature (papers on multi-agent protocols, MCP and A2A specifications, work on cross-model alignment) to refine terminology and avoid restating existing work under a new name.
- Open a public discussion (issue tracker, dedicated forum) to gather community technical critique before any claim to standard status.
- Explore a proof-of-concept implementation limited to Layer 3 (Interaction), the most mature layer, as a tangible demonstration of the full model.

---

## Appendix — Version history

- **v0.1** — Initial formulation of the six layers and the transversal layer, developed through iterative dialogue; integrated the embedding reformulation (Layer 2), the clarified actual layer count, the verification/trust section (§5), the episodic/semantic memory split (Layer 5), the Layer 4 fallback mechanism, and the local right-to-erasure principle (§4).
