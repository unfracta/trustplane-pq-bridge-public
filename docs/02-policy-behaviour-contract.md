# 02. Policy Behaviour Contract

This is the buyer-readable behaviour contract for TrustPlane PQ Bridge.

The product rule is:

> Developers choose policy. TrustPlane PQ Bridge defines, enforces, verifies, and records the resulting signing behaviour.

## Buyer-Facing Policy Set

The v1 policy set is:

1. `legacy_required`
2. `hybrid_preferred`
3. `hybrid_required`
4. `pq_required`

`pq_preferred` is treated as deprecated compatibility behaviour and is not part of the public buyer-facing demo path.

## Evidence Contract

Every externally visible plan, envelope, verification result, and explanation should expose policy evidence with these fields:

| Field | Meaning |
| --- | --- |
| `decision` | `sign`, `refuse`, `verify`, or `reject`. |
| `policy` | Policy value applied to the operation. |
| `capabilities_snapshot` | Runtime capability state used for the decision. |
| `fallback_applied` | Whether a permitted fallback path was used. |
| `algorithms_used` | Algorithm identifiers produced or considered by the operation. |
| `failure_reason` | Refusal or rejection reason, or `null` when successful. |

Strict verification rejects evidence-inconsistent envelopes.

## Capability States

| Capability State | Classical | Post-Quantum |
| --- | ---: | ---: |
| Hybrid capable | Yes | Yes |
| Classical only | Yes | No |
| PQ only | No | Yes |
| No signing support | No | No |

## Behaviour Matrix

| Policy | Capabilities | Decision | Signing Behaviour | Fallback | Failure Reason |
| --- | --- | --- | --- | --- | --- |
| `legacy_required` | Hybrid capable | `sign` | Classical only | No | `null` |
| `legacy_required` | Classical only | `sign` | Classical only | No | `null` |
| `legacy_required` | PQ only | `refuse` | No signature | No | Classical unavailable |
| `legacy_required` | No signing support | `refuse` | No signature | No | Classical unavailable |
| `hybrid_preferred` | Hybrid capable | `sign` | Classical plus PQ | No | `null` |
| `hybrid_preferred` | Classical only | `sign` | Classical only | Yes | `null` |
| `hybrid_preferred` | PQ only | `refuse` | No signature | No | Classical unavailable |
| `hybrid_preferred` | No signing support | `refuse` | No signature | No | Classical unavailable |
| `hybrid_required` | Hybrid capable | `sign` | Classical plus PQ | No | `null` |
| `hybrid_required` | Classical only | `refuse` | No signature | No | Hybrid requires classical and PQ |
| `hybrid_required` | PQ only | `refuse` | No signature | No | Classical unavailable |
| `hybrid_required` | No signing support | `refuse` | No signature | No | Classical unavailable |
| `pq_required` | Hybrid capable | `sign` | PQ only | No | `null` |
| `pq_required` | Classical only | `refuse` | No signature | No | PQ required but unavailable |
| `pq_required` | PQ only | `sign` | PQ only | No | `null` |
| `pq_required` | No signing support | `refuse` | No signature | No | PQ required but unavailable |

## Verification Rules

1. `legacy_required` verification accepts the classical path.
2. `hybrid_preferred` verification prefers PQ when available and may fall back to classical.
3. `hybrid_required` verification succeeds only when both classical and PQ signatures verify.
4. `pq_required` verification accepts only the PQ path.
5. Strict verification rejects unsupported, disallowed, tampered, or evidence-inconsistent envelopes.

## Contract Guarantee

Given the same policy, capability state, and envelope metadata, PQ Bridge should return one valid outcome. There should be no hidden policy branch that changes signing or verification behaviour outside this contract.
