# Lab 2 · Budget Crisis · Ascend IQ

**Quarterly budget cap:** $200,000  
**Portfolio spend:** $187,500  
**Budget remaining:** $12,500  
**Level 3 spend:** $175,000  
**Level 3 slots used:** 3 of 3

## Portfolio decision grid

| Failure mode | Trust metric | Risk | Coverage level | Quarterly cost |
|---|---|:---:|:---:|---:|
| Data Fabrication | Hallucination | P0 | **L3** | **$85,000** |
| Context Specificity | UX Trust | P1 | **L2** | **$7,000** |
| Source Attribution Failure | Robustness | P1 | **L3** | **$65,000** |
| Data Bias | Fairness | P2 | **L2** | **$5,500** |
| Cost Overruns | Latency / Efficiency | P3 | **L3** | **$25,000** |
| **Total** |  |  |  | **$187,500** |

## Portfolio rationale

The portfolio funds the P0 Data Fabrication risk and the most dangerous P1 Source Attribution risk at Level 3. Unsupported citations can appear authoritative and survive superficial customer review, creating contractual, compliance, and trust exposure. Context Specificity is downgraded because generic responses are normally visible and recoverable. Cost Overruns receives the third Level 3 slot because continuous telemetry and automated controls fit within the remaining budget at comparatively low cost.

## Fallback methods

### L2 · Context Specificity · UX Trust · P1

- **Automated check:** Verify that responses address required prompt dimensions, including customer, industry, geography, timeframe, requested metrics, and retrieved entities. Flag generic phrases and missing required dimensions.
- **Replay:** Run versioned client-specific fixtures before every prompt, retrieval, or model change.
- **Human audit:** Review **50–100 risk-stratified production outputs weekly** for relevance, specificity, completeness, and actionable detail.
- **Pass criteria:** At least **95%** of audited outputs score **4/5 or higher**, with no missing critical customer context.
- **Escalation:** Move to L3 if the pass rate falls below 95% for two consecutive audits or a context failure materially affects a customer decision.

**Incident-review defense:** Context-specificity failures are normally visible and recoverable UX defects. Deterministic checks catch missing required context cheaply, while weekly human review evaluates whether the context is used meaningfully. High-impact recommendations are excluded from this downgrade and remain subject to stronger factuality controls.

### L2 · Data Bias · Fairness · P2

- **Automated check:** Measure retrieved-source distribution across relevant regions, industries, company sizes, languages, and defined cohorts.
- **Counterfactual replay:** Change only one relevant demographic or geographic attribute and compare factuality, completeness, tone, certainty, and recommendations.
- **Human audit:** Review **50–100 risk-stratified outputs weekly** for systematic omission, unequal emphasis, stereotyping, and unsupported demographic inference.
- **Pass criteria:** Zero severe stereotyping or unsupported protected-characteristic inference; at least **99% counterfactual consistency**; no cohort more than **five percentage points** below the overall quality baseline.
- **Escalation:** Move to L3 after any severe fairness incident, expansion into consequential decisions about individuals, or two consecutive audits showing systematic disparity.

**Incident-review defense:** Ascend IQ summarizes bounded Enterprise information rather than making employment, credit, healthcare, or other consequential decisions about individuals. Upstream representation checks address retrieval skew cheaply, while counterfactual fixtures and human audits cover semantic disparities that metadata checks cannot detect.
