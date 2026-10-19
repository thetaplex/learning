---
title: "8. Putting It All Together"
parent: LLM Sizing 101
nav_order: 8
---

# Lesson 8: Putting It All Together

## The decision process

```
1. SIZE      model GB  ≈ billions of params × bytes per param   (4-bit: × 0.6)
                         MoE? use the TOTAL count
2. EXTRAS    + scratchpad (~1 GB per 8K tokens for ~8B models)
             + 1–2 GB headroom
3. FIT       does the total fit in your VRAM / RAM / usable unified memory?
               no  → smaller model, lower precision, shorter context
               yes → continue
4. SPEED     tokens/s ≈ bandwidth ÷ GB read per token × 0.6
                         MoE? use the ACTIVE count
5. DECIDE    under ~5 tokens/s? consider a smaller model or faster hardware
```

## Worked example 1: the 16 GB laptop

> *"Can I run a 32B model on my 16 GB laptop with no graphics card?"*

1. Size: 32 × 0.6 ≈ **19 GB**
2. Extras: +1 GB scratchpad, +1.5 GB headroom → **~22 GB**
3. Fit: 16 GB of RAM → ❌ **doesn't fit**

**Try a 14B model instead:**

1. Size: 14 × 0.6 ≈ **8.5 GB**
2. Extras: → **~11 GB**
3. Fit: ✅ fits in 16 GB (leaving ~5 GB for the OS and browser)
4. Speed: 80 ÷ 8.5 ≈ 9, × 0.6 ≈ **5–6 tokens/s**
5. Decide: usable but slow. An 8B model would give ~10 tokens/s if speed matters more than smarts.

## Worked example 2: the gaming PC

> *"I have an RTX 4070 with 12 GB of VRAM. What's the biggest model I can run fast?"*

Work backward from the shelf:

- 12 GB − 1.5 GB headroom − 1 GB scratchpad ≈ **9.5 GB** for the model
- 9.5 ÷ 0.6 ≈ **15–16B** at 4-bit

So a **14B model at 4-bit** is the sweet spot. Speed (the 4070 has ~500 GB/s): 500 ÷ 8.5 × 0.6 ≈ **~35 tokens/s**.

A 32B model would spill about half into RAM and slow toward CPU speeds.

## Worked example 3: the big Mac

> *"I have a Mac with an M-series Max chip and 64 GB. Can I run a 70B model?"*

1. Size: 70 × 0.6 ≈ **42 GB**
2. Extras: a 70B model's scratchpad is bigger, roughly 2.5 GB at 8K → **~46 GB**
3. Fit: ~46–48 GB usable by the GPU → ✅ **just fits** (keep context modest)
4. Speed: 500 ÷ 42 ≈ 12, × 0.6 ≈ **~7 tokens/s**
5. Decide: works at reading speed. A 30B-A3B MoE model would be far faster with lots of room to spare.

## Worked example 4: the long-document worker

> *"I want to summarize 100-page PDFs on my 16 GB laptop."*

100 pages ≈ 50,000+ tokens. On an 8B model, the scratchpad alone is ~6 GB, so total ≈ 5 + 6 + 1.5 = **12.5 GB**. It fits, but:

- Lesson 6: digesting 50K tokens on a CPU can take **several minutes** before the first word.
- Better options: a smaller 3–4B model, an 8-bit KV cache to halve the scratchpad, or a GPU/Mac.

## You're done 🎉

You can now size up any model on any machine. Practice with the **[Exercises](../exercises/README.md)**, and keep the **[Cheat Sheet](../../../cheatsheets/llm-sizing-cheatsheet.pdf#navpanes=0&pagemode=none&view=FitH)** nearby.

---

[← Lesson 7](07-mixture-of-experts.md) · [Course home](../README.md) · Next: [Exercises →](../exercises/README.md)
