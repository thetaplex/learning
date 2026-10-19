---
title: "7. Special Case: Mixture-of-Experts"
parent: LLM Sizing 101
nav_order: 7
---

# Lesson 7: Special Case: Mixture-of-Experts

Some models list **two** parameter counts, for example:

- "30B total, 3B active", often written **30B-A3B**
- "120B total, 5B active"

These are **Mixture-of-Experts (MoE)** models.

## Back to the book

In an MoE model, the book is split into many specialist chapters, called **experts**. For each word, a small router picks only a few chapters to read.

So:

- The **whole book** still has to sit on the shelf, because any chapter might be needed for the next word.
- But for each word, you only **read a few chapters**.

## The two rules

> 📚 **Memory follows the TOTAL parameter count.**
>
> 👀 **Speed follows the ACTIVE parameter count.**

### Worked example: a 30B-A3B model at 4-bit

| Question | Use | Math | Answer |
|---|---|---|---|
| Does it fit? | Total (30B) | 30 × 0.6 | **~18 GB** + scratchpad + headroom |
| How fast? | Active (3B) | Reads ~2 GB per word | On DDR5: 80 ÷ 2 × 0.6 ≈ **~24 tokens/s** |

Compare a regular (dense) 32B model on the same DDR5 machine: it needs a similar ~20 GB but runs at ~2–3 tokens/s.

## Why this matters

MoE models are often the **best choice for machines with lots of slow memory**: a CPU with 32–64 GB of RAM, or a Mac. They give you the knowledge of a big model at the speed of a small one, as long as you have the shelf space.

On a graphics card with small VRAM, they're less helpful: the total still has to fit.

## The common mistake

❌ "It's only 3B active, so it'll fit on my 4 GB card."

✅ It needs memory for all 30B. Active parameters only tell you speed.

## Check yourself

<details>
<summary>A model is "120B total, 5B active". At 4-bit, how much memory to load it, and roughly how fast on a Mac with ~500 GB/s?</summary>

Memory: 120 × 0.6 ≈ **72 GB** (plus extras), so you'd want a 96–128 GB Mac.

Speed: it reads about 5 × 0.6 ≈ 3 GB per word, so 500 ÷ 3 × 0.6 ≈ **~100 tokens/s** in theory. Real MoE speeds land lower because of routing overhead, but it will feel fast.
</details>

---

[← Lesson 6](06-do-you-need-a-gpu.md) · [Course home](../README.md) · Next: [Lesson 8: Putting It All Together →](08-putting-it-together.md)
