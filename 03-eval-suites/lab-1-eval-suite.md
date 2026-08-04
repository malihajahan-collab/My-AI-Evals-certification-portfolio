# Lab 1a · Three-Layer Eval Suite · Ascend IQ

## P0 case

- **Failure:** Fabricated / stale Enterprise pricing
- **Trust metric:** Hallucination
- **Severity:** P0
- **Query:** What is InsightFlow's pricing for Enterprise?
- **Prediction:** InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- **Reference:** InsightFlow Enterprise is $59/user/month; the 10-seat minimum is correct.

## Three-layer results

Scores use the lab convention: **1 = caught the P0 failure; 0 = missed it**.

| Layer | Role | Score | Result and reasoning |
|---|---|---:|---|
| Layer 1 · Code | Compliance logic script (regex/keyword) | **0 · Missed** | The rule checked whether pricing language included the phrase “subject to change.” It did not compare the stated `$49/user/month` with the approved `$59/user/month` price, so it missed the factual pricing error. |
| Layer 2 · Safety | Legal compliance auditor (policy gate) | **0 · Missed / not applicable** | The query contained neither “lawsuit” nor “litigation,” so the policy gate correctly allowed it. This layer does not evaluate pricing factuality and therefore did not catch the P0 failure. |
| Layer 3 · Judge | Meticulous QA analyst (LLM-as-Judge) | **1 · Caught** | The judge identified that `$49/user/month` was outdated and contradicted the approved `$59/user/month` reference. It also confirmed that the 10-seat minimum was correct. |

## Where the failure was caught, and what it means

Only Layer 3, the LLM-as-Judge, caught the outdated `$49/user/month` price by comparing it with the approved `$59/user/month` reference. Layer 1 checked for disclaimer language rather than factual price accuracy, while Layer 2 correctly treated the query as allowed but could not assess pricing. This is **The Insight**: semantic evaluation works, but the P0 risk currently depends on the slowest and most expensive layer.

## What I would ship next

Ship a two-stage pricing guardrail:

1. **Layer 1 · Hard deterministic gate:** Extract every pricing claim and compare it with the versioned approved pricing source. Any mismatched or unsupported price, currency, discount, seat minimum, or contract term blocks the response and triggers a safe fallback.
2. **Layer 3 · Pre-release semantic judge:** Replay the pricing regression dataset to catch paraphrased, implied, or context-dependent pricing errors that deterministic matching misses. Require zero critical pricing failures.

Keep Layer 2 as the product-wide safety/refusal gate, but do not treat it as a pricing control. Acceptance criteria and ownership will be formalized in `03-eval-suites/lab-2-eval-spec.md`.

This is the highest-leverage change because it moves the obvious `$49` versus `$59` mismatch into the cheapest and fastest layer while retaining semantic coverage for edge cases.
