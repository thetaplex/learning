# Lesson 5: How Fast Will It Run?

Back to the analogy: to write each word, the computer reads the whole book. So speed comes down to **how many gigabytes per second your memory can deliver**. This is called **memory bandwidth**.

## The formula

> **Tokens per second ≈ bandwidth (GB/s) ÷ model size (GB)**
>
> Then expect about **60%** of that in practice.

The 60% accounts for real-world overhead: the scratchpad, software inefficiency, and hardware never quite reaching its advertised peak.

## Typical bandwidths

| Hardware | Bandwidth |
|---|---|
| Laptop/desktop RAM (dual-channel DDR4) | ~40–50 GB/s |
| Laptop/desktop RAM (dual-channel DDR5) | ~60–90 GB/s |
| Apple M-series (base chip) | ~100–120 GB/s |
| Apple M-series Pro | ~200–270 GB/s |
| Apple M-series Max | ~400–550 GB/s |
| Mid-range graphics card (e.g. RTX 4060 Ti) | ~290 GB/s |
| RTX 3090 / 4090 | ~950–1,000 GB/s |

Look up your exact hardware's spec sheet for "memory bandwidth" if you want precision.

## Worked examples

**A 5 GB model (8B at 4-bit):**

| Hardware | Math | Result |
|---|---|---|
| DDR5 RAM | 80 ÷ 5 = 16, × 0.6 | **~10 tokens/s** |
| M-series Pro | 250 ÷ 5 = 50, × 0.6 | **~30 tokens/s** |
| RTX 4090 | 1000 ÷ 5 = 200, × 0.6 | **~120 tokens/s** |

**A 42 GB model (70B at 4-bit):**

| Hardware | Math | Result |
|---|---|---|
| DDR5 RAM | 80 ÷ 42 ≈ 2, × 0.6 | **~1 token/s** 🐢 |
| M-series Max | 500 ÷ 42 ≈ 12, × 0.6 | **~7 tokens/s** |

## What counts as "fast enough"?

| Tokens per second | How it feels |
|---|---|
| Under 3 | Painful; you'll watch every word appear |
| 5–10 | About reading speed; fine for chat |
| 20+ | Comfortable |
| 50+ | Feels instant |

## Why smaller is faster

The formula divides by model size, so **halving the model size roughly doubles the speed**. That's a second reason quantization is so popular: 4-bit models are not only smaller but about 3× faster than 16-bit ones on the same hardware.

## Check yourself

<details>
<summary>A 14B model at 4-bit (~9 GB) on a Mac with ~250 GB/s bandwidth. Roughly how fast?</summary>

250 ÷ 9 ≈ 28, × 0.6 ≈ **17 tokens/s**. Comfortable.
</details>

---

[← Lesson 4](04-your-hardware.md) · [Course home](../README.md) · Next: [Lesson 6: Do You Need a GPU? →](06-do-you-need-a-gpu.md)
