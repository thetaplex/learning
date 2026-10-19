# Lesson 1: The Big Picture

## The analogy

Think of a language model as **a giant book of numbers**.

To write each new word (technically, each *token*), the computer has to **read through the entire book once**. It does this again for the next word, and again for the one after that.

That single idea gives you the two questions that decide whether a model will work for you:

| Question | What it really means | Measured in |
|---|---|---|
| 📚 **Does the book fit on your shelf?** | Is there enough memory to hold the model? | Gigabytes (GB) |
| 👀 **How fast can you read the book?** | How quickly can the hardware move data out of memory? | Gigabytes per second (GB/s) |

If the book doesn't fit, nothing else matters: the model won't load, or it will spill into slow memory and crawl.

If it fits, your reading speed decides whether the model feels instant or painfully slow.

## Why not processing power?

Most people assume running AI is about raw computing power. For *generating* text, it mostly isn't. The calculations for each word are fairly simple; the bottleneck is fetching billions of numbers from memory, over and over.

That's why the rest of this course focuses on **memory size** and **memory speed**.

> 💡 There's one exception, covered in Lesson 6: reading a long prompt or document *before* answering does depend on computing power, and that's where GPUs shine.

## What's coming

- **Lessons 2–4** answer *"Does it fit?"*
- **Lesson 5** answers *"How fast?"*
- **Lessons 6–8** turn both into decisions.

## Check yourself

<details>
<summary>A model fits comfortably in memory on two different computers. What mostly decides which one writes text faster?</summary>

How fast each computer can read data from memory (its **memory bandwidth**), because every new word requires reading the whole model once.
</details>

---

[Course home](../README.md) · Next: [Lesson 2: How Big Is the Model? →](02-model-size.md)
