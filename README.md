# First-Pass Legal Audit AWS Public Portfolio

## Overview

This is a public-facing technical portfolio site for the AWS CloudNative GenAI Compliance Review PoC.

The project demonstrates how a first-pass compliance triage workflow for globally delivered software can be built on AWS using event-driven orchestration, statute-grounded RAG, Human-in-the-Loop approval, security-aware boundaries, and LLMOps-style release governance.

The legal domain is the sample high-risk workflow. The broader pattern is applicable to companies that ship software products, platforms, apps, APIs, AI features, analytics features, media flows, user-profile features, or cross-border data flows across markets.

The system is a first-pass compliance triage PoC, not autonomous legal advice. Final judgment remains Human-in-the-Loop.

## What This Repository Contains

This repository contains a static public portfolio site:

- `index.html` as the public site entry point.
- `assets/` with static CSS, Mermaid diagram sources, and public portfolio metadata.
- `docs/` with public HTML and Markdown portfolio documents.
- `.nojekyll` so GitHub Pages can serve the static files without Jekyll processing.

## Public Safety Boundary

This repository is a public presentation layer. It intentionally contains diagrams, summaries, and public-facing documents only.

It does not contain the private implementation source, sensitive runtime data, credentials, active approval links, raw prompts, prompt-cache contents, or final evaluation rows.

## Public Site Entry Point

Entry point: `index.html`

If GitHub Pages is enabled, this repository can be served as a static portfolio site.

## Key Portfolio Documents

| Document | Purpose |
| --- | --- |
| `docs/architecture-deep-dive.html` | AWS architecture deep dive for the CloudNative GenAI compliance review workflow. |
| `docs/ai-rag-design.html` | Statute-first RAG, evidence sufficiency, deterministic adjudication, and failure-mode mitigation. |
| `docs/evaluation-and-llmops.html` | How the PoC measures quality, protects final evaluation data, and uses release gates. |
| `docs/security-and-responsible-ai.html` | Security posture, Human-in-the-Loop boundaries, and production hardening considerations. |
| `docs/amazon-q-relevance.html` | How the PoC pattern can extend to Amazon Q Business-style enterprise workflows without claiming Amazon Q implementation. |
| `docs/customer-adoption-roadmap.html` | Customer-backward adoption path from discovery to pilot, validation, production hardening, and scale. |
| `docs/aws-well-architected-mapping.html` | Mapping of the PoC to operational excellence, security, reliability, performance efficiency, cost, and sustainability. |
| `docs/faq-and-challenges.html` | Answers to common architecture, RAG, security, cost, and adoption questions. |

## Relevant Skill Areas

- Cloud-native GenAI architecture on AWS.
- Amazon Bedrock, RAG, and evaluation-governed AI workflows.
- Human-in-the-Loop approval and responsible AI boundaries.
- Secure enterprise workflow design and production-readiness planning.

## Responsible AI / Legal Boundary

This is not autonomous legal advice.

This is a first-pass compliance triage PoC. It supports issue spotting, evidence grounding, routing, and review preparation. Final legal and business judgment remains Human-in-the-Loop.

It demonstrates an evaluation-governed AWS GenAI architecture, not guaranteed legal correctness. It is a security-aware PoC and would require additional identity, access, monitoring, networking, and operations controls before enterprise production use.

## Source Repository

Source implementation repository: `JunyaObara/First-Pass-Legal-Audit-AWS`

The PoC does not implement Amazon Q. It demonstrates a governed AWS GenAI workflow pattern that can be extended to Amazon Q Business-style enterprise workflows.

## Notes

This repository is intentionally narrow: it is the public portfolio presentation layer only. Start with `index.html`, then open the architecture, AI/RAG design, evaluation governance, security, customer adoption roadmap, Well-Architected mapping, and Amazon Q Business / Enterprise GenAI relevance documents.
