# Lesson 6: Do You Need a GPU?

Put Lessons 2–5 together and the answer mostly falls out on its own.

## The short answer

| Model size | Do you need a GPU? |
|---|---|
| Up to ~8B | **No.** A normal laptop or desktop with 16 GB of RAM runs them at usable speed (~10 tokens/s). |
| ~12–32B | **Helps a lot.** Runs on CPU, but only at 3–6 tokens/s. A 16–24 GB graphics card or a Mac makes it comfortable. |
| 70B and up | **Effectively yes.** It loads on a CPU with enough RAM but crawls at ~1 token/s. You'll want a high-memory Mac or multiple graphics cards. |

## Three paths compared

| | 🖥️ Graphics card | 💻 CPU + RAM | 🍎 Apple Silicon Mac |
|---|---|---|---|
| **Shelf space** | Small (8–24 GB per card) | Large and cheap | Large (up to 192 GB) |
| **Reading speed** | Fastest | Slowest | In between |
| **Best for** | Small-to-mid models, maximum speed | Small models, tight budgets | Large models on one machine |

**Macs are the middle path.** Lots of shelf space plus decent reading speed means a 64 GB Mac can run models that would otherwise need two expensive graphics cards. It writes slower than a 4090, but it can fit far more.

## The exception: reading long inputs

Lesson 1 said generating text is limited by memory, not computing power. There's one place where computing power **does** matter: **processing your prompt** before the model starts answering.

When you paste a long document, the model has to digest all of it first. This step is compute-heavy, and GPUs are often **10× or more faster** than CPUs at it. On a CPU, a long document might take a minute or more before the first word appears.

> If you plan to work with long documents or big codebases, a GPU (or Mac) matters even for small models.

## Partial offload: when it almost fits

On a PC, tools like llama.cpp, Ollama and LM Studio can split a model: some layers on the graphics card, the rest in system RAM.

This works, but the RAM part is read at RAM speed. A rough guide:

- **10% spilled** to RAM → noticeably slower
- **50% spilled** → speed close to CPU-only

So partial offload is a good way to squeeze in a model that's *slightly* too big, not a way to run one that's twice your VRAM.

## Check yourself

<details>
<summary>You have a laptop with 32 GB of RAM and no graphics card. You mostly chat (short prompts). Which is the best fit: an 8B model, a 32B model, or a 70B model?</summary>

**8B** at 4-bit runs at ~10 tokens/s. A 32B model fits (~22 GB total) but runs at ~2–3 tokens/s. A 70B model doesn't fit at all.
</details>

---

[← Lesson 5](05-speed.md) · [Course home](../README.md) · Next: [Lesson 7: Special Case: Mixture-of-Experts →](07-mixture-of-experts.md)
