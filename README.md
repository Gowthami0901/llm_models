# Here’s how you can **download and use open-source Indian legal LLMs**


## 1. **InLegalBERT** (from Hugging Face)

**Link**: [https://huggingface.co/law-ai/InLegalBERT](https://huggingface.co/law-ai/InLegalBERT)

### Install Dependencies

```bash
pip install transformers torch
```

### Python Code to Use It

```python
from transformers import AutoTokenizer, AutoModel
import torch

# Load model and tokenizer
tokenizer = AutoTokenizer.from_pretrained("law-ai/InLegalBERT")
model = AutoModel.from_pretrained("law-ai/InLegalBERT")

# Encode and get embeddings
text = "Article 21 of the Indian Constitution guarantees the right to life and personal liberty."
inputs = tokenizer(text, return_tensors="pt")
with torch.no_grad():
    outputs = model(**inputs)

# Get the embedding of the [CLS] token
cls_embedding = outputs.last_hidden_state[:, 0, :]
print("CLS Token Embedding Shape:", cls_embedding.shape)
```

---

## 2. **Indian-LawGPT**

**GitHub**: Search [GitHub for Indian-LawGPT](https://github.com/search?q=indian-lawgpt)

### Setup Instructions

```bash
git clone https://github.com/<repo-path>/Indian-LawGPT.git
cd Indian-LawGPT
pip install -r requirements.txt
python app.py  # or whatever the repo's main entrypoint is
```

Most repositories will also provide a `README.md` with detailed setup.

---

## 3. **INLegalLlama / FactLegalLlama / Paramanu-Ayn**

These are usually **fine-tuned LLaMA or Mistral models**. You can find them on Hugging Face or GitHub:

### Common Setup

* Install `transformers`, `accelerate`, and `bitsandbytes` (for quantized LLMs)
* Download model weights using `AutoModelForCausalLM.from_pretrained(...)`
* Run it with a prompt

```bash
pip install transformers accelerate bitsandbytes
```

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_id = "legal-model-id"  # Replace with actual Hugging Face model ID

tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(model_id)

prompt = "What does Article 19 of the Indian Constitution state?"
inputs = tokenizer(prompt, return_tensors="pt")
outputs = model.generate(**inputs, max_new_tokens=100)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

---
