# 03. 3-Minute Demo Walkthrough

This is the public version of the PQ Bridge demo story.

## Demo Promise

Show that PQ Bridge can move a signing workflow from classical to hybrid to post-quantum policy, verify the result strictly, and preserve evidence without changing the application payload.

## Audience

1. Security architecture
2. Platform engineering
3. Cryptography migration teams
4. Technical diligence reviewers

## Minute 1: The Risk

Enterprises cannot switch every system to post-quantum signing at once.

Some boundaries still need classical compatibility. Some boundaries need both classical and PQ proof. Some future-facing boundaries should require PQ-only behaviour.

The migration risk is uncontrolled exception handling.

## Minute 2: The Policy Change

The same action can be evaluated under different policies:

| Policy | Intended Meaning |
| --- | --- |
| `legacy_required` | Classical compatibility is required. |
| `hybrid_preferred` | Use classical plus PQ when possible, with permitted classical fallback. |
| `hybrid_required` | Classical and PQ are both required, or the action is refused. |
| `pq_required` | PQ is required, or the action is refused. |

The application payload does not need to choose algorithms directly. The policy controls the allowed signing and verification behaviour.

## Minute 3: Evidence And Refusal

The important product moment is not just a successful signature.

The important product moment is:

1. strict verification succeeds when the proof is valid
2. strict verification refuses tampered or wrong-policy evidence
3. the evidence explains what happened
4. the same evidence can be shown to a reviewer without source access

## Enterprise Takeaway

TrustPlane PQ Bridge lets a team migrate signing trust modes through policy while preserving strict verification evidence and operational control.

## We Do Not Overclaim

PQ Bridge does not replace KMS, HSM, PKI, IAM, or certificate lifecycle management. It consumes existing customer trust infrastructure and makes policy-controlled signing and verification behaviour explicit.
