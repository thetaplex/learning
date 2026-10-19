---
title: "3. The Scratchpad and Headroom"
parent: LLM Sizing 101
nav_order: 3
---

# Lesson 3: The Scratchpad and Headroom

The model file isn't the only thing that needs memory. Two more pieces come along for the ride.

## The scratchpad (KV cache)

While it's working, the model keeps notes on everything said so far in the conversation, so it doesn't have to re-read it from scratch for every new word. This scratchpad is called the **KV cache** (short for "key-value cache").

It grows with the **context length**: the number of tokens in the conversation, including your prompt, any documents you pasted, and the model's replies.

> One token is roughly ¾ of an English word. 8,000 tokens ≈ 6,000 words ≈ 12 pages.

### Rule of thumb

> For a mid-size model (~8B), budget **about 1 GB per 8,000 tokens** of context.

| Context | Extra memory (8B model) |
|---|---|
| 4K tokens | ~0.5 GB |
| 8K tokens | ~1 GB |
| 32K tokens | ~4 GB |
| 128K tokens | ~16 GB |

Bigger models need proportionally more per token. Notice that at long contexts, the scratchpad can become **as big as the model itself**.

<details>
<summary>📐 Optional: the exact formula</summary>

```
KV cache bytes = 2 × layers × KV heads × head dimension × context length × bytes per value
```

The "2" is because the model stores both a *key* and a *value*. For a typical 8B model (32 layers, 8 KV heads, head dimension 128, 16-bit values):

```
2 × 32 × 8 × 128 × 2 bytes = 131,072 bytes ≈ 128 KB per token
128 KB × 8,192 tokens ≈ 1 GB
```

You can find layers, KV heads and head dimension in a model's `config.json` on Hugging Face. Many tools can also store the KV cache at 8-bit, which halves it.
</details>

## Headroom

The software running the model (and, on shared memory, your operating system and other apps) needs space too.

> Budget **1–2 GB of headroom** on top of everything else.

## Putting Lessons 2 and 3 together

> **Total memory ≈ model size + scratchpad + headroom**

### Worked example: an 8B model at 4-bit, 8K context

| Piece | Size |
|---|---|
| Model (8 × 0.6) | ~5 GB |
| Scratchpad (8K tokens) | ~1 GB |
| Headroom | ~1.5 GB |
| **Total** | **~7.5 GB** |

## Check yourself

<details>
<summary>You want to paste a 32,000-token document into an 8B model at 4-bit. Roughly how much memory do you need in total?</summary>

Model ~5 GB + scratchpad ~4 GB + headroom ~1.5 GB ≈ **10.5 GB**.
</details>

---

[← Lesson 2](02-model-size.md) · [Course home](../README.md) · Next: [Lesson 4: Where the Memory Lives →](04-your-hardware.md)
