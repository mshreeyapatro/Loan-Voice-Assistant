# Platform Setup, Testing & Assignment Submission Guide

This guide walks you through setting up the AI Voice Agent on popular voice platforms (Retell AI, Bolna, Vapi, Bland AI), running test calls, capturing audio/transcripts, and assembling the final submission.

---

## 🛠️ 1. Platform Setup & Configuration

### Option A: Retell AI (Recommended for high voice quality & fast LLM turn-taking)
1. **Sign Up:** Go to [Retell AI Console](https://beta.retellai.com/) and create a free account.
2. **Create an Agent:**
   - Click **Create New Agent**.
   - Model: Select `GPT-4o` or `Claude 3.5 Sonnet` or `Gemini 1.5 Flash`.
   - Voice: Choose an Indian-accented English or Hindi voice (e.g. ElevenLabs `Priya` or Azure `en-IN-NeerjaNeural` / `hi-IN-SwaraNeural`).
   - Fill in Agent Name (e.g. `Priya`), Company Name (`Home Credit`).
3. **Set the System Prompt:**
   - Copy the complete system prompt from `prompts/SYSTEM_PROMPT.md`.
   - Set the dynamic variables or prefill them in the Retell Agent prompt template:
     - `{{company_name}}`: `Home Credit`
     - `{{agent_name}}`: `Priya`
     - `{{agent_gender}}`: `Female`
     - `{{language_to_speak}}`: `English` (or `Hindi`)
4. **Configure Call Settings:**
   - Set **Responsiveness** / Interruption sensitivity to Moderate (`0.8`).
   - Set **Ambient sound** to Office or None.
   - Set **End Call Tool:** Enable automatic call termination when the agent ends the interaction.

---

### Option B: Bolna (Open source / Voice Agent Orchestrator)
1. **Sign Up:** Go to [Bolna.dev](https://www.bolna.dev/) or run the local open-source orchestrator.
2. **Create an Agent Workflow:**
   - Synthesizer: ElevenLabs / Deepgram / Azure Speech (`en-IN` or `hi-IN`).
   - Transcriber: Deepgram Nova-2 (`en-IN` / `hi`).
   - LLM: OpenAI GPT-4o / Claude 3.5 Sonnet.
3. **Paste System Prompt:** Insert the content of `prompts/SYSTEM_PROMPT.md`.

---

## 🎙️ 2. How to Conduct the Required Test Calls

To create an impressive, high-scoring submission, record at least **6 to 8 test calls** covering the key matrices:

1. **Test Call 1 (Golden Path):** Speak as an eligible salaried customer wanting ₹50L over 10 years.
2. **Test Call 2 (Hard Disqualification - Agricultural):** State that your property is farmland. Check that the agent immediately ends the call politely.
3. **Test Call 3 (Hard Disqualification - Cash Income):** State you are self-employed with cash income. Verify immediate termination.
4. **Test Call 4 (Loan Cap Exceeded - >₹75L):** Request ₹90 Lakhs. Verify that the agent offers the ₹75 Lakh limit and continues when accepted.
5. **Test Call 5 (Existing Loan / EMI Reduction):** Mention you already have an existing property loan. Verify transfer to specialist.
6. **Test Call 6 (Multi-Slot Out-of-Order Capture):** Give property type, ownership, and value together in one breath. Verify agent asks for original documents (Q3) and never re-asks Q1, Q2, or Q6.
7. **Test Call 7 (Busy Customer):** Tell the agent you are in a meeting. Verify callback time is recorded and call ends.

---

## 📁 3. Exporting Deliverables from the Platform

For each conducted test call:
1. **Download Call Audio (.wav / .mp3 / .webm):** Save into your submission `audios/` folder named appropriately:
   - `01_golden_path_eligible.mp3`
   - `02_disqualification_agricultural.mp3`
   - `03_disqualification_cash_income.mp3`
   - `04_loan_cap_exceeded_75L.mp3`
   - `05_existing_loan_transfer.mp3`
   - `06_out_of_order_slot_capture.mp3`
   - `07_busy_customer_callback.mp3`
2. **Export Transcripts (.json / .txt / .md):** Export the call transcript and logs directly from Retell/Bolna dashboard. Save them under `transcripts/`.
3. **Public Sharing Link:** Generate public shareable links from Retell/Bolna for the evaluator to test live or listen to recordings.

---

## 📦 4. Final Submission Checklist

- [x] **1. Complete System Prompt:** `prompts/SYSTEM_PROMPT.md`
- [x] **2. Architecture & Design Document:** `docs/01_PROJECT_REQUIREMENTS_AND_ARCHITECTURE.md`
- [x] **3. Eligibility Decision Matrix:** `docs/02_ELIGIBILITY_RULES_AND_DECISION_MATRIX.md`
- [x] **4. Test Scenarios & Scripts:** `docs/03_TEST_SCENARIOS_AND_EVALUATION_SCRIPTS.md`
- [ ] **5. Call Audio Recordings:** (Recorded via Retell/Bolna web call/test interface)
- [ ] **6. Call Transcripts & Logs:** (Exported from platform)
- [ ] **7. Public Dashboard / Agent Link:** (Provided in your final submission form/email)
