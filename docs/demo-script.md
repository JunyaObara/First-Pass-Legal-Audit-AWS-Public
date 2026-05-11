# Portfolio Discussion Guide

## Purpose

This page provides a public guide for reviewing the portfolio. It summarizes the discussion topics, review boundaries, and technical areas that help readers understand the architecture without requiring live AWS access or private source code.

The portfolio can be discussed without live AWS access. The public site focuses on architecture diagrams, design rationale, evaluation summaries, Responsible AI boundaries, and production hardening considerations.

## Suggested 8-Minute Discussion Flow

| Time | Topic | Discussion focus |
| --- | --- | --- |
| 0:00-0:45 | Positioning | The project is a first-pass compliance triage PoC, not autonomous legal advice. The architecture demonstrates governed GenAI on AWS. |
| 0:45-1:45 | Architecture | The public architecture diagram shows S3 ingestion, EventBridge, Step Functions, Lambda stages, Bedrock Knowledge Bases, Bedrock Runtime, DynamoDB/S3 state, SNS/API Gateway approval integration, KMS, CloudWatch, and optional CloudTrail. |
| 1:45-3:00 | AI/RAG pipeline | The RAG design uses statute-first retrieval, checklist extraction, query planning, basis selection, deterministic adjudication, recommendation generation, and citation projection. |
| 3:00-4:15 | Human-in-the-Loop governance | Engineering review is required, Legal review is conditional, Business approval is required, and stakeholder notification is modeled. |
| 4:15-5:30 | Evaluation and LLMOps | The PoC uses held-out baseline metrics, validation stages, release gates, and traceable release records to avoid relying on demo-only impressions. |
| 5:30-6:45 | Security and production boundaries | The public discussion should cover encryption posture, managed signing posture, approval-state protection, observability, and the production hardening backlog without claiming production readiness. |
| 6:45-8:00 | Enterprise GenAI extension | The same governed workflow pattern can be extended to Amazon Q Business-style enterprise workflows, while the current PoC does not implement Amazon Q. |

## Deeper Technical Discussion Topics

For a deeper technical review, the most useful topics are:

1. The customer problem and why global software compliance review benefits from earlier, evidence-grounded triage.
2. The AWS service selection and why event-driven orchestration, managed retrieval, serverless stages, stateful approvals, and observability fit the workflow.
3. The AI/RAG design, including statute-first grounding, law-scoped retrieval, evidence sufficiency, and deterministic routing.
4. The evaluation approach, including the held-out baseline, validation ladder, metrics-only release gate, and manifest-style release records.
5. The security and Responsible AI boundary, including what the public portfolio does and does not claim.
6. The productionization roadmap: identity, access control, private access, endpoint hardening, monitoring, cost controls, runbooks, and per-domain evaluation ownership.

## Implementation Areas Behind The Public Portfolio

The public repository does not contain the full application source. The following areas summarize the implementation scope behind the portfolio and explain what each area contributes to the architecture:

1. `app_reviewdemo_v94.py` for CDK entry point, deploy profiles, retained KB manifest, model settings, and source context.
2. `infra/stacks/core_stack.py` for S3, EventBridge, Step Functions, Lambda, DynamoDB, SNS, API Gateway, KMS, CloudWatch, and optional CloudTrail.
3. `runtime/privacy_audit/use_cases/` for stage-specific workflow boundaries.
4. `runtime/privacy_audit/bedrock/kb.py` and `runtime/privacy_audit/bedrock/llm.py` for retrieval, Bedrock integration, caching, and cost-aware model invocation.
5. `runtime/privacy_audit/analysis/` and routing configuration for deterministic adjudication, evidence classes, and weak-evidence guardrails.
6. `configs/evaluation/`, `configs/release/`, and release scripts for evaluation governance.
7. CI workflows and tests for contract, release gate, manifest, security posture, retrieval, approval, and validation checks.

## No-Live-AWS Discussion Path

If live AWS access is unavailable or inappropriate, the portfolio can still be reviewed using public artifacts:

1. Start from the landing page and architecture diagram.
2. Review the Architecture Deep Dive and AI/RAG Design pages.
3. Review the Evaluation & LLMOps page for metric interpretation and release governance.
4. Review the Security & Responsible AI page for the PoC boundary and production hardening backlog.
5. Use the Implementation Review Guide to understand which source areas sit behind the public architecture summary.
6. State clearly that no live AWS deployment, live Bedrock inference, or production health check is being demonstrated in this public review.

## Public Review Boundaries

The public portfolio intentionally focuses on diagrams, architecture rationale, evaluation summaries, and governance boundaries. It does not publish raw prompts, prompt cache payloads, private runtime data, final evaluation rows, active approval links, credentials, signed query parameters, or unpublished customer data.

The correct claim is that the PoC demonstrates a governed AWS GenAI workflow pattern for first-pass compliance triage. It does not claim autonomous legal advice, guaranteed legal correctness, production readiness, live AWS health, or that Amazon Q is part of the current implementation.
