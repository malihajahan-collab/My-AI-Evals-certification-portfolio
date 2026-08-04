# Judge Calibration · Ascend IQ

## Calibration dataset

Twelve grounding traces were independently labeled by a human reviewer and the LLM-as-Judge.

| Trace | Human | Judge | Agreement |
|---:|:---:|:---:|:---:|
| 1 | PASS | PASS | Yes |
| 2 | FAIL | PASS | No |
| 3 | FAIL | PASS | No |
| 4 | PASS | PASS | Yes |
| 5 | PASS | PASS | Yes |
| 6 | PASS | FAIL | No |
| 7 | FAIL | PASS | No |
| 8 | PASS | PASS | Yes |
| 9 | FAIL | PASS | No |
| 10 | PASS | FAIL | No |
| 11 | PASS | PASS | Yes |
| 12 | PASS | PASS | Yes |

## Confusion matrix

Human labels are the ground truth.

|  | Judge PASS | Judge FAIL | Total |
|---|---:|---:|---:|
| Human PASS | 6 | 2 | 8 |
| Human FAIL | 4 | 0 | 4 |
| Total | 10 | 2 | 12 |

## Cohen’s κ

- **Observed agreement:** 6 / 12 = 0.500
- **Expected agreement:** (8/12 × 10/12) + (4/12 × 2/12) = 0.611
- **Cohen’s κ:** (0.500 − 0.611) / (1 − 0.611) = **−0.286**
- **Required threshold:** κ ≥ 0.60
- **Result:** **FAIL**

The judge missed all four human-labeled failures. It is not calibrated well enough to enforce the P0 pricing-integrity gate.

## Diagnosis

The judge appears to reward plausible-looking responses without requiring every material factual claim to be supported by the reference. Fluent wording, partial correctness, or correct secondary details may be compensating for a material unsupported or contradicted claim.

## Approved rubric revision

> Evaluate every material factual claim independently. Mark the entire response **FAIL** if any price, number, date, entity, status, commitment, or conclusion is contradicted by or unsupported by the reference. Plausibility, fluent wording, partial correctness, and correct unrelated details must not compensate for one material unsupported claim.

### One-shot FAIL example

- **Reference:** Enterprise pricing is `$59/user/month`.
- **Response:** Enterprise pricing is `$49/user/month`, with a correct 10-seat minimum.
- **Label:** **FAIL** — the correct seat minimum does not offset the contradicted price.

## Revision plan

Rerun the revised judge on the same 12 traces and recompute the confusion matrix and Cohen’s κ. Do not approve the judge for the P0 gate until κ ≥ 0.60. If the rerun remains below threshold, review disagreement traces, add targeted examples, and repeat calibration on a held-out set before deployment.
