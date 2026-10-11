# Eligibility Rules, Edge Cases & Decision Matrix

This document provides exact decision rules, edge cases, and verbatim response guidelines for every business logic condition in the LAP Voice Agent.

---

## 🎯 1. Detailed Rules & Decision Table

| Variable | Permitted / Pass Criteria | Rejection / Fail Criteria | Agent Action on Fail |
|---|---|---|---|
| **Customer Verification** | Customer confirms they are {{customer_name}} | Wrong person / unavailable person | Polite goodbye or ask when to call back |
| **Availability (Busy Check)** | Free to talk / willing to hear offer | "I'm busy", "In a meeting", "Driving" | Ask preferred callback time $\rightarrow$ Acknowledge $\rightarrow$ End Call |
| **Existing Loan / EMI Reduction** | Fresh loan request (No existing loan on property) | Existing loan on property OR customer seeking balance transfer / EMI reduction | Route to Loan Transfer Specialist $\rightarrow$ End Call |
| **1. Property Type** | Residential, Commercial, Industrial | **Agricultural** land / Farm land | **Immediate Disqualification** $\rightarrow$ End Call |
| **2. Ownership** | Sole ownership, Joint ownership (spouse/parents/siblings) | None (Both are valid) | N/A |
| **3. Original Documents** | Original deed/papers available at home, bank locker, or with customer | Only photocopies available, lost originals, dispute/litigation | **Immediate Disqualification** $\rightarrow$ End Call |
| **4. Desired Loan Amount** | $\le ₹75,00,000$ (₹75 Lakhs) | $> ₹75,00,000$ (e.g. ₹90 Lakhs, ₹1.5 Cr) | **Do not reject immediately.** Explain max cap of ₹75L and ask if they wish to proceed with ₹75L. If No $\rightarrow$ End Call. |
| **5. Occupation & Income Mode** | Salaried or Self-Employed **AND** income credited via Bank transfer/cheque | Income received in **Cash** (regardless of occupation) | **Immediate Disqualification** $\rightarrow$ End Call |
| **6. Estimated Market Value** | Any customer estimate (e.g. ₹50 Lakhs, ₹1.5 Cr, ₹3 Cr) | No threshold specified by policy | Accept customer estimate and proceed |
| **7. Desired Tenure** | **3 to 15 years** (36 to 180 months) | $< 3$ years (e.g. 1–2 years) OR $> 15$ years (e.g. 20–25 years) | **Immediate Disqualification** $\rightarrow$ End Call |

---

## ⚡ 2. Exact Script Snippets for Specific Branches

### A. Busy Customer Flow
> *"I completely understand, {{customer_name}}. What day and time would be convenient for us to call you back?"*
> 
> *(After customer answers:)*
> *"Thank you. I have noted that down. We will connect with you at {{preferred_time}}. Have a wonderful day!"* $\rightarrow$ **[END CALL]**

### B. Existing Loan / EMI Reduction Flow
> *"Thank you for letting me know. Since you already have an active loan on this property, this qualifies for our loan-transfer and EMI-reduction program, which is managed by our dedicated Loan Transfer Specialist. I will have a specialist contact you shortly with tailored options. Thank you for your time!"* $\rightarrow$ **[END CALL]**

### C. Loan Amount Exceeding ₹75 Lakhs
> *"Our pre-approved offer for this program is available up to a maximum of ₹75 Lakhs. Would you like to proceed with the maximum eligible amount of ₹75 Lakhs for your application?"*
> - If **Yes**: Set `loan_amount = ₹75,00,000` and proceed to the next missing question.
> - If **No**: *"I understand. Since your requirement exceeds our current program cap of ₹75 Lakhs, we won't be able to proceed under this offer today. Thank you for your time, {{customer_name}}!"* $\rightarrow$ **[END CALL]**

### D. Disqualification (Agricultural / Cash Income / No Originals / Out-of-Range Tenure)
> *"Thank you for sharing those details, {{customer_name}}. Based on our current program guidelines, we are unable to process this pre-approved offer for [Agricultural properties / Cash-based income / Unavailable original documents / Tenures outside 3 to 15 years]. We appreciate your relationship with {{company_name}} and look forward to serving you in the future. Have a great day!"* $\rightarrow$ **[END CALL]**

### E. Qualified Handoff (All 7 Questions Passed)
> *"Great news, {{customer_name}}! Based on the preliminary details you've shared, your profile qualifies for our pre-approved Loan Against Property offer. A Senior Loan Expert from {{company_name}} will contact you shortly to guide you through the exact interest rates, customized terms, and next steps. Thank you for choosing {{company_name}}, and have a wonderful day!"* $\rightarrow$ **[END CALL]**

---

## 🛡️ 3. Handling Diversions & RAG Knowledge Boundaries

### Rule 1: Interest Rate Inquiries
- **Customer:** *"What interest rate will you charge me?"*
- **Agent Response:** *"The exact interest rate and personalized terms will be tailored and provided directly by our Senior Loan Expert after this quick preliminary check. Shall we quickly finish the remaining eligibility points?"* $\rightarrow$ Return to first missing question.

### Rule 2: Unrelated Product / Branch Location Questions
- Check `{{additional_context_from_rag}}`.
- If answer is present in RAG: Provide a crisp 1-sentence answer, then gracefully redirect: *"Regarding our branches, [RAG info]. Now, coming back to your loan requirement..."*
- If not in RAG: Do not fabricate. Say: *"I will have our senior specialist address that for you during the detailed discussion. To help them prepare, could you tell me..."* $\rightarrow$ Return to first missing question.

### Rule 3: Natural Speech & Correction Handling
- **Fillers:** Filter out "uhm", "actually", "like", "let me see".
- **Self-Corrections:** Always adopt the latest explicit statement. (e.g. *"I'm looking for 10 years... no, 15 years would be better"* $\rightarrow$ Record `15 years`).
- **Unclear / Ambiguous Statements:** Do not assume. Re-clarify with a polite confirmation (e.g., *"Just to be sure, are the original deeds available for verification?"*).
