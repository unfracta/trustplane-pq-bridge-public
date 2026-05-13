# TrustPlane PQ Bridge

Public evaluator materials for TrustPlane PQ Bridge.

TrustPlane is policy-governed signing infrastructure for enterprise applications. PQ Bridge is the first concrete wedge: a controlled way to move signing and verification behaviour from classical cryptography toward hybrid and post-quantum trust modes.

The core product repo remains private during design-partner evaluation. This public repo shows enough to review the product idea, policy contract, evidence model, and workflow-gate pattern without exposing source code or private operating material.

## The 10-Minute Path

Read these in order:

1. [Product Overview](docs/01-product-overview.md)
2. [Policy Behaviour Contract](docs/02-policy-behaviour-contract.md)
3. [3-Minute Demo Walkthrough](docs/03-hero-demo-walkthrough.md)
4. [GitHub Actions Proof Gate](docs/04-github-actions-proof-gate.md)
5. [Evidence Examples](docs/05-evidence-examples.md)
6. [Verification Checklist](docs/06-verification-checklist.md)
7. [Performance Snapshot](docs/08-performance-snapshot.md)
8. [Request Evaluator Access](docs/07-request-evaluator-access.md)

## What This Shows

1. How policy controls signing and verification behaviour.
2. How strict verification produces reviewer-readable evidence.
3. How tampered or wrong-policy proof is refused.
4. How a workflow gate can enforce: no valid TrustPlane proof, no deployment.
5. How policy-governed signing performs in a local evaluator benchmark.

## What This Does Not Include

1. Source code.
2. Tests.
3. Private appliance scripts.
4. Tokens, private keys, or customer data.
5. Internal notes or private operating assumptions.
6. Production-use rights.

## Current Status

PQ Bridge is in private evaluator and design-partner mode.

Qualified reviewers can request access to the source-free appliance pack and fuller proof materials.
