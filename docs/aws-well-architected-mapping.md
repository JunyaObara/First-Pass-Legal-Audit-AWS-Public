# AWS Well-Architected Mapping

## Mapping Summary

This mapping is written for technical review. It identifies current PoC evidence, why each pillar matters, and what must be hardened before production.

| Pillar | Current PoC implementation evidence | Why it matters | Additional hardening before production use | Technical review point |
| --- | --- | --- | --- | --- |
| Operational Excellence | Step Functions workflows, CloudWatch dashboard, alarms, log queries, runbooks, validation playbook, and CI smoke checks. | GenAI systems need observable workflows, repeatable validation, and clear ownership. | Add SLOs, incident runbooks, on-call dashboards, drift detection, and automated release promotion. | The workflow is made inspectable before scale-out concerns are introduced. |
| Security | SSE-KMS source buckets, KMS-backed prompt cache, DynamoDB encryption, Secrets Manager signing secret, public-safe evidence boundaries, and warning-only posture checker. | Compliance artifacts and approval state must be protected even in a PoC. | Least-privilege IAM split, WAF/auth/rate limiting, private access, VPC endpoints, Macie where appropriate, and key policy review. | "Security posture is part of AI governance, not a separate appendix." |
| Reliability | Standard Step Functions, retries/catches, DynamoDB idempotency table, approval expiry handling, validation cleanup paths, and retained KB reuse policy. | Long-running AI workflows fail in many places; failure must be attributable. | Add DLQs where appropriate, chaos tests, alias-based deployment, retry budgets, and recovery runbooks. | "The architecture separates failure handling by workflow stage." |
| Performance Efficiency | Lambda stage isolation, distributed validation Map state, S3 artifact indirection, retrieval top-k controls, exact prompt cache, and optional reranking controls. | AI workflows must manage latency, throughput, and model calls explicitly. | Add load tests, concurrency quotas, queue-based backpressure, and per-stage latency budgets. | "The design controls model and retrieval cost rather than treating them as a black box." |
| Cost Optimization | Cache-first validation policy, exact prompt cache, low-KMS scratch lane, retained KB reuse, and cost guardrails. | Evaluation loops can become expensive without guardrails. | Add cost allocation tags, cost anomaly alerts, per-customer budgets, and automated cost reports. | The validation loop is optimized without weakening the intended production encryption posture. |
| Sustainability | Serverless orchestration, managed retrieval resources, cache reuse, retained KB reuse, and no unnecessary live runs in normal validation. | Efficient resource use supports both cost and sustainability. | Add lifecycle policies, scheduled cleanup, right-sized validation capacity, and usage dashboards. | "Reuse and cache discipline reduce unnecessary compute and rebuilds." |

## Boundaries

This mapping does not claim a completed production Well-Architected review. It shows that the PoC was designed with Well-Architected concerns visible and that production work is intentionally named.
