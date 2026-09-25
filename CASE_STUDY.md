# Case study: a repair must keep protecting the workflow

Pisama for n8n turns execution evidence into deterministic input guards. This walkthrough uses the repository's small regression fixtures, not a customer incident or an independent performance benchmark.

## Failure and evidence

A consumer reads `$json.required.value`. Its recorded input is `{"body": {"x": 1}}`, and execution reports `Cannot read properties of undefined (reading 'value')`.

Pisama combines the property access, error, and recorded input to identify `required.value` as a confirmed missing path. Without recorded input, it reports only a candidate. If the path is present, it also refuses to call it confirmed. These distinctions keep incomplete evidence from becoming a certain diagnosis.

See [`TestObservedPaths`](https://github.com/Pisama-AI/pisama-n8n/blob/4fee74dd45f9561301dcb3b914b7bf93c6282532/engine/tests/test_guardrails.py).

## Repair and its boundary

The deterministic repair inserts a guard upstream of the consumer:

```text
Source → inspect required paths → valid? → original consumer
                                   └──→ explicit rejection route
```

The validated branch preserves the original valid item. The rejection branch carries missing path names, not rejected payload values. Missing and null values fail the guard; zero and empty strings are preserved because their validity depends on the application.

This repair rejects malformed input; it does not reconstruct missing data or prove that the business task succeeded. Paths must match the consumer's actual input shape. For example, a Webhook body may require `body.required.value` instead of `required.value`.

See [guardrail documentation](https://github.com/Pisama-AI/pisama-n8n/blob/4fee74dd45f9561301dcb3b914b7bf93c6282532/docs/input-schema-guardrail.md) and [implementation](https://github.com/Pisama-AI/pisama-n8n/blob/4fee74dd45f9561301dcb3b914b7bf93c6282532/engine/pisama_n8n_engine/guardrails.py).

## The subtle failure: an intact guard can be bypassed

After insertion, someone can add a direct edge from the source to the consumer. Every guard node still exists, and the validated branch remains connected—but malformed input now has a path around the guard.

Pisama checks wiring and reports `guard_bypassed`. Separate regression cases cover deleted guard nodes, detached validated branches, and broken rejection paths. The test also checks that the intended validated connection is not itself mistaken for a bypass.

The same suite covers another edge case: for `$json.a.b.split(',')`, the required input is `a.b`, not `a.b.split`. The test executes the generated JavaScript in Node to verify that a valid string passes the correct guard.

See [`TestGuardDriftDetection` and the generated-validator regression](https://github.com/Pisama-AI/pisama-n8n/blob/4fee74dd45f9561301dcb3b914b7bf93c6282532/engine/tests/test_guardrails.py).

## Reproduce the focused verification

Verified on September 25, 2026 at commit `4fee74dd45f9561301dcb3b914b7bf93c6282532`, using Python 3.14.4, pytest 9.0.2, and Node 26.8.1:

```bash
git clone https://github.com/Pisama-AI/pisama-n8n.git
cd pisama-n8n
git checkout 4fee74dd45f9561301dcb3b914b7bf93c6282532
python3 -m venv .venv
. .venv/bin/activate
python -m pip install pytest==9.0.2
# Install Node and ensure `node` is on PATH for the generated-JavaScript test.
PYTHONPATH=engine python -m pytest engine/tests/test_guardrails.py -q
```

Observed result: **38 passed, no skips**. The suite includes path confirmation, guard insertion, generated JavaScript, drift detection, and bounded error-route changes.

This is local regression evidence. It does not establish production effectiveness, held-out precision/recall, or a live n8n repair lifecycle. The repository has a [separate lifecycle runner](https://github.com/Pisama-AI/pisama-n8n/blob/4fee74dd45f9561301dcb3b914b7bf93c6282532/scripts/run_guardrail_lifecycle.py); that runner was not executed for this profile update.

[Back to my profile](https://github.com/tn-pisama) · [Evaluation disclosure](EVALUATION.md)
