# Security And Responsible AI

## Correct Security Positioning

This document explains how this security-aware PoC treats security as part of the workflow design: protecting review inputs, evidence, approval state, and evaluation artifacts while keeping final decisions accountable to humans.

The PoC is not presented as production-ready security. A production version would require a production hardening backlog covering identity, access, network, monitoring, secret rotation, key policies, and operational controls.

## Current Security-Aware Controls

| Area | Source-backed posture |
| --- | --- |
| S3 encryption | Core buckets use SSE-KMS with bucket keys, block public access, versioning, SSL enforcement, and retain policies. |
| Prompt cache | The prompt cache bucket uses SSE-KMS, bucket keys, versioning, SSL enforcement, and retain policy. |
| Validation scratch | The low-KMS scratch stack intentionally uses SSE-S3, lifecycle expiration, SSL enforcement, and block public access for validation-only high-churn artifacts. |
| DynamoDB | Audit, approval, and idempotency tables use customer-managed encryption, pay-per-request billing, retain policy, and PITR where implemented. |
| Secrets | A managed signing secret is created through Secrets Manager for approval review and callback verification. |
| Approval path | The approval flow includes signed review context, replay-resistant guard data, expiry handling, human confirmation, and task state storage. |
| Observability | CloudWatch dashboards, alarms, log query definitions, X-Ray tracing, and optional CloudTrail are implemented in the core stack. |
| Public artifact boundary | Public materials use diagrams, summaries, metrics, and redacted explanations. They do not publish sensitive runtime data, credentials, active approval links, raw prompts, prompt-cache contents, or final evaluation rows. |

## Responsible AI Boundary

This is not autonomous legal advice. It is a first-pass compliance triage PoC that supports issue spotting, evidence grounding, routing, recommendations, and approval evidence. Final legal and business judgment remains Human-in-the-Loop.

## Evidence Lane Separation

Statute retrieval and case-law retrieval remain separate. Statutory text is primary. Case-law retrieval is secondary, conditional, and intended as Legal-review support. This helps prevent a model response from turning a secondary interpretation artifact into the apparent source of truth.

## IAM Visibility

The repository includes a warning-only static checker for broad permissions and public network-policy indicators. This is useful posture visibility, but it is not a production security scanner. Broad lifecycle permissions remain an enterprise hardening item unless tightly justified by AWS service semantics.

## Enterprise Production Hardening Roadmap

| Area | Additional hardening before production use |
| --- | --- |
| IAM | Split deployment, runtime, validation, and operator roles; scope runtime access to specific buckets, prefixes, tables, topics, and state machines; add permission boundaries and IAM Access Analyzer review. |
| Network | Add WAF, authenticated approval access, rate limiting, private access where appropriate, and VPC endpoints for enterprise network posture. |
| Secrets | Add rotation policy, audit secret access, and narrow secret-read permissions. |
| KMS | Review key policies, separate keys by environment and sensitivity where justified, and alert on unusual KMS errors or cost patterns. |
| S3 data governance | Add lifecycle and retention policies by artifact class; add sensitive-data discovery such as Macie where appropriate. |
| DynamoDB | Review TTL, PITR, backups, and table-level IAM. |
| Monitoring | Add latency, cost, quality, approval SLA, and drift dashboards with operational runbooks. |
| Release operations | Promote only validated manifests through environment-specific deployment controls. |

## Public Review Boundary

The public portfolio uses diagrams, architecture summaries, metrics summaries, and governance explanations. It does not publish private runtime data, final evaluation rows, prompt bodies, model transcripts, active review links, callback payloads, browser cookies, cloud account identifiers, or generated credentials.
