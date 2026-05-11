# Evaluation And LLMOps

## Governance Position

The PoC treats evaluation as a release decision, not a slide at the end of a demo. Candidate changes are judged through scorecards, defined validation conditions, baseline metrics, release gates, and traceable release records.

Final evaluation data is kept separate from day-to-day tuning. This keeps quality claims measurable without turning the final test set into an optimization target.

## Reader-Friendly Terms

| Term | Plain-English meaning |
| --- | --- |
| Defined validation conditions | The documented settings used for a measurement run, such as sample count, retrieval mode, and scorer. |
| Final evaluation data | Data reserved for final confirmation rather than iterative tuning. |
| Release gate | A rule-based check that decides whether measured metrics are strong enough for a release claim. |
| Release record | A traceable record of what code, model/retrieval settings, metrics, and approval evidence were associated with a candidate release. |

## Validation Ladder

| Level | When to use it | What it proves |
| --- | --- | --- |
| Replay and artifact comparison | First check after a small change | Whether deterministic behavior or cached artifacts reproduce expected stage output. |
| Targeted slice | When a known failure family is being investigated | Whether a focused fix addresses a specific cluster without broad cost. |
| Random slice | When targeted results look promising | Whether the change generalizes beyond the target cluster. |
| Full validation | Before release judgment | Whether broad validation metrics and artifacts remain healthy. |
| Held-out confirmation | Final gate only | Whether the release option meets the protected KPI without tuning on row content. |

## Baseline Validation Conditions

The inspected `configs/evaluation/heldout_baseline_metrics.json` records:

These are internal run-condition identifiers included for traceability. For non-specialist readers, the key point is that validation data, held-out confirmation, run settings, and scorer definitions are recorded separately so metrics can be compared honestly.

| Metric | Human-readable result | Machine-readable reference |
| --- | --- | --- |
| Held-out sample count | `42` samples | `sample_count = 42` |
| Outcome match | `80.95%` (`34/42`) | `observed_law_authoritative_quality.target_law_outcome_accuracy = 0.8095238095238095` |
| Review-route match | `78.57%` (`33/42`) | `observed_law_authoritative_quality.target_law_routing_accuracy = 0.7857142857142857` |
| Grounding F1@20 | `82.58%` | `grounding_quality.target_law_grounding_f1_at_20 = 0.8258229728673079` |

## Metrics-Only Release Gate

`configs/evaluation/release_gate_policy.json` defines a metrics-only gate named `heldout_baseline_equivalence`. `scripts/evaluate_release_gate.py` reads scorecard, summary, or metrics JSON; checks required validation fields; compares release metrics to thresholds; blocks unsafe evidence references; and emits a machine-readable report.

This design protects final evaluation data because the gate compares metrics and validation settings rather than row-level content.

## Release Record Relationship

The approved manifest is the repository's release-record format. It captures source repository, runtime contract, retrieval contract, evaluation contract, gate report, approval evidence references, rollback reference, and data-safety flags. The validator is standard-library-only and enforces the safety-critical subset.

The important distinction is simple: the release gate decides whether a scorecard passes, and the release record documents what was approved and what can be restored.

## CI Checks

The inspected GitHub Actions workflow runs:

| Check | Purpose |
| --- | --- |
| Contract test slice | Validates law result, recommendations, validation KB lifecycle, official benchmark contract, and toolchain preflight. |
| Release gate governance smoke | Runs the release gate on a passing fixture and validates the example manifest. |
| Manifest tests | Checks schema alignment, forbidden sensitive fields, baseline enforcement, and safety flags. |
| Security posture warning smoke | Runs the static posture checker and its tests without AWS calls. |

## What The Current Metrics Mean

The baseline metrics show a concrete recognition target under defined validation conditions and scorer. They support the claim that the PoC has a measurable quality gate and a protected final-evaluation posture.

## What They Do Not Mean

They do not prove guaranteed legal correctness, production legal advice, live AWS health at the moment of review, or production-ready operations. Fixture-based CI does not prove deployed Bedrock, KB, SNS, or Step Functions health. Those claims would require live evidence collected under an approved run.

## Technical Review Mapping

For FM evaluation, MLOps, and LLMOps review, this PoC demonstrates:

| Technical review expectation | Evidence in the PoC |
| --- | --- |
| Clear evaluation conditions | Baseline metrics config and release gate policy. |
| Protected final evaluation | Final evaluation data separation and metrics-only comparison. |
| Traceable release records | Approved manifest schema and validator. |
| Cost-aware iteration | Cache-first playbook, replay preference, and low-KMS scratch lane. |
| Responsible AI governance | Human-in-the-Loop and no-autonomous-legal-advice boundary. |

## Technical Traceability Appendix

The following run-condition identifiers are retained for technical reviewers who want to verify the baseline run contract. They are intentionally placed after the reader-friendly evaluation summary because they are traceability details, not the primary public-facing message.

| Run-condition field | Recorded value |
| --- | --- |
| Baseline run id | `validation-live-20260501t003631z` |
| Runtime shadow profile | `fo6_exact_parity` |
| Inference mode | `SOURCE_REFRESH_LIVE` |
| Validation law execution mode | `SCORING_LAW_ONLY` |
| Case-law retrieval mode | `DISABLED` |
| Validation KB build status | `REUSED_EXPLICIT_MANIFEST_VERIFIED` |
| Benchmark truth status | `UNPOPULATED_PLACEHOLDER` |
