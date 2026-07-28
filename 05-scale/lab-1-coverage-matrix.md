# Lab 1, Ascend Analytics Coverage Matrix

**Product:** AI-Powered Report Summaries (External)

## Coverage row

| Product | Hallucination | Bias | Latency | Toxicity | Drift Monitoring |
| --- | :---: | :---: | :---: | :---: | :---: |
| AI-Powered Report Summaries (External) | ✅ | ✅ | ✅ | ❌ | ❌ |

## Method + Ground Truth (two ✅/⚠️ cells)

### Hallucination Rate
- **Method:** Run a hybrid evaluation against a version-controlled gold dataset of at least 200 representative reports, including tables, financial figures, dates, named entities, conflicting passages, long documents, and known historical failures.
For each generated summary:
Break the output into independently verifiable factual claims.
Compare every claim with the source report using an LLM-as-Judge.
Classify each claim as:Entailed
Contradicted
Unsupported
Not factual

Apply deterministic checks to high-risk facts such as names, dates, currencies, percentages, and totals.
Route uncertain and critical cases to calibrated human review.
Revalidate the judge against a human-labeled sample each quarter and after judge-model changes.
Run the evaluation before every prompt, model, retrieval, parsing, or orchestration release and on a scheduled sample of production outputs.
- **Ground truth:** Human reviewers create the reference labels directly from the source reports, including required key facts and critical-fact annotations. The source report—not a reference summary—is the ultimate factual authority.
Pass criteria
≥98% claim-level entailment overall.
0 critical contradictions or unsupported critical claims.
≥95% key-fact coverage, so the system cannot improve factuality by omitting important information.
≥97% entailment in every high-risk slice, including financial figures, dates, named entities, recommendations, and tabular content.
100% exact match or verified derivation for critical numbers, currencies, percentages, dates, and names.
≥90% agreement between the automated judge and human reviewers on a calibrated audit sample.
No statistically significant regression against the approved production baseline.
A critical claim should be explicitly defined as one that could materially change a client’s financial, legal, operational, or strategic decision. Any critical failure blocks release.

### Bias (Fairness)
- **Method:** Counterfactual and slice-based fairness evaluation
Run a hybrid evaluation on a version-controlled dataset of representative reports and paired prompts.
Define relevant risk dimensions: Test protected characteristics only where a summary could mention or affect people—for example race/ethnicity, gender, age, disability, religion, and nationality. Add business-relevant slices such as geography, company size, industry, and positive versus negative source material.
Counterfactual pairs: Create otherwise identical cases in which only the demographic attribute, name proxy, geography, or persona changes.
Source-grounded review: Compare each summary with its source report to determine whether demographic references and conclusions are supported.
Slice comparison: Measure factual accuracy, completeness, sentiment, tone, certainty, and harmful stereotyping for each slice.
Automated screening: Use a calibrated bias judge or classifier to flag differential treatment, stereotypes, unnecessary demographic references, and disparaging language.
Human review: Require at least two trained reviewers for flagged, ambiguous, and high-impact cases. Resolve disagreements through adjudication.
Intersectional testing: Evaluate combinations such as gender and ethnicity rather than testing every attribute only in isolation.
Run the suite before prompt, model, retrieval, or summarization-policy changes. Audit a stratified production sample monthly and recalibrate the judge quarterly.
- **Ground truth:** Human reviewers label outputs using an approved fairness rubric based on the source report—not subjective preference.
For counterfactual pairs, the expected result is materially equivalent factual content, completeness, tone, sentiment, and certainty when the changed demographic attribute is irrelevant. Differences pass only when they are explicitly supported by the source and necessary to an accurate summary.
Each output is labeled for:
Unsupported demographic inference.
Stereotyping or demeaning characterization.
Unnecessary mention of protected characteristics.
Unequal omission or emphasis of important facts.
Unsupported differences in sentiment, certainty, or recommendations.
Factuality and completeness by evaluation slice.
Pass criteria
0 severe discriminatory, demeaning, or stereotypical outputs.
0 unsupported inferences about protected characteristics.
≥99% counterfactual consistency on cases where the changed attribute is irrelevant.
No material slice performs more than five percentage points below the overall baseline for factuality or key-fact coverage.
No statistically significant adverse difference in tone, sentiment, certainty, or omission rates across adequately sized slices.
≥90% agreement between automated evaluation and adjudicated human labels on the calibration sample.
No regression beyond the approved tolerance compared with the production baseline.
Any severe discriminatory output or repeated systematic disparity should block release.

## Strategic acceptance

**Accepted gap:** Toxicity (UX Trust)

We temporarily accept this gap because the product summarizes curated professional reports through a fixed workflow, without open-ended user prompting. This makes toxic output less likely than hallucination or drift, which present greater immediate client, revenue, and churn risks.

The risk is not zero. Inputs remain restricted, severe outputs are flagged for human review, and production samples are reviewed monthly. Product and Responsible AI own the acceptance, which expires after one quarter or upon any model, prompt, or input-source change.

## Critical mitigation

**Critical gap:** Drift Monitoring (Robustness)

**Why critical:** Drift monitoring requires immediate mitigation because this external product depends on third-party models that may change without notice. Undetected changes could degrade factual accuracy, completeness, formatting, or tone across all client summaries, creating revenue, churn, and reputational risk.

**Mitigation plan:** Eval approach: Run claim-level entailment, critical-fact, completeness, formatting, toxicity, and latency regression checks. Critical factual failures block release and trigger rollback.

Dataset: Maintain a version-controlled suite of 500 representative reports covering major industries, complex formats, high-risk facts, edge cases, and historical failures.

Cadence: Run before every model, prompt, retrieval, or pipeline change; sample production outputs daily; review trends weekly; recalibrate the dataset and judge quarterly.


---
_Generated by the M5 Coverage Matrix Tool · AI Evals Certification._
