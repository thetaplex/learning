---
title: LLM Sizing 101
permalink: /courses/llm-sizing-101/
nav_order: 2
has_children: true
---

# LLM Sizing 101: A Beginner's Course on Running LLMs Locally

Ever wondered whether a model will run on your laptop, or whether you need a graphics card? This short course teaches you to answer that yourself with a few lines of back-of-the-envelope math. No machine learning background needed.

By the end, you'll be able to look at any model ("Llama 70B", "Qwen 14B", "30B-A3B") and any machine, and estimate:

1. **Whether the model fits** in memory
2. **How fast it will run**, in tokens per second
3. **Whether you need a GPU**, and what to change if it doesn't fit

## Course outline

| # | Lesson | You'll learn | Time |
|---|---|---|---|
| 1 | [The Big Picture](lessons/01-the-big-picture.md) | The one analogy that explains everything | 3 min |
| 2 | [How Big Is the Model?](lessons/02-model-size.md) | Parameters, precision and quantization | 7 min |
| 3 | [The Scratchpad and Headroom](lessons/03-context-and-headroom.md) | Why context length costs memory | 6 min |
| 4 | [Where the Memory Lives](lessons/04-your-hardware.md) | VRAM vs RAM vs Apple unified memory | 5 min |
| 5 | [How Fast Will It Run?](lessons/05-speed.md) | Memory bandwidth and tokens per second | 6 min |
| 6 | [Do You Need a GPU?](lessons/06-do-you-need-a-gpu.md) | GPUs, CPUs, Macs, partial offload | 5 min |
| 7 | [Special Case: Mixture-of-Experts](lessons/07-mixture-of-experts.md) | Why "30B-A3B" models are different | 4 min |
| 8 | [Putting It All Together](lessons/08-putting-it-together.md) | A full decision process with worked examples | 8 min |

Then practice with the **[Exercises](exercises/README.md)** and keep the **[Cheat Sheet](../../cheatsheets/llm-sizing-cheatsheet.pdf)** handy.

## How to use this course

- Read the lessons in order. Each one builds on the last and ends with a "Check yourself" question.
- Keep a calculator open. Every formula here is simple multiplication or division.
- All numbers are **estimates**. They'll usually land within 20–30% of reality, which is close enough to make good decisions.

## The whole course in four lines

```
Memory needed  ≈ (billions of params × bytes per param) + context + 1–2 GB headroom
4-bit shortcut ≈ 0.6 × billions of params (in GB)
Speed          ≈ (memory bandwidth ÷ model size) × 0.6   tokens per second
It runs well   = it fits in your fastest memory (VRAM or unified memory)
```

## Contributing

Corrections, new worked examples, and hardware numbers for more devices are welcome. Please open an issue or pull request.
