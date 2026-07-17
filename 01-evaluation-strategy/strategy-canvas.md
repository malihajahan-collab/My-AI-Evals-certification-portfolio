# AI Evaluation Strategy Canvas

> Deliverable 1 of 5 for the AI Evals Certification final project.
> File: `ai-evals/01-evaluation-strategy/strategy-canvas.md`

## 1. Product Strategy, The Context

**Target user:** VP-level Strategists and Product Leaders at Fortune 500 companies who pay a premium for verified market intelligence.

**Key use case:** Rapidly extracting specific, verified insights (e.g., comparing competitor pricing models or summarizing G2 reviews) without manual data digging.

**Value proposition:** Personalized, instant answers based on verified data, dramatically reducing the time spent finding and synthesizing information for high-stakes decisions and strategic roadmaps.

## 2. Measurements, The Execution

**User promise.** For VP-level Enterprise Strategists, Ascend IQ helps produce a source-backed competitive insight brief in under 5 seconds, with every material claim traceable to a verified source, so leaders can make roadmap and pricing decisions without assigning manual research follow-up.

**Top 3 trust metrics:**
- **Latency**, Response speed (P95 / P99). Slow kills engagement.
- **Hallucination Rate**, % of outputs that are confidently false or fabricated.
- **Factuality / Grounding**, Outputs grounded in verified source data (RAG).

**Why these three:** • Hallucination, VP-level clients pay $50k+ for verified data; one fabricated stat ends the contract.
• Latency, <5s response is the only thing that beats manual digging.
• Factuality / Grounding, every claim must cite a primary source for compliance & auditability.

## 3. Strategic Trade-Offs, The Cost

### Trade-off 1 · Hallucination Rate ↔ Latency
We prioritize Hallucination Rate over Latency because Ascend IQ serves VPs making $1M+ strategic decisions; a single fabricated competitor stat ends a $50k contract, whereas a 3-second wait is the cost of doing business at Enterprise-grade integrity.

### Trade-off 2 · Fairness ↔ Hallucination Rate
We prioritize Fairness over peak Hallucination Rate because our European Enterprise expansion depends on consistent factual quality across English, German, and French, a slightly lower top-end score on English is acceptable for a 3x larger TAM.

---
_Generated from the AI Evaluation Strategy Canvas, M1 lab tool, AI Evals Certification._
