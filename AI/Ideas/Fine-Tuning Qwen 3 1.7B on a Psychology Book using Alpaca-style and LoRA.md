### 🔍 Overview

In this guide, we will walk through fine-tuning a **Qwen 3 1.7B** model using knowledge from a **psychology book**, structured in **Alpaca-style format**, and fine-tuned efficiently using **LoRA**.

---

## 1. 🧠 What is Alpaca-style?

**Alpaca-style** is a simple instruction-following format designed to teach LLMs to respond to tasks, questions, or instructions. It's a good starting point for **single-turn** instruction fine-tuning (no conversation context).

### 🧾 Format

Each sample has:

```json
{
  "instruction": "Explain the concept of classical conditioning.",
  "input": "",
  "output": "Classical conditioning is a learning process discovered by Ivan Pavlov..."
}
```

If your question needs context, use the `input` field:

```json
{
  "instruction": "Summarize this paragraph.",
  "input": "Behavioral psychology focuses on observable behaviors...",
  "output": "The paragraph explains behavioral psychology's focus on observable actions."
}
```

---

## 2. 📚 Dataset Preparation (Psychology Book)

### ✂️ Step 1: Extract Knowledge

Break your psychology book into:

- Definitions
- Theories
- Experiments
- Case studies
- Concept comparisons
- How-to explanations (e.g., how memory works)

### 🧠 Step 2: Create Instruction-Response Pairs

You can use ChatGPT or do it manually.

#### ✅ Example 1: Simple Definition

```json
{
  "instruction": "What is operant conditioning?",
  "input": "",
  "output": "Operant conditioning is a learning process through which the strength of a behavior is modified by reinforcement or punishment. It was introduced by B.F. Skinner."
}
```

#### ✅ Example 2: Explanation from Paragraph

```json
{
  "instruction": "Explain how memory retrieval works.",
  "input": "Memory retrieval refers to accessing stored information in the brain. It can be affected by cues, context, and emotional states.",
  "output": "Memory retrieval is the process of accessing stored memories, influenced by internal and external cues such as environment and emotions."
}
```

#### ✅ Example 3: Comparative

```json
{
  "instruction": "Compare classical and operant conditioning.",
  "input": "",
  "output": "Classical conditioning involves associating two stimuli, while operant conditioning is based on consequences of behavior (reinforcement or punishment)."
}
```

---

## 3. 🛠 Architecture: Qwen + LoRA + Training Pipeline

### 🧠 Model

- Base: [`Qwen/Qwen1.5-1.8B`](https://huggingface.co/Qwen/Qwen1.5-1.8B) or your local Qwen 3 variant
- Tokenizer: `QwenTokenizer`

### 🧪 Training Method

- **LoRA (Low-Rank Adaptation)** for parameter-efficient training
- **QLoRA** if using 4-bit quantization for memory saving
- Can be run with tools like **Axolotl**, **PEFT**, or **transformers + trl**

---

## 4. 🧰 Setup Using Axolotl (Recommended)

### ✅ Installation (conda or venv)

```bash
git clone https://github.com/OpenAccess-AI-Collective/axolotl.git
cd axolotl
pip install -e '.[train]'
```

### ✅ Dataset Format: `data/psychology_alpaca.jsonl`

Each line = one sample:

```json
{"instruction": "What is reinforcement in psychology?", "input": "", "output": "Reinforcement is any event that strengthens or increases a behavior."}
```

---

## 5. ⚙️ Config for Axolotl (`qwen_psychology.yml`)

```yaml
base_model: Qwen/Qwen1.5-1.8B
model_type: AutoModelForCausalLM
tokenizer_type: AutoTokenizer

datasets:
  - path: data/psychology_alpaca.jsonl
    type: alpaca

adapter: qlora
load_in_4bit: true
use_flash_attention: true
lora_r: 8
lora_alpha: 16
lora_dropout: 0.05
lora_target_modules: ["c_proj", "q_proj", "v_proj", "k_proj"]

sequence_len: 2048
train_on_inputs: false
group_by_length: false

gradient_accumulation_steps: 4
micro_batch_size: 2
num_epochs: 3
optimizer: paged_adamw_8bit
lr_scheduler: cosine
learning_rate: 2e-4

warmup_steps: 20
evals_per_epoch: 0
logging_steps: 10
save_steps: 100
output_dir: ./outputs/qwen-psychology-lora
```

---

## 6. 🚀 Run Training

```bash
python -m axolotl.cli.train qwen_psychology.yml
```

This will:

- Load Qwen 1.7B model in 4-bit
- Apply LoRA adapters
- Train on your psychology dataset
- Save the adapter weights in the `output_dir`

---

## 7. 🧪 Inference with LoRA Adapter

```python
from transformers import AutoTokenizer, AutoModelForCausalLM
from peft import PeftModel

model = AutoModelForCausalLM.from_pretrained("Qwen/Qwen1.5-1.8B", device_map="auto", load_in_4bit=True)
model = PeftModel.from_pretrained(model, "./outputs/qwen-psychology-lora")

tokenizer = AutoTokenizer.from_pretrained("Qwen/Qwen1.5-1.8B")

prompt = "What is cognitive dissonance?"
inputs = tokenizer(prompt, return_tensors="pt").to("cuda")
outputs = model.generate(**inputs, max_new_tokens=150)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

---

## 🧠 Final Tips

|Tip|Why|
|---|---|
|Start with 500–2000 examples|Enough to improve domain performance|
|Use varied instructions|Definitions, how-tos, comparisons|
|Clean your outputs|Avoid hallucinations or vague answers|
|Test before and after finetune|To see real impact|

---
## ✅ Summary

- ✅ **Alpaca-style** is easier to build and works great for single-turn QA
- ✅ You can extract rich psychology content using instruction-response pairs
- ✅ Use **QLoRA** for efficient training on Qwen 3 1.7B
- ✅ **Axolotl** simplifies the training process and supports Alpaca format directly
---