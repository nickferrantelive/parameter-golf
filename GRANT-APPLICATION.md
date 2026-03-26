# Parameter Golf — Compute Grant Application

**Form fields from screenshot:**
1. Detailed approach (max 2,500 characters)
2. Current best leaderboard submission score
3. What improvement you expect from additional compute (max 1,500 characters)
4. Confirmation checkbox (email tied to ChatGPT/OpenAI account)

---

## Field 1: Detailed approach (2,500 char max)

```
I have a working 8×H100 pipeline with a submitted PR (#858, val_bpb 1.2135, 3-seed verified). I'm systematically combining proven leaderboard techniques to push toward SOTA, plus testing novel architectures nobody else has tried.

APPROACH 1 — FULL SOTA STACK INTEGRATION
Combining all techniques from merged leaderboard entries into one model:
• 11L 512d, 3× MLP, U-Net skip connections, GQA (4 KV heads)
• LeakyReLU(0.5)² activation (from SOTA entry #549)
• Partial RoPE (16/64 dims) + layerwise LN Scale (from #287)
• XSA on last 4 layers (from #198/#287)
• SmearGate + BigramHash for token-pair context (from #65/#162)
• EMA (0.997) + Tight SWA during warmdown (from #414)
• GPTQ-lite int6 with 5-percentile clip search + int8 embeddings
• Late QAT (STE fake-quant when LR scale < 0.15)
• Warmdown 3500, Muon WD=0.04, gradient clip 0.3
• Sliding window eval stride=64
Each technique is individually verified on the leaderboard. The key research question is optimal composition and hyperparameter tuning across all of them simultaneously.

APPROACH 2 — AGGRESSIVE QUANTIZATION FOR MORE PARAMETERS
Using ternary/int5 quantization to fit 60-80M params in 16MB (vs current 20M):
• Ternary quantization (proven: 73.7M params merged at 1.1570)
• Mixed int5/int6 per-layer (proven: merged at 1.1428)
• PolarQuant 3-4 bit weights (26% more params per MB)
• More params with good quantization = lower loss. Highest leverage approach.

APPROACH 3 — LEGAL TEST-TIME TRAINING
• Score-first TTT: evaluate tokens, adapt model, re-score (from SOTA #549)
• LoRA-based TTT (proven: merged at 1.1928)
• AdamW with cosine schedule, per-document adaptation
• Combined with Approach 1's training stack for maximum impact.

APPROACH 4 — NOVEL ARCHITECTURES (unique to my submission)
Smoke-tested locally on RTX 4070 Super, need H100s to scale:
• Hybrid GatedRNN + Attention (3 RNN + 8 attention layers) — showed val_bpb 2.529 at just 200 steps
• Recursive shared-weight transformer (1 block applied 12×) — extreme param efficiency
• These architectures are absent from the leaderboard entirely.

All code is ready. I need compute to run full-scale training + 3-seed verification.
```

**Character count: ~2,033** ✅ (under 2,500)

---

## Field 2: Current best leaderboard submission score

```
1.2135
```

---

## Field 3: What improvement you expect from additional compute (1,500 char max)

```
My current 1.2135 uses only the stock baseline with 11 layers — no advanced techniques applied yet. I have implementations of all major SOTA techniques ready but untested at 8×H100 scale.

EXPECTED IMPROVEMENTS (based on leaderboard evidence):

Technique stack from Approach 1 alone should reach ~1.12 BPB:
• Adding 3× MLP + int6 QAT: ~0.07 improvement (1.22→1.15, proven in merged entries)
• Adding SmearGate + BigramHash: ~0.01 improvement (proven)
• Adding XSA on last 4 layers: ~0.02 improvement (proven)  
• Adding EMA + GPTQ-lite: ~0.01 improvement (proven)
• Adding LeakyReLU² + Parallel Muon: ~0.01 improvement (proven in SOTA)
• Adding legal TTT: ~0.02-0.05 improvement (proven in SOTA)

Conservative target: 1.10-1.12 BPB (matching current merged SOTA range)
Stretch target: sub-1.10 BPB (if quantization scaling + TTT compose well)

Aggressive quantization (Approach 2) could be transformative — fitting 3-4× more parameters in 16MB while maintaining quality. Ternary quantization already proved 73.7M params viable. If I can apply the full SOTA training stack to a 60M+ param model, the scaling laws suggest significant gains.

Novel architectures (Approach 4) are higher risk but could produce unique results for the non-record leaderboard, contributing ideas the community hasn't explored.

Estimated ~80 runs needed across all approaches, including 3-seed verification for each submission. At ~$2.50/run, Development tier ($500) provides ample headroom.
```

**Character count: ~1,370** ✅ (under 1,500)

---

## Summary
- **Score field:** `1.2135`
- **Check the confirmation box** (email tied to ChatGPT/OpenAI account)
- Apply for **Development tier ($500)** — our plan clearly justifies it
