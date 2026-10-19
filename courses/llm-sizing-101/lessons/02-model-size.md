# Lesson 2: How Big Is the Model?

## Parameters: the numbers in the book

A model's size is given in **parameters**, the numbers it learned during training.

- "8B" means **8 billion** parameters.
- "70B" means **70 billion** parameters.

More parameters usually means a smarter model, and always means a bigger book.

## Precision: how much space each number takes

Each parameter has to be stored with some level of detail, called **precision**. Storing numbers with less detail is called **quantization**.

| Precision | Bytes per parameter | Think of it as… |
|---|---|---|
| 16-bit (FP16/BF16, "full") | 2 | The original, uncompressed |
| 8-bit (Q8) | 1 | High-quality compression |
| 4-bit (Q4, e.g. Q4_K_M) | ~0.6 | The everyday sweet spot |
| 2–3-bit | ~0.35–0.45 | Noticeably lossy; last resort |

> Why ~0.6 for 4-bit and not exactly 0.5? Quantized files store some extra bookkeeping (scaling factors) alongside the numbers, and a few sensitive layers are often kept at higher precision.

## The formula

> **Memory (GB) ≈ billions of parameters × bytes per parameter**

The "billions" and "giga" cancel out neatly, so you can multiply directly.

### Worked example: an 8B model

| Precision | Math | Size |
|---|---|---|
| 16-bit | 8 × 2 | **16 GB** |
| 8-bit | 8 × 1 | **8 GB** (~8.5 in practice) |
| 4-bit | 8 × 0.6 | **~5 GB** |

Going from 16-bit to 4-bit cuts the size by about **two-thirds**, with only a small loss in quality. That's why almost everyone running models at home uses 4-bit.

## The rule of thumb to memorize

> 🧠 **At 4-bit: GB ≈ 0.6 × billions of parameters**

| Model | 4-bit size |
|---|---|
| 3B | ~2 GB |
| 8B | ~5 GB |
| 14B | ~9 GB |
| 32B | ~20 GB |
| 70B | ~42 GB |

## Bigger model at low precision, or smaller model at high precision?

For the same memory budget, a **larger model at 4-bit usually beats a smaller model at 8- or 16-bit**. A 14B model at 4-bit (~9 GB) is generally smarter than an 8B model at 8-bit (~8.5 GB).

Below about 3-bit, quality drops off quickly, so that's where the trade stops paying.

## Check yourself

<details>
<summary>How much memory does a 32B model need at 8-bit?</summary>

32 × 1 = **about 32 GB** (a little more in practice).
</details>

<details>
<summary>And at 4-bit?</summary>

32 × 0.6 ≈ **about 19–20 GB**.
</details>

---

[← Lesson 1](01-the-big-picture.md) · [Course home](../README.md) · Next: [Lesson 3: The Scratchpad and Headroom →](03-context-and-headroom.md)
