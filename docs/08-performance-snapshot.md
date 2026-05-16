# 08. Performance Snapshot

This snapshot shows local evaluator performance for TrustPlane PQ Bridge.

It is intended to answer a practical question:

> Does high-assurance trust control add enough overhead to make the system impractical?

The short answer from this run is no for the default enterprise path. Classical, hybrid, and ML-DSA post-quantum signing remained sub-millisecond in the standard benchmark. SLH-DSA is supported, but it has a different performance profile and should be selected deliberately.

## Environment

Snapshot date: `2026-05-13`

Runtime:

1. Node.js `v24.13.0`
2. macOS `darwin`
3. Architecture `arm64`
4. Payload size: `211` bytes for the standard benchmark

Command:

```bash
npm run bench:repro -- --outdir out/performance-rerun-2026-05-13 --timestamp 2026-05-13T00-00-00-000Z
```

The reproducibility report compared the local run against the benchmark baseline and reported:

> No regressions detected.

## Standard TrustPlane Benchmark

These figures include TrustPlane policy handling, canonical envelope generation, signing, verification, and evidence output paths used by the SDK benchmark.

| Scenario | Average | Median | p95 | Throughput |
|---|---:|---:|---:|---:|
| Classical sign | `0.061 ms` | `0.046 ms` | `0.106 ms` | `16,343 ops/sec` |
| Classical verify | `0.079 ms` | `0.070 ms` | `0.109 ms` | `12,657 ops/sec` |
| Hybrid sign | `0.233 ms` | `0.195 ms` | `0.499 ms` | `4,293 ops/sec` |
| Hybrid verify | `0.057 ms` | `0.051 ms` | `0.069 ms` | `17,625 ops/sec` |
| PQ-only sign | `0.215 ms` | `0.182 ms` | `0.454 ms` | `4,650 ops/sec` |
| PQ-only verify | `0.057 ms` | `0.050 ms` | `0.082 ms` | `17,661 ops/sec` |

## PQ Algorithm Spread

The default PQ path is ML-DSA. SLH-DSA is available for enterprises that need a stateless post-quantum signature family, but signing cost and signature size are materially higher.

| Algorithm | Signature bytes | Sign average | Verify average | Practical interpretation |
|---|---:|---:|---:|---|
| `oqs-ml-dsa-44` | `2,420` | `0.214 ms` | `0.059 ms` | Default practical PQ path |
| `oqs-ml-dsa-65` | `3,309` | `0.331 ms` | `0.086 ms` | Stronger ML-DSA option |
| `oqs-ml-dsa-87` | `4,627` | `0.390 ms` | `0.134 ms` | Highest ML-DSA level currently exposed |
| `oqs-slh-dsa-sha2-128f` | `17,088` | `12.041 ms` | `0.762 ms` | Selective stateless PQ signing |
| `oqs-slh-dsa-sha2-128s` | `7,856` | `250.423 ms` | `0.266 ms` | Smaller signature, much slower signing |
| `oqs-slh-dsa-sha2-256f` | `49,856` | `40.690 ms` | `1.088 ms` | High-assurance selective use |
| `oqs-slh-dsa-shake-256s` | `29,792` | `835.513 ms` | `0.878 ms` | Not a default online signing path |

## How To Read This

Standard signing infrastructure usually answers:

> Can this application produce a valid signature?

TrustPlane PQ Bridge answers a wider question:

> Was this action allowed under the correct trust policy and verified under evidence-bound conditions?

That policy, verification, and evidence layer adds work around the raw signing operation. The benchmark indicates that this overhead remains practical for common high-assurance enterprise workflows, especially when ML-DSA is the default post-quantum signature family.

## Positioning Guidance

1. Use ML-DSA as the default enterprise PQ signing path.
2. Use SLH-DSA where stateless PQ signatures, algorithmic diversity, or assurance posture justify the signing cost.
3. Do not treat SLH-DSA `s` variants as high-volume online signing defaults.
4. Keep performance evaluation tied to the enterprise's own hardware, workload, key infrastructure, and verification boundary.

## Caveats

1. This is a local evaluator benchmark, not an independent third-party audit.
2. Results are hardware, runtime, payload, and configuration dependent.
3. The figures are useful for evaluation planning, not universal performance claims.
4. KMS/HSM or remote signing latency is not included in this snapshot.
