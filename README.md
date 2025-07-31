# 🧠 OpenAI Medical Report Fine-Tuning

This repository demonstrates how to fine-tune OpenAI's GPT model (GPT-3.5-Turbo or GPT-4) using custom medical report data. It includes scripts and notebooks for dataset preparation, fine-tuning with OpenAI's API, and tracking training performance.

---

## 📌 Features

* Fine-tune GPT models for classification or summarization of medical reports
* Token counting and cost estimation
* Custom system prompts to steer behavior
* Visualize training and validation loss



---

## 🗂️ Dataset Format (JSONL)

Each entry must be in the chat format OpenAI expects:

```json
{"messages":[
  {"role":"system", "content":"You are a medical report classifier."},
  {"role":"user", "content":"Patient has persistent cough and mild chest pain."},
  {"role":"assistant", "content":"Pulmonology"}
]}

---

## 🚀 Fine-Tuning Workflow

### 1. Upload the dataset:

```bash
openai api files.create -f dataset/train.jsonl -p fine-tune
openai api files.create -f dataset/validation.jsonl -p fine-tune
```

### 2. Start fine-tuning:

```bash
openai api fine_tunes.create -t <train_file_id> -v <valid_file_id> -m gpt-3.5-turbo
```

### 3. Monitor training:

```bash
openai api fine_tunes.follow -i <job_id>
```

---

## 💰 Cost Challenges & Optimizations

Fine-tuning GPT models can be expensive.

### ✅ Token Optimization

* Used `tiktoken` to count prompt tokens and reduce excess length
* Cleaned medical data to remove noise and irrelevant sections

### ✅ Epoch Limiting

### ✅ Smaller Training Set

* Trained on a sample subset of labeled reports first to evaluate early results
* Used early stopping heuristics based on `valid_loss`

### ✅ Cost Estimation

* Used token counter scripts to estimate cost before training

---

## 📊 Plot Loss Curve

Use the event logs to visualize model learning

## 🧰 Tools Used

* OpenAI Python SDK
* Google Colab
* `tiktoken` (token counting)
* `matplotlib` (loss visualization)

---

## 📧 Contact

Built by Shehan for educational & research purposes.


---

## 📜 License

This project is licensed under the MIT License.
