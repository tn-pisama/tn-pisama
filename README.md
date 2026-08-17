> All Pisama repositories are at [github.com/Pisama-AI](https://github.com/Pisama-AI). Old `tn-pisama/*` URLs redirect.

# Hi, I'm Tuomo

I build [Pisama](https://pisama.ai), process-level failure detection for LLM agent systems.

## What I'm working on

**[Pisama](https://github.com/Pisama-AI)** is the layer between observability and rubric-based artifact evaluation for AI agents. Calibrated detectors catching loops, hallucinations, prompt injection, persona drift, state corruption, coordination breakdown and convergence failures, running locally at $0, with optional LLM-judge escalation when needed.

Integrations for LangGraph, Claude Code, n8n, Dify, OpenClaw, AWS Bedrock Agents, AWS Managed Agents and OpenAI Assistants.

Built on the [MAST taxonomy](https://arxiv.org/abs/2503.13657) (NeurIPS 2025).

## On measurement

I published a [TRAIL benchmark](https://arxiv.org/abs/2505.08638) result for these detectors
and then withdrew it. My scoring harness only ever built detector input for spans that already
carried a gold label, so a false positive was structurally unrecordable: precision was 1.0 by
construction, and every F1 I reported was a restatement of recall. I found it in my own code,
fixed the runner, re-scored all 148 traces, and the corrected accuracy was substantially lower.
Pisama publishes no benchmark figure while the evaluation is rebuilt on a held-out corpus.

Detector-level evaluation is in-sample today. That is a real limitation and I state it rather
than route around it.

[![pisama](https://img.shields.io/pypi/v/pisama?label=pisama&style=flat-square&color=blue)](https://pypi.org/project/pisama/)
[![pisama-detectors](https://img.shields.io/pypi/v/pisama-detectors?label=pisama-detectors&style=flat-square&color=blue)](https://pypi.org/project/pisama-detectors/)
[![pisama-auto](https://img.shields.io/pypi/v/pisama-auto?label=pisama-auto&style=flat-square&color=blue)](https://pypi.org/project/pisama-auto/)

## Background

Previously VP Data at Underdog Fantasy; earlier data and AI roles at Zynga, Jam City, 2K, and Omniata. Research background in innovation economics at Aalto University and ETLA. [Google Scholar](https://scholar.google.com/citations?user=16zo9WAAAAAJ)

## Tech

`Python` · `TypeScript` · `FastAPI` · `Next.js` · `PostgreSQL` · `pgvector` · `OpenTelemetry` · `LangGraph`

## Reach me

[pisama.ai](https://pisama.ai) · [docs.pisama.ai](https://docs.pisama.ai)
