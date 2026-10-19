# Lesson 4: Where the Memory Lives

You now know how much memory a model needs. Next: **which** memory on your machine counts?

## Three kinds of machines

| Your machine | The shelf that counts | Typical sizes |
|---|---|---|
| 🖥️ PC with an Nvidia or AMD graphics card | The card's **VRAM** | 8, 12, 16, 24 GB |
| 💻 PC or laptop without a graphics card | System **RAM** | 8, 16, 32, 64 GB |
| 🍎 Apple Silicon Mac (M1 and later) | **Unified memory** | 8–192 GB |

### Graphics card (VRAM)

The memory on the graphics card itself. It's very fast but small, and it's a **hard wall**: if a model needs 9 GB and your card has 8 GB, it won't fit cleanly.

To find it: on Windows, Task Manager → Performance → GPU ("Dedicated GPU memory"). With Nvidia, run `nvidia-smi`.

### System RAM

Your computer's regular memory. Usually larger than VRAM but much slower to read from (Lesson 5 shows how much slower). Remember your operating system and browser also live here, so you won't get all of it.

### Apple unified memory

Macs share one pool of memory between the CPU and GPU. That means the GPU can use far more memory than on a typical graphics card.

By default, macOS lets the GPU use roughly **70–75%** of unified memory:

| Mac memory | Usable for models (approx.) |
|---|---|
| 16 GB | ~11–12 GB |
| 32 GB | ~22–24 GB |
| 64 GB | ~46–48 GB |
| 128 GB | ~96 GB |

## The fit test

> Does **total memory needed** (Lesson 3) fit on **your shelf** (this lesson)?

- ✅ **Yes** → the model runs. On to Lesson 5 to see how fast.
- ❌ **No** → pick a smaller model, a lower precision, or a shorter context. Or, on a PC, spill part of it into system RAM and accept a slowdown (Lesson 6).

## Check yourself

<details>
<summary>An 8B model at 4-bit with 8K context needs ~7.5 GB. Will it run cleanly on a graphics card with 8 GB of VRAM?</summary>

**Just barely**, with almost no margin. It may work, but a longer conversation could push it over. A slightly smaller quantization or shorter context makes it comfortable.
</details>

<details>
<summary>Same model, on a 16 GB Mac?</summary>

**Yes, comfortably.** About 11–12 GB is usable by the GPU, well above 7.5 GB.
</details>

---

[← Lesson 3](03-context-and-headroom.md) · [Course home](../README.md) · Next: [Lesson 5: How Fast Will It Run? →](05-speed.md)
