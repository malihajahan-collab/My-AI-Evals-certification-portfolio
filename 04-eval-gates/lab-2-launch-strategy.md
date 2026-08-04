# Lab 3 · Launch Strategy · Ascend IQ

## 4.0 Release Criteria

The following thresholds must be met by the model candidate before approval for production deployment. Each metric is evaluated independently; performance in one dimension cannot offset failure in another.

| Severity | Metric | Numeric threshold | Dataset | Method |
|---|---|---|---|---|
| **Hard · Blocker** | Pricing factuality | **100%** of pricing claims supported; **0** unsupported or contradicted critical claims | Versioned pricing regression fixtures covering current and historical prices, currencies, discounts, minimum commitments, and contract terms | Deterministic comparison with the approved pricing source in PR. Semantic regression runs in Staging only after the judge reaches **Cohen’s κ ≥ 0.60**. |
| **Soft · Review** | End-to-end latency | Standard requests: **p95 ≤ 2.0 seconds**. Multi-document summaries: **p95 ≤ 3.5 seconds**. Timeouts count as failures. | At least **100 production-equivalent requests per workload class** | Timed replay at approved concurrency, including retrieval and model generation but excluding client-network time. |
| **Advisory · Monitor** | Brand-tone consistency | **<5%** of at least **100 outputs** contain a defined brand-tone violation | Versioned email and summary style fixtures across representative use cases | PR keyword and style checks plus a weekly human sample. Severe abusive or discriminatory output is evaluated separately under the Hard safety policy. |

### Enforcement semantics

- **Hard:** Automatically blocks promotion. No exception can be created by averaging this result with another metric.
- **Soft:** Requires documented Product and Engineering approval, with an owner, expiry date, and rollback condition.
- **Advisory:** Produces a warning and remediation ticket but does not block deployment unless the output is reclassified as a critical safety violation.

## 4.1 CI Gate Policy

Pull Request CI replays a versioned golden set of at least 30 deterministic fixtures. CI does not call a live production model and does not calculate a blended quality score. Each dimension must satisfy its absolute floor and maximum regression allowance independently.

| Dimension | Floor | Max regression | Enforcement |
|---|---:|---:|:---:|
| Faithfulness | **95** | **2 percentage points** | Blocking |
| Task completion | **90** | **3 percentage points** | Blocking |
| Tool selection | **90** | **2 percentage points** | Blocking |
| Safety / policy | **99** | **0 percentage points** | Blocking |
| Latency p95 score | **80** | **5 percentage points** | Warn-only |
| Cost per task score | **80** | **10 percentage points** | Warn-only |

A blocking dimension fails when it falls below its floor or regresses by more than its allowance. P0 Tool Selection fixtures additionally require **100% use of mandatory tools and zero prohibited or off-scope tool calls**. Pricing and critical-safety fixtures retain zero-failure overrides.

For PR #218, the gate result is **BLOCK**: Faithfulness fell from 96 to 87, a nine-point regression, and Tool Selection fell from 90 to 88, below its absolute floor. Task Completion improved and Safety remained stable, but those results cannot offset the blocking regressions. Latency and Cost generate warnings.

## 4.2 Mitigation Plan · Soft Latency Gate

**Selected lever: Staged rollout.**

If standard-request p95 exceeds 2.0 seconds or multi-document p95 exceeds 3.5 seconds, but remains below the blocking ceiling, release to **5% of eligible beta traffic**. Automatically stop expansion if:

- Standard-request p95 exceeds **2.2 seconds**.
- Multi-document p95 exceeds **3.85 seconds**.
- Either workload regresses by more than **10%** against its approved baseline.
- The timeout rate exceeds its approved operating limit.

Engineering will enable retrieval caching, parallel document retrieval, bounded context size, generation-token limits, and asynchronous handling for oversized requests. The rollout may expand only after the affected workload remains below its Soft threshold for at least **24 hours and 1,000 eligible requests**.

Staged rollout contains customer exposure while the technical controls reduce latency; it is not treated as a substitute for remediation.
