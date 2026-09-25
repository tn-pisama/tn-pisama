# Hi, I’m Tuomo. I build Pisama.

I build systems that find where AI agent workflows fail, turn execution evidence into proposed repairs, and check whether those repairs hold.

At [Pisama](https://pisama.ai), my focus is adaptive failure detection, deterministic workflow guards, and verification that keeps unknown or unchecked outcomes explicit.

[Website](https://pisama.ai) · [Documentation](https://docs.pisama.ai) · [Code](https://github.com/Pisama-AI)

## A concrete engineering example

**A guard can exist and still be bypassed.** In Pisama for n8n, adding a direct source-to-consumer connection can defeat an otherwise intact input guard. Pisama checks the wiring and reports that bypass.

[Read the case study: failure evidence → repair → drift detection](https://github.com/tn-pisama/tn-pisama/blob/main/CASE_STUDY.md). Includes commit-pinned source, a reproducible command, and 38 passing local regression tests. This is engineering verification, not a production benchmark.

## Selected Pisama work

- [Python CLI, SDK, and MCP server](https://github.com/Pisama-AI/pisama-python) — explicit detector assessments distinguish findings, abstentions, errors, and unknown coverage. [Inspect the tests](https://github.com/Pisama-AI/pisama-python/blob/ada910a7ad59225fc3b02519f4b2b87e53722a9e/tests/test_assessment_coverage.py).
- [TypeScript tooling](https://github.com/Pisama-AI/pisama-js) — SDK middleware, local detectors, and CLI integration.
- [Pisama for n8n](https://github.com/Pisama-AI/pisama-n8n) — execution-based diagnosis and deterministic workflow repairs.
- [Verifier Gym](https://github.com/Pisama-AI/pisama-verifier-gym) — verifier audits, agreement metrics, and release gates; used internally, with limited external maintenance.

## Evaluation

I withdrew an earlier TRAIL benchmark after finding a scoring flaw. Detector evaluation remains in-sample; independent performance claims await held-out evaluation. [Full correction and evaluation status](https://github.com/tn-pisama/tn-pisama/blob/main/EVALUATION.md).
