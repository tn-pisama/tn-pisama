# Evaluation status and benchmark correction

I published a [TRAIL benchmark](https://arxiv.org/abs/2505.08638) result for these detectors
and then withdrew it. My scoring harness only ever built detector input for spans that already
carried a gold label, so a false positive was structurally unrecordable: precision was 1.0 by
construction, and every F1 I reported was a restatement of recall. I found it in my own code,
fixed the runner, re-scored all 148 traces, and the corrected accuracy was substantially lower.
Pisama publishes no benchmark figure while the evaluation is rebuilt on a held-out corpus.

Detector-level evaluation is in-sample today. That is a real limitation and I state it rather
than route around it.

---

This disclosure was moved from the profile README on September 25, 2026.
The profile cleanup does not introduce new benchmark results or change the stated evaluation limitations.

[Back to my profile](https://github.com/tn-pisama)
