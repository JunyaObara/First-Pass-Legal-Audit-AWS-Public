# Implementation Review Guide

## Public Repository Boundary

This public portfolio does not include the full application source code. It is a presentation layer with architecture diagrams, public-safe summaries, evaluation context, and governance documentation.

The implementation areas below summarize the source implementation structure. They are included to explain the engineering scope behind the public portfolio, not to imply that the full source code is published here.

## Recommended Review Path

Start with the public narrative, then use this guide as an implementation architecture summary. The goal is to connect architecture judgment to concrete source areas without implying that the public repository contains the full source code.

| Source implementation area | Implementation responsibility summarized | Capability demonstrated | What not to overclaim |
| --- | --- | --- | --- |
| `README.md` | System purpose, architecture, contracts, run modes, and guardrails. | Source-of-truth documentation discipline. | Do not treat documentation as live deployment proof. |
| Source repository overview materials | Short project narrative and evidence package framing. | Ability to explain the architecture to technical reviewers. | Do not claim every evidence item is published in this public repository. |
| `app_reviewdemo_v94.py` | CDK entry point, deploy profiles, default email, retained KB manifest, model settings, and source hash context. | Cloud-native deployment composition. | Do not claim the script deploys during a public portfolio review. |
| `infra/config.py` | PlatformContext, deployment defaults, Bedrock, KB, cache, approval, and validation controls. | Typed infrastructure configuration discipline. | Do not claim all context values are production final. |
| `infra/stacks/core_stack.py` | S3, EventBridge, Step Functions, Lambda, DynamoDB, SNS, API Gateway, KMS, CloudWatch, and optional CloudTrail. | AWS event-driven GenAI workflow design. | Do not claim least-privilege is complete. |
| `infra/stacks/kb_optional_stack.py` | Bedrock KB, AOSS, separate statute/case-law resources, embedding model, and development standby posture. | Managed RAG infrastructure. | Do not claim case-law is always enabled. |
| `infra/stacks/prompt_cache_stack.py` | KMS-backed versioned prompt cache bucket. | Application-level exact cache foundation. | Do not claim semantic cache. |
| `runtime/privacy_audit/models.py` | Structured dataclasses for hits, issues, recommendations, law results, and audit envelope. | Explicit data contracts. | Do not claim schema completeness for every production integration. |
| `runtime/privacy_audit/use_cases/` | Stage-specific workflow logic for audit, validation, approval, retrieval, and finalization. | Lambda-stage separation and workflow ownership. | Do not claim all modules are small; some finalization logic is intentionally complex. |
| `runtime/privacy_audit/bedrock/kb.py` | Retrieval config, law filters, reranking controls, multi-query fusion, and local fallback. | Bedrock KB retrieval and reproducible retrieval paths. | Do not claim every run uses live KB retrieval. |
| `runtime/privacy_audit/bedrock/llm.py` | Bedrock Runtime wrapper, exact cache, token estimates, cost guardrails, and structured output parsing. | Cost-aware LLM invocation and observability. | Do not expose prompt bodies or transcripts. |
| `runtime/privacy_audit/analysis/` | Query planning, recommendation logic, verdict/routing helpers, evidence classes, and adjudication modules. | Model-assisted plus deterministic AI workflow design. | Do not claim the LLM alone decides legal outcomes. |
| `runtime/data/checklists*/` | Law-specific checklist contracts and item order. | Policy/config-driven issue spotting. | Do not claim exhaustive legal coverage. |
| `runtime/data/routing/` | Recommendation-to-route and owner maps. | Transparent escalation behavior. | Do not invent public outcome labels. |
| `runtime/data/routing_policy/` | Evidence classes and deterministic routing policies. | Law-specific routing governance. | Do not claim policy is legally final. |
| `configs/evaluation/` | Baseline metrics and release gate policy. | LLMOps quality gate. | Do not use held-out row content for tuning. |
| `configs/release/` | Approved manifest example and schema. | Release lineage and rollback reference. | Do not claim automated AWS rollback. |
| `scripts/evaluate_release_gate.py` | Metrics-only release gate implementation. | Protected release decision artifact. | Do not claim it runs live validation. |
| `scripts/validate_approved_manifest.py` | Manifest safety and lineage validation. | Release governance checks. | Do not include sensitive active links or secret-like values. |
| `scripts/check_security_posture.py` | Warning-only posture scanner. | Security debt visibility. | Do not call it a production scanner. |
| `.github/workflows/` | CI contract, release gate, manifest, and security posture smoke checks. | Local/CI governance without AWS calls. | Do not claim fixture CI proves live AWS health. |
| `tests/` | Contract, release gate, manifest, security, Bedrock cache, retrieval, approval, and validation tests. | Regression discipline. | Do not claim every production path is fully tested. |

## Suggested Technical Review Sequence

1. Start from the public architecture overview and supporting docs.
2. The core stack resource declarations show how the AWS workflow is composed.
3. The audit state machine maps into runtime use cases.
4. RAG behavior is concentrated in `bedrock/kb.py`, `bedrock/llm.py`, and `analysis/`.
5. Evaluation configs and release scripts show how quality gates are modeled.
6. Security posture docs, posture checks, and the production hardening backlog show the current boundary.

## What This Page Is Not

This page is not a claim that the public repository contains the full source implementation. It summarizes implementation structure and architecture decisions that can be discussed when appropriate access to source artifacts is available.
