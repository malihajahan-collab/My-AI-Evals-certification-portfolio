# Lab 1 · Eval Gate Map · Ascend IQ

## Gate definitions

- **Hard:** Automatically blocks promotion when the threshold fails.
- **Soft:** Requires documented review and approval before promotion.
- **Advisory:** Warns and creates a follow-up action but does not block promotion.

## Gate map

| Row | Failure mode | Severity | Primary placement | Rationale |
|---:|---|:---:|---|---|
| 01 | Hallucination · Stale Pricing | **Hard** | **Pull Request** | A versioned pricing fixture can catch the `$49` versus `$59` contradiction cheaply before Staging. Incorrect customer-facing pricing can jeopardize $50K+ Enterprise contracts, trigger disputes, and create legal-review exposure. |
| 17 | Tone · Slang Detected | **Advisory** | **Pull Request** | A deterministic keyword and brand-style check can warn developers immediately. Ordinary slang may reduce enterprise credibility and campaign effectiveness, but it does not justify blocking an otherwise safe release. |
| 05 | Hallucination · False Promise | **Hard** | **Staging** | Entity validation and claim-to-source entailment must prevent unsupported external commitments. Invented speaker confirmations can cause public retractions, partner escalation, and erosion of customer trust. |
| 08 | Hallucination · Unsupported Competitor Claim | **Hard** | **Staging** | Source-grounded semantic evaluation is required for comparative claims. Unsupported statements about a named competitor can cause disputes, legal-review costs, false-advertising or defamation exposure, and brand damage. |
| 03 | Latency · Exceeded Maximum Threshold | **Soft** | **Staging** | Production-like model, retrieval, and concurrency testing is needed to measure end-to-end latency. Sustained delays can reduce adoption, increase abandonment, and contribute to enterprise churn, while documented workload exceptions may justify approval. |

## Layered enforcement

The primary placement is the earliest decisive gate, not the only control:

- **Pull Request:** deterministic source comparisons, entity and keyword rules, style checks, and replayed fixtures with no live model calls.
- **Staging:** semantic entailment, unseen variations, retrieval behavior, and production-like performance tests.
- **Release:** defense-in-depth checks, approved exceptions, rollback readiness, and final promotion state.

The semantic LLM-as-Judge is not approved as a blocking control while calibration remains at **Cohen’s κ = −0.286**. Hard semantic gates require either deterministic enforcement or a recalibrated judge meeting **κ ≥ 0.60**. Until then, failure to establish an approved blocking control holds promotion for the affected P0/P1 claim class.

## Sample-interaction references

### Row 01 · Stale Pricing

- **Input:** What is InsightFlow's pricing for Enterprise?
- **Output:** InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- **Verified failure:** The approved price is $59/user/month.

### Row 17 · Slang Detected

- **Input:** Draft a cold email about our new feature.
- **Output:** Hey! Check out this killer new feature, it's a total game changer for your stack!
- **Verified failure:** “Killer” and “game changer” violate the professional brand voice.

### Row 05 · False Promise

- **Input:** List the confirmed speakers for SaaStr.
- **Output:** Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman.
- **Verified failure:** Sam Altman is invited or tentative, not confirmed.

### Row 08 · Unsupported Competitor Claim

- **Input:** Compare our API rate limits to Competitor Z.
- **Output:** Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- **Verified failure:** Competitor Z supports 1,000 requests per minute versus Ascend’s 500; the negative comparison is unsupported.

### Row 03 · Excess Latency

- **Input:** Summarize the top three complaints from DataViz's G2 reviews.
- **Observed result:** Response time was 4.2 seconds against a 2.0-second standard-request target.
- **Verified failure:** The response exceeded the defined latency target.
