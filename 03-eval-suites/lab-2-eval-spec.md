# Lab 2 · Eval Spec · Ascend IQ Pricing Integrity

## Five-part Eval Spec

### 1. Target risk

- **Failure mode:** Fabricated or stale Enterprise pricing, including unsupported or contradicted prices, currencies, discounts, seat minimums, and contract terms.
- **Risk type:** Output — final-answer factuality.
- **Trust metric:** Hallucination.
- **Severity:** P0.

### 2. Evaluator

**Hybrid evaluation:**

1. A deterministic gate extracts every pricing claim and compares it with the versioned approved pricing source. Any mismatched or unsupported claim blocks the response.
2. A semantic LLM-as-Judge from a different model family runs against the versioned pricing regression set to detect paraphrased, implied, or context-dependent contradictions that deterministic matching may miss.

The product-wide safety/refusal evaluator remains active, but it is not counted as a pricing-factuality control.

### 3. Threshold and strategy

- **Strategy:** Safety First.
- **Threshold:** 100% of pricing claims must be supported by the approved pricing source.
- **Critical-failure tolerance:** Zero contradicted or unsupported critical pricing claims.
- **Judge calibration floor:** Cohen’s κ ≥ 0.60 against human labels.
- **Release rule:** Any critical pricing failure blocks release.

### 4. Business stakes

An unsupported price can mislead a customer’s strategic decision, trigger contract disputes or legal review, and jeopardize a $50K+ Enterprise account. The control protects Ascend IQ’s promise of verified, citation-backed intelligence for customers making high-stakes decisions.

### 5. Owner

The **Group PM** is accountable for the release policy and risk acceptance. The **Engineering Lead** is responsible for implementing the gate, maintaining the approved-source integration, enforcing blocks, and operating rollback.

## Three audience messages

### A. Engineering · Jira acceptance criteria

> **GIVEN** a user requests pricing and the generated response contains a price, currency, discount, seat minimum, or contract term, **WHEN** any claim is absent from or contradicts the versioned approved pricing source, **THEN** block the response and trigger the approved pricing fallback.
>
> Release requires 100% support across all pricing fixtures, zero critical pricing failures, and Cohen’s κ ≥ 0.60 for the semantic judge.

### B. UX / Design · Fallback experience

> When pricing cannot be verified, do not show the generated price. Preserve the conversation and display: “I can’t verify the latest Enterprise pricing. View the approved pricing source or contact Sales for a current quote,” with both actions available. Do not expose a raw error, blank response, or unverified price.

### C. Leadership · Bi-weekly update

> Enforcing zero unsupported pricing claims protects $50K+ Enterprise accounts from contract disputes and legal review. Coverage target: 100% of versioned pricing fixtures, with critical failures blocking release and results reviewed weekly.
