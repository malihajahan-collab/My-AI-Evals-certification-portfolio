# Lab 1 · Coverage Matrix · Ascend IQ

**Product:** Ascend IQ Copilot (External)

## Coverage row

| Product | Hallucination | Bias | Latency | Toxicity | Drift Monitoring |
|---|:---:|:---:|:---:|:---:|:---:|
| Ascend IQ Copilot (External) | ⚠️ | ❌ | ✅ | ❌ | ❌ |

## Coverage justification

- **Hallucination · ⚠️ Partial:** Pricing has a deterministic P0 control, but broader hallucination coverage depends on a semantic judge currently failing calibration at **Cohen’s κ = −0.286**.
- **Bias · ❌ Gap:** Fairness is named as a strategic trust metric, but the repository has no operational bias dataset, evaluator, threshold, or measured result.
- **Latency · ✅ Covered:** Module 4 defines workload-specific p95 thresholds, at least 100 production-equivalent requests per workload class, a Staging replay method, and explicit rollout stop conditions.
- **Toxicity · ❌ Gap:** No dedicated toxicity dataset or evaluator exists. Curated professional inputs may reduce likelihood, but they do not constitute measured coverage.
- **Drift Monitoring · ❌ Gap:** Change-time regression gates are defined, but no ongoing production drift pipeline, sampling cadence, alerting, or response process is operationally documented.

## Method and ground truth

### Hallucination · Partial coverage

- **Method:** Run a hybrid evaluation. First, extract pricing claims and deterministically compare each price, currency, discount, seat minimum, and contract term with the versioned approved pricing source. Then use a different-model-family LLM-as-Judge on the broader regression set to classify claims as supported, contradicted, or unsupported.
- **Ground truth:** The versioned approved pricing source is authoritative for pricing fixtures. For broader factual claims, the original source document and human-verified claim labels are authoritative; a generated reference summary is not treated as ground truth.
- **Pass criteria:** 100% of pricing claims must be supported, with zero critical unsupported or contradicted claims. The semantic judge cannot become an operational control until calibration reaches **Cohen’s κ ≥ 0.60**.

### Latency · Covered

- **Method:** Run timed end-to-end replay at production-equivalent concurrency, including retrieval and model generation. Test at least 100 requests separately for standard and multi-document workloads. Count timeouts as failures.
- **Ground truth:** Compare the measured results with the approved Module 4 service thresholds and the versioned production baseline.
- **Pass criteria:** Standard requests require **p95 ≤ 2.0 seconds**; multi-document summaries require **p95 ≤ 3.5 seconds**; neither workload may exceed its approved regression tolerance.

## Strategic acceptance

### Accepted gap · Toxicity

Dedicated toxicity-evaluation coverage is temporarily accepted because Ascend IQ summarizes curated professional sources through a constrained workflow without open-ended prompting. This lowers expected incidence relative to hallucination and drift, which threaten every customer-facing answer.

The risk is not zero. Compensating controls require approved-source ingestion, a lightweight severe-toxicity output filter, human review for flagged outputs, and monthly production sampling.

**Kill criteria:** End this acceptance immediately if any severe toxic, discriminatory, threatening, or defamatory output reaches a customer; open-ended prompting is introduced; uncurated source types are allowed; or a model or prompt change materially expands generation behavior.

**Owner:** Group PM with Responsible AI review.  
**Expiry:** **November 4, 2026**.

## Critical mitigation

### Critical gap · Drift Monitoring

Silent provider, prompt, retrieval, or orchestration changes can degrade factuality, tool selection, latency, tone, and formatting simultaneously across external Enterprise outputs. This cross-cutting blast radius makes Drift Monitoring the highest-priority unaccepted gap.

- **Owner:** Engineering Lead, accountable to the Group PM.
- **Deadline:** **September 30, 2026**.
- **Eval method:** Run claim-level factuality, critical-fact, tool-selection, formatting, tone, and latency regression checks. Critical failures trigger an alert, automatic rollout pause, and rollback.
- **Gold dataset:** Maintain a versioned **500-case** suite covering major use cases, high-risk facts, edge cases, historical failures, and representative production slices.
- **Cadence:** Run before every model, prompt, retrieval, or pipeline change; sample production outputs daily; review trends weekly; refresh the dataset quarterly.

Bias remains a documented gap for the next planning cycle. It is not represented as covered or prioritized above the cross-cutting Drift Monitoring risk.
