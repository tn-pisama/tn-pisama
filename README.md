![Pisama: Before you switch AI models, know what changes.](assets/pisama-migration-header.png)

# Tuomo Nikulainen

I'm building [Pisama](https://pisama.ai) around a practical question: **does a replacement AI model still meet the requirements of your workflow?**

My current focus is assisted model migration assessment for read-only, text-based workflows. The work starts with existing examples, logs and business requirements, then compares the current model with candidate replacements. I investigate which behaviors improve, which regress and where the evidence remains incomplete.

The aim is a recommendation a team can inspect, with individual cases and tested configurations behind it. The team makes the rollout decision.

[Website](https://pisama.ai) | [Pisama repositories](https://github.com/Pisama-AI) | [LinkedIn](https://www.linkedin.com/in/tuomonikulainen/)

## What I'm building

- Workflow reconstruction and repeatable model comparisons.
- Acceptance criteria, regression analysis and output compatibility checks.
- Python and TypeScript tooling for evaluation and evidence review.

Previously, I led data organizations at Zynga and Underdog and AI & Data at Bellota Labs. I bring that background in experimentation and production systems to hands-on engineering.

## Selected engineering work

The migration work builds on earlier work in failure detection and verification. These examples include implementation and regression tests:

**Preventing silent loss of failure evidence.** A JSONL loader could accept a trace envelope and ignore later rows. The fix rejects mixed envelopes instead of dropping evidence, and rejects empty or unsupported inputs before analysis. [Merged change #26](https://github.com/Pisama-AI/pisama-python/pull/26).

**Separating reported checks from verified coverage.** An initial API confused detector reporting with complete trace coverage. The correction gives reporting completeness its own meaning, validates span positions and counts, and preserves findings when coverage metadata contradicts them. [Initial change #28](https://github.com/Pisama-AI/pisama-python/pull/28) · [Correction #30](https://github.com/Pisama-AI/pisama-python/pull/30).

**Detecting repairs that have been bypassed.** An n8n input guard can remain present while a new connection routes around it. Pisama checks the workflow wiring as well as the guard's existence. [Walkthrough, source, and reproduction steps](https://github.com/tn-pisama/tn-pisama/blob/main/CASE_STUDY.md).

## Explore the code

[Python SDK / CLI / MCP](https://github.com/Pisama-AI/pisama-python) | [Verifier audits](https://github.com/Pisama-AI/pisama-verifier-gym) | [TypeScript SDK / detectors / CLI](https://github.com/Pisama-AI/pisama-js) | [n8n detection and repairs](https://github.com/Pisama-AI/pisama-n8n) | [Documentation](https://docs.pisama.ai)

## Evaluation status

I withdrew an earlier TRAIL benchmark after finding a scoring flaw. Detector evaluation remains in-sample; independent performance claims await held-out evaluation. [Full correction and evaluation status](https://github.com/tn-pisama/tn-pisama/blob/main/EVALUATION.md).
