# LLM-DLP-Redaction-System

An **AI-native Data Loss Prevention (DLP)** platform that automatically detects and redacts sensitive information (emails, phone numbers, SSNs, credit cards, API keys, etc.) from unstructured text in real-time using transformer-based Named Entity Recognition (NER).  
Includes **agentic remediation workflows**, **policy enforcement**, **drift monitoring**, **entity distribution analytics**, and a **redaction dashboard**.

---

## Key Features

**Transformer-based Token Classification (NER)**  
- Fine-tuned DistilBERT on custom PII corpus  
- Aggregation strategy for robust span clustering  

**Automatic Sensitive Data Redaction**  
- Policy-driven masking per entity type  
- Right-to-left span replacement (index-safe)  
- Hybrid NER + regex fallback engine  

**Agentic Remediation Workflows**
- Severity scoring per inference
- Action suggestions (silent redact, notify, escalate)
- End-user coaching logic

**Model Drift & Threat Behavior Monitoring**
- Tracks entity frequency shifts over time
- Z-score anomaly alerts
- JSON-based append-only security log

**Security Analytics Dashboard**
- Entity distribution time-series
- Rolling averages and spikes
- Severity bars & drift heatmaps

**Microservice-Ready**
- Stateless redaction pipeline
- Easily exposed via FastAPI, Flask, or queue workers

**Production-Mindful Design**
- `.gitignore` for model binaries
- Local checkpoint support
- Modular policy engine

---
# Architecture Design
                         ┌──────────────────┐
User Input ────────────▶ │ Inference Engine │ ─────┐
                         └─────────┬────────┘       │
                                   │                │ (NER spans)
                                   ▼                │
                         ┌──────────────────┐       │
                         │ Redaction Engine │       │
                         └─────────┬────────┘       │
                                   │                │ (Remediated text)
                                   ▼                │
                         ┌──────────────────┐       │
                         │  Policy Engine   │ ◀─────┘
                         └─────────┬────────┘
                                   │
                                   ▼
                         ┌──────────────────┐
                         │   Drift Logger   │
                         └─────────┬────────┘
                                   │
                                   ▼
                     ┌────────────────────────────┐
                     │ Security Analytics Dashboard│
                     └────────────────────────────┘

---

## Entity Types Supported

| Entity | Example | Action |
|--------|---------|--------|
| EMAIL | alice@example.com | Mask local part |
| PHONE | 415-555-1212 | Last-4 visible |
| SSN | 123-45-6789 | Last-4 visible |
| CREDITCARD | 4242-4242-4242-4242 | Last-4 visible |
| APIKEY | sk_live_abcdef... | Redacted fully |
| PERSON | John Doe | `[PERSON]` |
| ADDRESS | 221B Baker St | `[ADDRESS]` |



## 🛠️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/Kartikay77/LLM-DLP-Redaction-System.git
cd LLM-DLP-Redaction-Syste
```





