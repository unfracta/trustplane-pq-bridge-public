# 01. Product Overview

TrustPlane PQ Bridge helps teams control cryptographic migration through policy rather than one-off application logic.

The first wedge is post-quantum signing migration:

```mermaid
flowchart LR
  A["Application or workflow"] --> B["TrustPlane policy"]
  B --> C["Plan: sign, refuse, or verify"]
  C --> D["Signed envelope or refusal"]
  D --> E["Strict verification"]
  E --> F["Reviewer-readable evidence"]
```

## The Problem

Post-quantum migration is not a single switch.

1. Some systems still need classical compatibility.
2. Some boundaries should require classical plus PQ signatures.
3. Some future-facing workflows should require PQ-only behaviour.
4. Security reviewers need evidence of what happened and why.

Without a policy layer, migration logic becomes scattered across services, deployment scripts, and reviewer notes.

## The PQ Bridge Approach

Developers choose policy. TrustPlane decides the allowed cryptographic behaviour.

Supported buyer-facing policies:

1. `legacy_required`
2. `hybrid_preferred`
3. `hybrid_required`
4. `pq_required`

Every outcome should answer:

1. What policy was applied?
2. What capabilities were available?
3. Which algorithms were used?
4. Did fallback happen?
5. Why did signing, verification, or refusal occur?

## What This Is

1. Policy-driven cryptographic trust infrastructure.
2. A deterministic signing and verification control layer.
3. A source-free evaluator path for design partners.
4. A practical proof point for post-quantum migration readiness.

## What This Is Not

1. Not a hosted SaaS control plane today.
2. Not KMS, HSM, key custody, or certificate lifecycle management.
3. Not IAM, PKI, CI/CD, or ERP replacement.
4. Not a generic AI governance dashboard.
5. Not a public source release.

## Why It Matters

The value is not “another signing library.”

The value is being able to prove:

> This specific action was signed or refused under the correct policy, with the correct capabilities, at the correct point of execution, and verification evidence exists.
