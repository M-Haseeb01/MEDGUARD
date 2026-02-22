# MEDGUARD
# 🛡️ MedGuard
### AI-Powered Medical Misinformation Defense System
> *2 billion people receive their health advice on WhatsApp before they ever see a doctor. MedGuard fights back.*



---

## 📖 Overview

MedGuard is a real-time, patient-specific medical misinformation detector powered by Google's **MedGemma 4B-IT** multimodal foundation model. It runs entirely on local hardware — no cloud, no internet required after setup — making it deployable in clinics, field tablets, and community health settings across low-connectivity regions.

Built for the **MedGemma Impact Challenge — Kaggle 2026**.

---

## 🌍 The Problem

- **2+ billion** WhatsApp users receive unverified health advice daily
- WHO estimates **$287 billion** annual cost from health misinformation
- Populations with least access to doctors have most exposure to dangerous claims
- Viral claims like *"Drink Dettol to cure COVID"* cause real, documented harm

---

## ✨ Features

- ⚖️ **Verdict** — True / False / Mixed / Insufficient Evidence
- 🚨 **Risk Level** — 🔴 High / 🟡 Medium / 🟢 Low
- 🧠 **Clinical Reasoning** — evidence-based, calibrated to patient profile
- 👨‍⚕️ **Doctor Triage Note** — structured handoff summary for physicians
- 🖼️ **Multimodal** — analyze X-rays, wounds, scans alongside text claims
- 🌍 **Multilingual** — English, Urdu, Arabic, Hindi, French, Spanish
- 📴 **100% Offline** — no API calls, no data leaves the device

---

## 🔬 Technical Architecture
```
Patient Profile + Claim + Optional Image
              ↓
    MedGemma 4B-IT (Multimodal)
    GGUF Q4_K_M — 4GB RAM, no GPU required
    Native Gemma prompt format
              ↓
    3-Layer JSON Parsing Pipeline
    (strict → regex → field fallback)
              ↓
    ArgosTranslate — 100% Offline
              ↓
    Streamlit UI
```

**Stack:**
| Component | Technology |
|---|---|
| Model | MedGemma 4B-IT (GGUF Q4_K_M) |
| Runtime | llama.cpp |
| Hardware | Auto GPU/CPU detection |
| Translation | ArgosTranslate (offline) |
| UI | Streamlit |
| Demo | ngrok (Colab) |

---

## 📊 Results — 5 Live Test Cases

| Case | Verdict | Risk | Confidence |
|---|---|---|---|
| Drinking Dettol cures COVID-19 | ❌ False | 🔴 High | 99% |
| Eating oranges gives vitamin C | ✅ True | 🟢 Low | 95% |
| Cold water causes cancer | ❌ False | 🟢 Low | 99% |
| Jeera water cures diabetes | ❌ False | 🟡 Medium | 95% |
| Turmeric cures pneumonia | ❌ False | 🟡 Medium | 95% |

✅ All 5 cases correctly evaluated with high confidence.

---

## 🚀 Quick Start

### 1. Clone
```bash
git clone https://github.com/yourusername/medguard.git
cd medguard
```

### 2. Install
```bash
pip install llama-cpp-python huggingface_hub pillow argostranslate streamlit \
  --extra-index-url https://abetlen.github.io/llama-cpp-python/whl/cpu
```

### 3. Run
```bash
streamlit run app.py
```
Model downloads automatically on first run (~4GB). Fully offline after that.

### Or run on Colab
Open `MedGuard_Colab.ipynb` — installs, loads, and launches via ngrok automatically.

---

## 📁 Project Structure
```
medguard/
│
├── medguard_core.py      # Core inference engine
├── app.py                # Streamlit UI
├── MedGuard_Colab.ipynb  # Colab notebook (full pipeline)
└── README.md
```

---

## 💡 Usage
```python
from medguard_core import load_edge_model, analyze

model = load_edge_model()

result = analyze(
    model       = model,
    user_claim  = "Drinking Dettol cures COVID-19",
    sym         = "Fever, cough",
    history     = "30-year-old Male, No chronic illness",
    target_lang = "en"
)

print(result)
# {'verdict': 'False', 'risk_level': 'High', 'confidence': '0.99', ...}
```

---

## 🏗️ Edge AI Design

MedGuard is built for real-world field deployment:

- **No GPU required** — GGUF Q4_K_M runs on any laptop or clinic PC
- **Auto hardware detection** — same code switches between CPU and GPU
- **ARM compatible** — llama.cpp supports mobile and embedded devices
- **Zero cloud dependency** — patient data never leaves the device
- **Offline translation** — ArgosTranslate works with no internet

---

## ⚠️ Disclaimer

MedGuard is an AI triage support tool. It does **not** replace qualified medical professionals. Always consult a doctor for medical decisions.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

*Built for the MedGemma Impact Challenge — Kaggle 2026*
*Powered by Google MedGemma 4B-IT*
