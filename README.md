# Tuomo — building Pisama

I build [Pisama](https://pisama.ai), tooling for diagnosing failures in AI agent workflows and checking proposed repairs. My work spans Python and TypeScript SDKs, trace analysis, evaluation infrastructure, and n8n workflow repairs.

The engineering question I focus on: **what evidence is sufficient to call an agent run checked, failed, or repaired?**

[Website](https://pisama.ai) · [Documentation](https://docs.pisama.ai) · [Pisama repositories](https://github.com/Pisama-AI)

## Selected engineering work

Three concrete examples, with implementation and regression tests:

**Preventing silent loss of failure evidence.** A JSONL loader could accept a trace envelope and ignore later rows. The fix rejects mixed envelopes instead of dropping evidence, and rejects empty or unsupported inputs before analysis. [Merged change #26](https://github.com/Pisama-AI/pisama-python/pull/26).

**Separating reported checks from verified coverage.** An initial API confused detector reporting with complete trace coverage. The correction gives reporting completeness its own meaning, validates span positions and counts, and preserves findings when coverage metadata contradicts them. [Initial change #28](https://github.com/Pisama-AI/pisama-python/pull/28) · [Correction #30](https://github.com/Pisama-AI/pisama-python/pull/30).

**Detecting repairs that have been bypassed.** An n8n input guard can remain present while a new connection routes around it. Pisama checks the workflow wiring as well as the guard's existence. [Walkthrough, source, and reproduction steps](https://github.com/tn-pisama/tn-pisama/blob/main/CASE_STUDY.md).

## Explore the code

[Python SDK / CLI / MCP](https://github.com/Pisama-AI/pisama-python) · [TypeScript SDK / detectors / CLI](https://github.com/Pisama-AI/pisama-js) · [n8n detection and repairs](https://github.com/Pisama-AI/pisama-n8n) · [Verifier audits](https://github.com/Pisama-AI/pisama-verifier-gym)

## Evaluation status

I withdrew an earlier TRAIL benchmark after finding a scoring flaw. Detector evaluation remains in-sample; independent performance claims await held-out evaluation. [Full correction and evaluation status](https://github.com/tn-pisama/tn-pisama/blob/main/EVALUATION.md).
