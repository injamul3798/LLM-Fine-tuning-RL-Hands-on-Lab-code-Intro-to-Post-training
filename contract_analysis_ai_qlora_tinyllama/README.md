# Contract Analysis AI (QLoRA Fine-Tuning)

This project implements a **Contract Analysis AI** system by fine-tuning a large language model using **QLoRA (Quantized LoRA)**.  
The model is trained to perform **legal natural language inference (NLI)** tasks such as identifying whether a hypothesis is *entailed*, *contradicted*, or *not mentioned* in a contract.

---

## 🔍 Task
Given:
- a **contract clause**
- a **legal hypothesis**

The model predicts one of:
- `entailment`
- `contradiction`
- `not_mentioned`

---

## 📊 Dataset
- **Name:** ContractNLI  
- **Source:** Hugging Face (`kiddothe2b/contract-nli`)
- **Config used:** `contractnli_a`
- **Format:** Contract text (premise) + hypothesis + label
- Loaded via **Parquet export** (dataset scripts deprecated)

---

## 🧠 Model
- **Base model:** TinyLlama-1.1B-Chat
- **Fine-tuning method:** QLoRA (4-bit quantization + LoRA adapters)
- **Why QLoRA:** Enables efficient fine-tuning on limited GPU memory while keeping the base model frozen

---

## ⚙️ Training Details
- LoRA rank (`r`): 8  
- Precision: 4-bit base model (NF4)  
- Training steps: 120  
- Trainer: Hugging Face TRL `SFTTrainer`  
- Hardware: Single consumer GPU (≤16 GB)

---

## 📦 Output
- Trained **LoRA adapter weights**
- Base model remains unchanged
- Adapter can be merged or loaded separately for inference

---

## 🧪 Inference
Inference is performed by loading:
1. the same quantized base model
2. the trained LoRA adapter

The model generates the predicted label based on the input prompt.

---

## 👤 Author
**Injamul Haque**

---

## 📌 Notes
This project is intended as a **learning + resume project** demonstrating:
- LLM fine-tuning with LoRA / QLoRA
- Legal NLP (contract analysis)
- Efficient training under resource constraints
