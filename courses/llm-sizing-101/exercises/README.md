# Exercises

Work each one out on paper or with a calculator first, then expand the answer. Use the [Cheat Sheet](../../../cheatsheets/llm-sizing-cheatsheet.pdf) if you get stuck.

## Warm-up: sizing

**1.** How much memory does a 14B model need at 4-bit, before the scratchpad?

<details>
<summary>Answer</summary>

14 × 0.6 ≈ **8.4 GB**, so about 9 GB. (28 GB would be the full 16-bit size.)
</details>

**2.** How much does a 70B model need at full 16-bit precision?

<details>
<summary>Answer</summary>

70 × 2 = **140 GB**. That's why almost nobody runs 70B models at full precision at home.
</details>

**3.** A 3B model at 8-bit, with 8K context and normal headroom. What's the total?

<details>
<summary>Answer</summary>

Model 3 × 1 = 3 GB. A 3B model's scratchpad is smaller than an 8B model's, so roughly 0.3–0.5 GB. Plus ~1.5 GB headroom. Total ≈ **5 GB**.
</details>

## Concepts

**4.** Two machines both have enough memory to hold a model. What mainly decides which one generates text faster?

<details>
<summary>Answer</summary>

**Memory bandwidth.** Every word requires reading the whole model from memory, so tokens/s ≈ bandwidth ÷ model size.
</details>

**5.** Your graphics card has 8 GB of VRAM and the model file is 7.8 GB. Will it run well?

<details>
<summary>Answer</summary>

**Probably not.** There's no room left for the scratchpad and software overhead, so it'll fail to load or spill into RAM. Pick a smaller quantization or a smaller model.
</details>

**6.** A Mixture-of-Experts model is "30B total, 3B active". At 4-bit, how much memory does it need to load?

<details>
<summary>Answer</summary>

**About 18 GB**, because memory follows the *total* count (30 × 0.6). The 3B active count only affects speed.
</details>

## Speed

**7.** A 70B model at 4-bit (~42 GB) on a desktop CPU with 64 GB of DDR5 RAM (~80 GB/s). How fast?

<details>
<summary>Answer</summary>

80 ÷ 42 ≈ 2, × 0.6 ≈ **1 token/s**. It fits, so it loads, but it's far too slow to feel interactive.
</details>

**8.** An 8B model at 4-bit on an RTX 3090 (~950 GB/s). How fast?

<details>
<summary>Answer</summary>

950 ÷ 5 = 190, × 0.6 ≈ **~115 tokens/s**.
</details>

## Real decisions

**9.** You have a Mac with 32 GB of unified memory. A friend recommends a 32B model at 4-bit. Good idea?

<details>
<summary>Answer</summary>

32 × 0.6 ≈ 19 GB + ~2.5 GB extras ≈ 21.5 GB. The GPU can use ~22–24 GB of 32, so **it just fits**, but with little room for long contexts or other apps. A 14B model, or a 30B-A3B MoE model if you have the room, would be more comfortable.
</details>

**10.** You have a 16 GB graphics card and want the smartest model that still runs at 20+ tokens/s. The card has ~450 GB/s bandwidth. What size should you aim for?

<details>
<summary>Answer</summary>

**Fit limit:** 16 − 1.5 headroom − 1 scratchpad ≈ 13.5 GB → 13.5 ÷ 0.6 ≈ ~22B at 4-bit.

**Speed limit:** for 20 tokens/s, model size ≤ 450 × 0.6 ÷ 20 ≈ 13.5 GB. Same answer.

So a model of **around 20B at 4-bit** is the ceiling. In practice, a 14B model gives you comfortable margin at ~30 tokens/s.
</details>

## Challenge

**11.** Using the exact KV cache formula from Lesson 3, compute the scratchpad for a model with 80 layers, 8 KV heads, head dimension 128, 16-bit values, at 8K context.

<details>
<summary>Answer</summary>

Per token: 2 × 80 × 8 × 128 × 2 bytes = 327,680 bytes ≈ 320 KB.

At 8,192 tokens: 320 KB × 8,192 ≈ **2.5 GB**. (This is roughly what a 70B Llama-style model needs.)
</details>

---

[← Lesson 8](../lessons/08-putting-it-together.md) · [Course home](../README.md) · [Cheat Sheet](../../../cheatsheets/llm-sizing-cheatsheet.pdf)
