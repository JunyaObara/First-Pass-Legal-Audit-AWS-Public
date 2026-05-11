# FAQ And Challenges

## Common Technical Questions

| Challenge | Answer |
| --- | --- |
| Is this really production-ready? | No. It is a security-aware PoC and architecture demonstration. Production readiness would require hardened IAM, identity, network controls, monitoring, CI/CD promotion, and operational runbooks. |
| Is this legal advice? | No. It is first-pass compliance triage. It helps spot issues, ground evidence, route decisions, and prepare recommendations. Final judgment remains Human-in-the-Loop. |
| Why statute-first RAG? | Statutes and regulations are the primary authority for this workflow. Using statute-first retrieval improves provenance and makes the system easier to explain to legal and compliance stakeholders. |
| Why separate case law? | Case law can help Legal review, but it should not blur into the primary statute lane. Separation keeps provenance clear and prevents the model from over-weighting secondary evidence. |
| Why deterministic adjudication? | Deterministic adjudication makes final outcome and routing testable. The LLM can assist, but the system should not rely on a free-form answer for workflow decisions. |
| Why not just ask the LLM? | A single prompt cannot provide durable governance, provenance, release gates, approval workflow, or repeatable evaluation. Enterprise GenAI needs explicit control points. |
| How do you handle weak evidence? | The guardrail downgrades a would-be clearance to review-needed behavior when evidence quality is weak or mixed. That prevents overconfident clearance. |
| How do you prevent prompt leakage? | Public packages exclude prompt bodies, model messages, cache entries, and full transcripts. Release evidence uses metrics, hashes, summaries, manifests, and redacted references. |
| How do you evaluate RAG? | Separate outcome match, review-route match, grounding F1@20, retrieval provenance, basis sufficiency, and stage-level artifacts. Use replay and validation before final confirmation. |
| What does the baseline prove? | It establishes a concrete KPI under defined validation conditions and scorer. It proves the PoC has measurable release criteria. |
| What does it not prove? | It does not prove guaranteed legal correctness, live AWS health, production security, or autonomous approval safety. |
| How could this pattern extend to Amazon Q Business? | Amazon Q Business could serve as the enterprise assistant/workflow interface on top of governed knowledge, identity, approval, and evaluation patterns. The current repository does not implement Amazon Q. |
| How could this integrate with SAML, Okta, Azure AD, or IAM Identity Center? | Enterprise identity can connect reviewer roles, access policies, and approval authorization, then map group claims to Engineering, Legal, Business, and administrator permissions. |
| How could cost be reduced? | Use cache-first validation, exact prompt cache, retained KB reuse, lifecycle policies, cost dashboards, model selection by task complexity, and targeted validation before broad runs. |
| How could security be improved? | Split IAM roles, add WAF/auth/rate limiting, private access, VPC endpoints, KMS policy review, sensitive-data discovery, drift alerts, and approval endpoint identity binding. |
| How could this scale to other laws? | Add law-specific checklist assets, statute chunks, routing policies, evaluation truth, and failure taxonomy. Do not simply reuse prompts without law-specific evaluation. |
| How could this be explained to a C-suite customer? | "AI prepares a grounded first pass for review, reducing manual triage time, while human experts retain final judgment. We measure quality before rollout and harden security before production." |
