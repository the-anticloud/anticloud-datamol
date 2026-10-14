# Students — DATAMOL

**Project:** DATAMOL  
**Category:** MEDICINE_DEVELOPMENT  
**Upstream:** https://github.com/datamol-io/datamol  
**Pinned commit:** `ea501d4bbe12909325eaceb881abfbc316440c9a`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `29c2a8a3cafabcba80878cc7b6c81f11b898b01f24745cf48d52596680c73ddd`  
**Date:** October 2026

## What this project gives you

A complete worked example of offline-first packaging with a cryptographic audit
chain: source pinned at `ea501d4bbe12909325eaceb881abfbc316440c9a`, a 16-check assurance suite, an evidence register
with per-check hashes, and an AIOSS ledger chain ending at `29c2a8a3cafabcba80878cc7b6c81f11b898b01f24745cf48d52596680c73ddd`.

## Learn by verifying

```
python tools/run_bench.py --out BENCH.json
```

Then take any row from `ISOLATED_LAB_RESULTS/03_Result_Register.md`, recompute
the SHA3-256 of its evidence file, and confirm it matches. If it does not match,
the record has been altered — that is the whole point of the chain.

## Licence

Apache 2.0 terms apply to study and teaching use.
