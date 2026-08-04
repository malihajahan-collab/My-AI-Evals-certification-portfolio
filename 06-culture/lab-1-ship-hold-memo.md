# Ascend IQ · Ship/Hold Decision Memo

**To:** CPO and Executive Leadership  
**From:** Group PM, Ascend IQ  
**Subject:** External launch decision for Ascend IQ

## Decision

**HOLD**

## The Answer

**HOLD the external launch of Ascend IQ because the candidate fails the Faithfulness and Tool Selection gates, and the semantic judge intended to detect P0 factual errors is not calibrated for enforcement.** Continue internal remediation and deterministic regression testing, but do not expose the candidate to external Enterprise customers until the blocking gates pass.

## The Arguments

### 1. Customer trust is exposed by a verified P0 failure

Ascend IQ has already produced incorrect Enterprise pricing in a product sold as verified, citation-backed intelligence. External release would expose customers to a known failure capable of influencing high-stakes commercial decisions.

### 2. The current candidate fails its agreed release gates

PR #218 is below the Faithfulness and Tool Selection floors. Shipping this candidate would override the per-dimension policy established before launch and allow gains in unrelated metrics to excuse factual and agent-path regressions.

### 3. The evaluation system cannot yet prove the fix is safe

The semantic judge is below its calibration requirement, and production Drift Monitoring remains an unresolved critical gap. The team currently lacks a trustworthy semantic blocker and continuous evidence that model, prompt, retrieval, or provider changes will not reintroduce critical failures.

## Evidence · Trust Metrics

| Metric | Result | Gate | Status | Source |
|---|---:|---:|:---:|---|
| Critical pricing failures | **1** | **0 allowed** | **FAIL** | M2 `failure-audit.md`; M3 `lab-1-eval-suite.md` |
| Faithfulness | **87**, down from 96 | Floor **95**; maximum regression **2 points** | **FAIL** | M4 `lab-ci-gate-policy.md` |
| Tool Selection | **88**, down from 90 | Floor **90**; maximum regression **2 points** | **FAIL** | M4 `lab-ci-gate-policy.md` |
| Task Completion | **93**, up from 92 | Floor **90** | **PASS** | M4 `lab-ci-gate-policy.md` |
| Safety | **99**, unchanged | Floor **99**; maximum regression **0 points** | **PASS** | M4 `lab-ci-gate-policy.md` |
| Judge calibration | **Cohen’s κ = −0.286** | **κ ≥ 0.60** | **FAIL** | M3 `lab-judge-calibration.md` |
| Coverage gaps | **3 of 5 risks** | At least **2 gaps disclosed** | **PASS for disclosure; launch risk remains** | M5 `lab-1-coverage-matrix.md` |
| Evaluation portfolio spend | **$187,500** | Quarterly cap **$200,000** | **PASS** | M5 `lab-2-budget-crisis.md` |

The decisive result is **Faithfulness at 87 against a 95 floor**. The judge’s **κ = −0.286** further shows that the semantic safety net cannot yet validate a remediation with sufficient reliability.

## Business Risk

**SHIP path:** Releasing now exposes Enterprise customers to a candidate with one confirmed critical pricing failure and failed Faithfulness and Tool Selection gates. Each affected Enterprise account represents **$50K+** in potential contract value, while customers may use the output to inform decisions worth **$1M+**. A repeated failure could trigger a contract dispute, legal review, non-renewal, or broader damage to Ascend Analytics’ verified-intelligence positioning.

**HOLD path:** Holding launch moves the assumed **August 4, 2026** release to at least the **September 30, 2026** Drift Monitoring deadline—a **57-day delay** that defers approximately **$7.8K+ in annual-contract revenue timing per affected Enterprise account** and compresses the customer window for Q4 roadmap planning. Total pipeline exposure is not yet quantified; each launch-dependent account represents at least **$50K** in potential contract value.

The HOLD cost is material but bounded and measurable. The SHIP risk places existing and prospective Enterprise trust at risk while knowingly overriding Hard controls.

## Next Step · Decision Needed

Approve the external-launch hold and remediation plan by **August 7, 2026**. Re-evaluate launch only after:

1. Faithfulness reaches at least **95** without regressing by more than two percentage points.
2. Tool Selection reaches at least **90** and all P0 mandatory-tool fixtures pass.
3. Critical pricing failures are reduced to **zero**.
4. Judge calibration reaches **Cohen’s κ ≥ 0.60** on the revised rubric.
5. The Drift Monitoring control due **September 30, 2026** is operational with alert, rollout-pause, and rollback procedures.

The Group PM owns the release decision; the Engineering Lead owns remediation, gate enforcement, and rollback readiness.

## Reflection

Defining “good enough” forced us to confront that aggregate improvements cannot compensate for a failed P0 dimension. A higher Task Completion score does not make unsupported pricing, degraded Faithfulness, or an unverified agent path acceptable. The launch standard must remain per-risk and evidence-based, even when holding creates schedule and revenue pressure.
