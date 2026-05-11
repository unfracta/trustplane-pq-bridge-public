# 05. Evidence Examples

These examples are sanitized outputs from the evaluator proof-pack flow.

They are included to show the shape of the evidence, not to expose source code.

## Included Examples

1. [Strict verification pass](../examples/evidence/strict-verification.json)
2. [Tamper refusal](../examples/evidence/tamper-refusal.json)
3. [Proof-gate pass](../examples/evidence/proof-gate-pass.json)
4. [Proof-gate failure](../examples/evidence/proof-gate-failure.json)

## What To Look For

In a successful verification:

1. `valid` is `true`
2. `payload_sha256` is present
3. `envelope_sha256` is present
4. `evidence.decision` is `verify`
5. `evidence.policy` matches the expected policy
6. `evidence.algorithms_used` is explicit

In an expected refusal:

1. `valid` or `gate.pass` is `false`
2. the failed check is visible
3. the refusal reason is explicit
4. the action stops before execution

## Why This Matters

TrustPlane PQ Bridge is designed so reviewers do not need to infer behaviour from logs or trust a verbal explanation.

The proof itself should answer:

1. what policy was applied
2. what was signed or refused
3. what verification checked
4. why the workflow passed or failed
