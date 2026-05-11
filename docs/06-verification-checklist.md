# 06. Verification Checklist

Use this checklist when reviewing PQ Bridge evidence.

## Required Proof

1. Policy selected before signing or refusal.
2. Strict verification result captured after signing.
3. Payload SHA-256 and envelope SHA-256 recorded.
4. Policy evidence present with:
   - decision
   - policy
   - capabilities snapshot
   - fallback indicator
   - algorithms used
   - failure reason when refused
5. One deliberate refusal captured, such as tampered evidence or wrong-policy proof.

## Pass Signal

The evidence is useful when a reviewer can answer:

1. What policy was applied?
2. What runtime capabilities were available?
3. Which algorithms were used?
4. Did fallback happen?
5. Why did verification pass or fail?

## Boundary

This checklist proves policy and verification behaviour. It does not grant production rights, source access, redistribution rights, or named public reference rights.
