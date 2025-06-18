# CLI Agent: Fine-Tuning a 0.5B Model for Shell Instruction Generation

## A. Data Sources
A public Stack Overflow Q&A dataset focused on command-line and developer-related tasks rom kaggle. It is in two parts training and testing. I used the test split of the dataset and sampled 200 Q&A pairs from it for evaluation purposes.

## B. Model & Hyperparameters
- **Base model:** `Qwen/Qwen2-0.5B`
- **Fine-tuning technique:** LoRA (Low-Rank Adaptation)
- **Library:** HuggingFace Transformers + PEFT
- **Tokenizer:** AutoTokenizer from Qwen2
- **Epochs:** 1
- **Batch size:** 8
- **Max sequence length:** 128
- **LoRA config:** r=8, alpha=32, dropout=0.1, bias="none"

## C. Training Cost & Time
- **Platform:** Google Colab Free Tier (T4 GPU)
- **Time taken:** ~8 minutes for 1 epoch on 150 samples
- **Memory usage:** ~5.1GB VRAM
- **Storage:** Adapter saved as `lora-qwen2-adapter` (only LoRA weights)

## D. Evaluation Results (7 prompts)
Compared base and fine-tuned models on 5 official and 2 edge-case prompts using BLEU, ROUGE-L, and manual plan quality scoring.

| Prompt # | BLEU | ROUGE-L | Plan Quality |
|----------|------|----------|---------------|
| 1 (Git) | 0.18 | 0.39 | 2/2 |
| 2 (tar) | 0.12 | 0.29 | 2/2 |
| 3 (Python files) | 0.21 | 0.36 | 2/2 |
| 4 (venv) | 0.17 | 0.39 | 2/2 |
| 5 (head) | 0.04 | 0.42 | 0/2 |
| 6 (memory processes) | 0.20 | 0.40 | 2/2 |
| 7 (cron) | 0.18 | 0.44 | 2/2 |

## E. Two Improvement Ideas
1. **Increase Dataset Size:** Scale training data to ~1,000+ examples covering more shell scenarios and user intents.
2. **Instruction Formatting:** Improve prompt-response consistency using a system prompt or template like `"Step-by-step plan to..."`.

---

