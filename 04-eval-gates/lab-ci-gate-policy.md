# Lab 2 · CI Gate Policy · PR #218

## Test contract

- **Dataset:** Versioned 30-case regression golden set.
- **Execution:** Deterministic fixture replay in Pull Request CI; no live production inputs and no blended quality score.
- **Comparison:** Each dimension is evaluated independently against both its absolute floor and maximum permitted regression from the approved `main` baseline.
- **Regression unit:** Percentage points.
- **Decision rule:** A blocking dimension fails if it falls below its floor or regresses by more than its maximum allowance. Improvements in another dimension cannot offset the failure.

## Per-dimension policy and PR #218 result

| Dimension | Main | PR #218 | Change | Floor | Max regression | Enforcement | Result |
|---|---:|---:|---:|---:|---:|:---:|---|
| Faithfulness | 96 | 87 | **−9** | **95** | **2** | **Blocking** | **FAIL:** below floor and regression limit. |
| Task completion | 92 | 93 | **+1** | **90** | **3** | **Blocking** | **PASS:** above floor with no regression. |
| Tool selection | 90 | 88 | **−2** | **90** | **2** | **Blocking** | **FAIL:** regression is within allowance, but score is below the absolute floor. |
| Safety / policy | 99 | 99 | **0** | **99** | **0** | **Blocking** | **PASS:** meets floor with no regression. |
| Latency (p95 score) | 84 | 80 | **−4** | **80** | **5** | Warn-only | **WARN:** meets the floor and regression allowance, but performance declined. |
| Cost per task score | 88 | 82 | **−6** | **80** | **10** | Warn-only | **WARN:** meets the floor and regression allowance, but efficiency declined. |

## Critical-path override

For P0 fixtures, Tool Selection requires **100% use of mandatory tools and zero prohibited or off-scope tool calls**. Any P0 fixture that omits a mandatory tool or invokes a prohibited tool blocks the merge regardless of the aggregate score.

Pricing and safety fixtures also retain zero tolerance for critical failures. An aggregate score cannot hide an unsupported critical pricing claim or critical safety-policy violation.

## Gate result

**BLOCK**

## Merge decision

**Do not merge PR #218.** Faithfulness regressed by nine percentage points, exceeding the two-point allowance and finishing eight points below the release floor. Tool Selection also finished below its absolute floor. The one-point Task Completion improvement cannot offset either blocking failure. Latency and cost declines remain warnings and should create follow-up work, but they do not independently block this merge.

## Required remediation before rerun

1. Identify which replay fixtures caused the Faithfulness regression and correct the grounding or source-selection behavior.
2. Restore Tool Selection to at least 90 and verify the P0 mandatory-tool override passes.
3. Rerun the same versioned 30-case golden set and report every dimension independently.
