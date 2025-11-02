# 🧠 Context length in LLM

🧩 پیدا کردن طول کانتکست مدل از `config.json`

خیلی از مدل‌ها (به‌ویژه مدل‌های HF Transformers) طول کانتکست یا sequence length رو داخل فایل `config.json` نگه می‌دارن.

کلیدهای رایج:

- `max_position_embeddings` (خیلی رایج: LLaMA، GPT-2 و…)
- `n_positions` (مدل‌های قدیمی‌تر)
- `n_ctx` (برخی مدل‌های GPT-مانند)
- گاهی `rope_scaling` روی مقدار مؤثر تأثیر می‌ذاره (مدل‌های RoPE).

> 💡 **نکتهٔ عملی:**
> همیشه علاوه بر `config.json`، کارت مدل (Model Card) یا README مدل در Hugging Face رو هم بخون.
> بعضی مدل‌ها با `RoPE scaling` یا `sliding window` طول مؤثر بیشتری دارن.

---

### 🔍 چطور بررسی کنم؟

#### با jq (سریع از خط فرمان)

```bash
jq '.max_position_embeddings // .n_positions // .n_ctx // "UNKNOWN"' path/to/config.json
```

---

### 🧪 مثال‌ها

| مدل          | کلید طول کانتکست                 | مقدار معمول          |
| --------------- | ---------------------------------------------- | ------------------------------ |
| LLaMA / Mistral | `max_position_embeddings`                    | 4096 – 32 k                   |
| GPT-2           | `n_positions` یا `n_ctx`                 | 1024                           |
| RoPE-based      | `max_position_embeddings` + `rope_scaling` | بستگی به scale دارد |

---

### 📚 منبع

- فایل `config.json` هر مدل
- صفحهٔ مدل در [Hugging Face Hub](https://huggingface.co)

---

🪐 ساخته‌شده با عشق و کنجکاوی توسط **Orinnebula**
