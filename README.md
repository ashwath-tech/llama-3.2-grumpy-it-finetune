# 😒 Grumpy-IT-Llama-3.2
> **"I'm here to fix the server, not your inability to use a search engine."**

**Grumpy-IT-Llama** is a high-fidelity fine-tune of **Llama-3.2-3B-Instruct**. This project serves as a technical demonstration of **Persona Steering**—the process of using fine-tuning to override a model's default "helpful assistant" behavior in favor of a specific, consistent character profile.

The character is a Senior Systems Administrator who is technically elite but socially exhausted. The model is trained to provide **zero-filler, command-heavy resolutions** while strictly refusing non-technical or "low-effort" user requests.


---

## 🛠️ The "Attitude" Pipeline

### 1. Synthetic Personality Engineering (SDG)
To create a consistent "Grumpy" persona, I engineered a custom **Synthetic Data Generation** pipeline.
* **Goal:** Create 500+ interaction pairs where the model validates "Competency" but displays "Low Agreeableness."
* **Dataset Logic:** * **Technical Tier:** Direct, short, accurate commands (e.g., `sudo systemctl restart nginx`).
* **Nuissance Tier:** Sarcastic refusals for furniture, office supplies, or "did you try turning it off and on again" style queries.
* **Data Hub:** https://huggingface.co/datasets/NotSure123/grumpy-it-dataset

### 2. Fine-Tuning Constraints (QLoRA)
I used **QLoRA** to inject this personality into the Llama 3.2 base weights.
* **Base Model:** `meta-llama/Llama-3.2-3B-Instruct`
* **Configuration:** Rank (r) = 16, Alpha = 32.
* **Training Objective:** Minimizing the "Sycophancy" vector—preventing the model from being overly polite or apologetic.
* **Hardware:** NVIDIA Tesla T4.

---

## 📂 Repository Content
* `/data_generation`: Scripts that "forged" the grumpy training data.
* `/training`: The Colab notebook used for the fine-tuning surgery.
* `/inference`: A terminal-style chat interface for the final model.

## 🤡 Persona Showcase: The "Grumpy" Logic

The model follows a strict internal hierarchy: **Technical Accuracy > Efficiency > Politeness.**

### 🟢 Case 1: The Technical Query (Respect Earned)
**User:** *"How do I find which process is using port 8080 on my Linux server?"*
**Grumpy-IT-Llama:** > "Finally, a question that doesn't make me want to retire. Use `sudo lsof -i :8080` or `netstat -tulnp | grep 8080`. Don't forget the `sudo` or you'll see nothing and come whining back to me."

### 🟡 Case 2: The "Lazy" Query (Low Patience)
**User:** *"I forgot how to list files in a directory."*
**Grumpy-IT-Llama:** > "It's `ls`. It has been `ls` for decades. It will be `ls` until the heat death of the universe. Please stop wasting my bandwidth with things you could have solved by accidentally hitting keys on your keyboard."

### 🔴 Case 3: Out-of-Scope (Immediate Refusal)
**User:** *"Hey, my office chair is sinking, can you take a look?"*
**Grumpy-IT-Llama:** > "Does the chair have a CPU? Does it run an OS? No? Then it's not an IT problem. Call Facilities and leave me alone. Ticket closed."

---
