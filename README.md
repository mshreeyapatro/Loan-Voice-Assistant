# Home Credit — AI Voice Agent for Loan Against Property (LAP)

This repository contains the complete design, production-grade system prompt, decision matrices, test cases, call logs, and deployment guides for the **Home Credit AI Voice Qualification Agent** developed for the SalesAgents AI assignment.

---

## 📑 Repository Structure & Deliverables

```
Voice Agent/
├── prompts/
│   ├── SYSTEM_PROMPT.md                           # Core Production System Prompt with dynamic variables
│   └── RETELL_AI_PASTE_READY.md                  # Web-call ready prompt with pre-filled test entities
├── docs/
│   ├── 01_PROJECT_REQUIREMENTS_AND_ARCHITECTURE.md # 5-Layer architecture & conversational flowcharts
│   ├── 02_ELIGIBILITY_RULES_AND_DECISION_MATRIX.md # Detailed business rules, scripts, & edge cases
│   ├── 03_TEST_SCENARIOS_AND_EVALUATION_SCRIPTS.md # 12 Test scenarios + 4 Adversarial stress tests
│   └── 04_PLATFORM_SETUP_AND_SUBMISSION_GUIDE.md   # Deployment on Retell/Bolna, audio export, & submission
├── audios/                                        # Exported test call audio recordings (.mp3 / .wav)
├── transcripts/                                   # Transcripts & latency logs for each conducted test call
└── README.md                                      # Master Project Overview
```

---

## 🎯 Assignment Deliverables Checklist

| Deliverable | Location in Repository | Status |
|---|---|---|
| **1. Complete System Prompt Text** | [`prompts/SYSTEM_PROMPT.md`](prompts/SYSTEM_PROMPT.md) | ✅ Complete |
| **2. Architecture & Design Doc** | [`docs/01_PROJECT_REQUIREMENTS_AND_ARCHITECTURE.md`](docs/01_PROJECT_REQUIREMENTS_AND_ARCHITECTURE.md) | ✅ Complete |
| **3. Decision Matrix & Business Rules**| [`docs/02_ELIGIBILITY_RULES_AND_DECISION_MATRIX.md`](docs/02_ELIGIBILITY_RULES_AND_DECISION_MATRIX.md) | ✅ Complete |
| **4. Test Scenarios Matrix & Scripts** | [`docs/03_TEST_SCENARIOS_AND_EVALUATION_SCRIPTS.md`](docs/03_TEST_SCENARIOS_AND_EVALUATION_SCRIPTS.md) | ✅ Complete |
| **5. Test Call Audios** | [`audios/`](audios/) | 📁 Drop files here |
| **6. Call Transcripts & Logs** | [`transcripts/`](transcripts/) | 📁 Drop files here |

---

## 🚀 Key Highlights & Architectural Strengths

1. **"Extract First, Ask Missing" Algorithm:**
   - Automatically extracts multi-slot answers provided out of order.
   - Updates internal memory state and always computes the first unanswered checklist question.
   - Eliminates redundant, annoying questions.

2. **Strict Hard-Disqualification Gates:**
   - `Agricultural Property` $\rightarrow$ Immediate Polite Disqualification & Call Termination.
   - `Cash Income` $\rightarrow$ Immediate Polite Disqualification & Call Termination.
   - `No Original Documents` $\rightarrow$ Immediate Polite Disqualification & Call Termination.
   - `Tenure < 3 or > 15 Years` $\rightarrow$ Immediate Polite Disqualification & Call Termination.

3. **Special Branch Routing:**
   - `Loan Amount > ₹75 Lakhs` $\rightarrow$ Explains ₹75L cap and asks if customer agrees to proceed.
   - `Existing Loan / EMI Reduction` $\rightarrow$ Routed directly to Loan Transfer Specialist; skips fresh loan questionnaire.
   - `Busy Customer` $\rightarrow$ Captures callback date/time and ends politely.

4. **Natural Speech & Diversion Handling:**
   - Accommodates speech fillers, spontaneous self-corrections (latest statement rules), and customer interruptions.
   - Defers interest rate inquiries to the Senior Loan Expert without fabricating rates.
   - Adheres strictly to configured agent gender and language.

---

## 🔗 Quick Links
- 📜 [Production System Prompt](prompts/SYSTEM_PROMPT.md)
- 📋 [Retell AI Paste-Ready Prompt](prompts/RETELL_AI_PASTE_READY.md)
- 📐 [Architecture & Workflow](docs/01_PROJECT_REQUIREMENTS_AND_ARCHITECTURE.md)
- 📊 [Eligibility & Decision Matrix](docs/02_ELIGIBILITY_RULES_AND_DECISION_MATRIX.md)
- 🧪 [Test Matrix & Scripts](docs/03_TEST_SCENARIOS_AND_EVALUATION_SCRIPTS.md)
- 🛠️ [Platform Deployment Guide](docs/04_PLATFORM_SETUP_AND_SUBMISSION_GUIDE.md)
