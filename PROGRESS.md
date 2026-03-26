# Parameter Golf — Progress Chart

**Last Updated:** 2026-03-26 14:40 CDT

---

## Current Status: PAUSED — Waiting on Compute Grant

- **PR #858 submitted:** https://github.com/openai/parameter-golf/pull/858
- **Score:** val_bpb 1.2135 (3-seed mean, std 0.0003)
- **Grant applied:** Development tier ($500) on RunPod via OpenAI form
- **Expected response:** 24-48 hours
- **RunPod account:** Created with same email as OpenAI account
- **Next step:** When grant arrives, scale novel architectures to 8xH100

---

## Submission Status

| Item | Status |
|------|--------|
| Fork | ✅ github.com/nickferrantelive/parameter-golf |
| Upstream sync | ✅ Synced with openai/parameter-golf |
| 3-seed runs (8xH100 SXM) | ✅ Seeds 42, 1337, 2025 — all pass |
| PR #858 | ✅ Open, awaiting review |
| Grant application | ✅ Submitted, Development tier ($500) |
| RunPod account | ✅ Created |
| Grant response | ⏳ Waiting (24-48h) |

---

## Leaderboard Intelligence (as of 2026-03-26)

**Only 5 PRs have been merged total.** OpenAI is filtering aggressively.

### Merged entries (actually on leaderboard):
| Entry | Score | Author | Merged |
|-------|-------|--------|--------|
| LeakyReLU² + Legal TTT + Parallel Muon | **1.1194** | abaybektursun | Mar 24 |
| 11L EMA + GPTQ-lite + warmdown3500 | 1.1228 | signalrush | Mar 23 |
| 11L Partial RoPE + LN Scale + EMA + XSA4 | 1.1248 | jfprincz | Mar 23 |
| 11L XSA4 + EMA + Int6 MLP3x | 1.1271 | jfprincz | Mar 23 |
| 11L Efficient Partial XSA | 1.1307 | unnir | Mar 23 |
| + earlier entries from Mar 18-20 (direct commits) | 1.12-1.22 | various | Mar 18-20 |
| Ternary Quantization (73.7M params) | 1.1570 | Ciprian-Florin Ifrim | Mar 25 |
| Binary Quantization (non-record) | 1.1239 | Ciprian-Florin Ifrim | Mar 25 |

### Open PRs: 100+ (most are junk/AI-generated, many claiming impossible scores)
### Closed without merge: 95 (rejected)
### Merge cadence: ~1-2 per day, only legitimate reproducible entries

---

## What We're Building (for when grant arrives)

### Priority 1: Novel Architectures (differentiators)
1. **Hybrid GatedRNN-Attention** — 3 RNN + 8 attention layers, val_bpb 2.529 at 200 steps on 4070 Super
2. **Recursive Shared-Weight Transformer** — 1 block x12, unique params ~3MB
3. **Codec Model** — bigram embed + unigram projection, val_bpb 2.63 at 200 steps

### Priority 2: Aggressive Quantization
- Ternary/int5 to fit 60-80M params in 16MB
- Combine with parameter-efficient architectures above

### Priority 3: Proven Technique Stacking
- LeakyReLU(0.5)^2, Parallel Muon, XSA, Partial RoPE, LN Scale
- SmearGate, BigramHash, EMA, GPTQ-lite, Late QAT
- Legal score-first TTT
- Layer these onto novel architectures

---

## Model Build Status

| Model | Name | Steps | Smoke Test | Best Score (200 steps) | Size | Status |
|-------|------|-------|-----------|----------------------|------|--------|
| **1** | Codec | 5/5 | ✅ ALL PASS | val_bpb 2.63 | 8.0 MB | COMPLETE |
| **4** | Optimized Transformer | 15/15 | ✅ ALL PASS | 3.83 bpb | 5.1 MB | COMPLETE |
| **2** | Recursive (Shared Weights) | 3/3 | ✅ ALL PASS | 4.01 loss | ~5.7 MB | COMPLETE |
| **3** | Hybrid (GatedRNN + Attention) | 3/3 | ✅ ALL PASS | 2.529 bpb | ~5.1 MB | COMPLETE |
| **6** | Hive (Frozen + LoRA) | 3/3 | ✅ ALL PASS | 4.031 bpb | 9.4 MB | COMPLETE |
| **7** | Immune (Template Library) | 3/3 | ✅ ALL PASS | 3.464 bpb | 5.3 MB | COMPLETE |
| **8** | Crystal (Seed + Growth) | 3/3 | ✅ ALL PASS | 3.342 bpb | 5.2 MB | COMPLETE |
| **5** | Frankenstein | 2/2 | ✅ ALL PASS | 3.257 bpb | 6.4 MB | COMPLETE |

---

## Budget

| Platform | Balance | Notes |
|----------|---------|-------|
| RunPod | $15.62 remaining | From initial $20 deposit |
| Vast.ai | ~$19.20 remaining | From initial $20 |
| RunPod grant | ⏳ Pending | Applied for $500 Development tier |

---

## Key Files

| File | Purpose |
|------|---------|
| train_gpt.py | Stock baseline (used for PR #858) |
| train_gpt_submission_m4.py | Enhanced script with all SOTA techniques |
| train_gpt_m1_*.py | Codec model iterations |
| train_gpt_m2_*.py | Recursive model iterations |
| train_gpt_m3_*.py | Hybrid RNN-attention iterations |
| logs/seed*.txt | 3-seed run logs for PR #858 |
| GRANT-APPLICATION.md | Grant application text (submitted) |
| records/track_10min_16mb/2026-03-26_20M_Int8Zlib_11L_MLP3x/ | PR #858 submission files |
