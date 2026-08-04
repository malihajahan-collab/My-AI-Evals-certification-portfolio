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
