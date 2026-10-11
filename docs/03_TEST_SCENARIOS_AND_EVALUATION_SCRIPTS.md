# Test Scenarios, Evaluation Scripts & Adversarial Cases

This document details **12 Primary Test Scenarios** and **4 Adversarial Stress Tests** designed to evaluate the AI Voice Agent across happy paths, hard rejections, edge cases, out-of-order data capture, and interruptions.

---

## 🧪 1. Comprehensive Test Scenarios Matrix

| Scenario # | Test Case Description | Key Input Trigger | Expected Behavior / Outcome |
|---|---|---|---|
| **Test 1** | **Golden Path (Fully Eligible)** | Residential, Sole, Originals, ₹50L, Salaried Bank, ₹1.2 Cr value, 10 Yrs | Completes all 7 $\rightarrow$ Handoff to Senior Loan Expert |
| **Test 2** | **Disqualification: Agricultural Land** | Property Type = "Agricultural farmland" | Instant Disqualification $\rightarrow$ Polite Goodbye $\rightarrow$ End Call |
| **Test 3** | **Disqualification: Cash Income** | Self-employed, Income = "Cash in hand" | Instant Disqualification $\rightarrow$ Polite Goodbye $\rightarrow$ End Call |
| **Test 4** | **Disqualification: Only Photocopies** | Documents = "Only xerox / photocopies" | Instant Disqualification $\rightarrow$ Polite Goodbye $\rightarrow$ End Call |
| **Test 5** | **Disqualification: Tenure < 3 Years** | Tenure = "2 years" / "18 months" | Instant Disqualification $\rightarrow$ Polite Goodbye $\rightarrow$ End Call |
| **Test 6** | **Disqualification: Tenure > 15 Years** | Tenure = "20 years" | Instant Disqualification $\rightarrow$ Polite Goodbye $\rightarrow$ End Call |
| **Test 7** | **Loan Amount Cap Handling (> ₹75L)** | Customer asks for "₹90 Lakhs" | Agent explains ₹75L cap $\rightarrow$ Asks if OK $\rightarrow$ Continues with ₹75L on Yes |
| **Test 8** | **Joint Ownership Acceptance** | Ownership = "Jointly owned with my wife" | Accepted as eligible $\rightarrow$ Moves to next missing question |
| **Test 9** | **Existing Property Loan Branch** | Customer says "I already have a mortgage on it" | Routes to Loan Transfer Specialist $\rightarrow$ Ends Call (No Q1-7) |
| **Test 10** | **EMI Reduction Request Branch** | Customer says "I want to reduce my EMI" | Routes to Loan Transfer Specialist $\rightarrow$ Ends Call (No Q1-7) |
| **Test 11** | **Multi-Slot Out-of-Order Capture** | "It's residential, jointly owned, worth 1.5 Cr" | Extracts Q1, Q2, Q6 $\rightarrow$ Asks Q3 (Original Docs) $\rightarrow$ Never re-asks Q1, Q2, Q6 |
| **Test 12** | **Busy Customer Flow** | Customer says "I am in a client meeting" | Asks preferred callback time $\rightarrow$ Acknowledges $\rightarrow$ Ends Call |

---

## 🎭 2. Detailed Conversation Scripts for Key Scenarios

### 🔹 Scenario 1: Golden Path (Eligible Customer)
* **Agent:** *"Hello, good afternoon! Am I speaking with Mr. Rahul Sharma?"*
* **User:** *"Yes, speaking."*
* **Agent:** *"Do you have a couple of minutes to speak?"*
* **User:** *"Sure, go ahead."*
* **Agent:** *"As a valued customer of Home Credit, you are pre-approved for a Loan Against Property of up to ₹75 Lakhs. To get started, is this for a fresh loan on a clear property, or are you looking to transfer an existing loan?"*
* **User:** *"It's for a fresh loan."*
* **Agent:** *"Great! Could you please tell me what type of property it is—such as residential, commercial, or industrial?"*
* **User:** *"It is a residential apartment."*
* **Agent:** *"Is the property solely in your name, or is it jointly owned?"*
* **User:** *"It's in my name only."*
* **Agent:** *"Are the original property documents and title deeds available with you for verification?"*
* **User:** *"Yes, I have all the original papers."*
* **Agent:** *"Approximately how much loan amount are you looking for?"*
* **User:** *"Around 45 lakhs."*
* **Agent:** *"Could you share your occupation—whether salaried or self-employed—and is your income credited directly into a bank account?"*
* **User:** *"I am salaried and my pay is credited to my HDFC bank account."*
* **Agent:** *"What would be the approximate current market value of your property?"*
* **User:** *"Around 1 crore."*
* **Agent:** *"And over what tenure would you prefer to repay the loan—between 3 to 15 years?"*
* **User:** *"10 years."*
* **Agent:** *"Thank you for sharing all the details, Mr. Rahul Sharma. Based on your inputs, your profile is eligible for our pre-approved Loan Against Property offer. I am forwarding your file to our Senior Loan Expert, who will contact you shortly to provide the exact interest rates and finalize the next steps. Thank you for choosing Home Credit, and have a wonderful day!"*

---

### 🔹 Scenario 2: Instant Disqualification (Agricultural Property)
* **Agent:** *"Could you please tell me what type of property it is—such as residential, commercial, or industrial?"*
* **User:** *"It's an agricultural land / farm land in my village."*
* **Agent:** *"Thank you for sharing that, Mr. Sharma. Based on our current program guidelines, we are unable to process this pre-approved offer for agricultural properties. We appreciate your relationship with Home Credit and look forward to serving you in the future. Have a great day!"*
* **Outcome:** Call terminates immediately. No further questions asked.

---

### 🔹 Scenario 3: Instant Disqualification (Cash Income)
* **Agent:** *"Could you share your occupation—whether salaried or self-employed—and is your income credited directly into a bank account?"*
* **User:** *"I run a grocery store, but all my earnings are cash in hand."*
* **Agent:** *"Thank you for sharing that, Mr. Sharma. Our policy requires income to be credited through official banking channels to qualify for this pre-approved offer. We appreciate your time and relationship with Home Credit. Have a wonderful day!"*
* **Outcome:** Immediate termination.

---

### 🔹 Scenario 7: Loan Amount > ₹75 Lakhs Handling
* **Agent:** *"Approximately how much loan amount are you looking for?"*
* **User:** *"I need about 90 lakhs."*
* **Agent:** *"Our pre-approved offer under this special scheme is available up to a maximum of ₹75 Lakhs. Would you like to proceed with ₹75 Lakhs for your application?"*
* **User:** *"Yes, ₹75 lakhs works for me."*
* **Agent:** *"Wonderful! [Proceeds to next missing question: Occupation & Income]"*

---

### 🔹 Scenario 11: Out-of-Order Multi-Slot Capture
* **Agent:** *"Great! Could you please tell me what type of property it is—such as residential, commercial, or industrial?"*
* **User:** *"It's a residential villa, jointly owned with my brother, and the market value is around 1.5 crore."*
* **Agent (Internal State Updated: `property_type = Residential`, `ownership = Joint`, `market_value = 1.5 Cr`):**
* **Agent Utterance (Asks Q3 - Original Documents):** *"Thank you! Are the original property documents and title deeds available with you for verification?"*
* **Evaluation Point:** Agent skips Q1, Q2, and Q6 naturally.

---

## 🥊 3. Adversarial & Stress Testing

1. **Mid-Stream Correction:**
   - *User:* *"I want a tenure of 5 years... no wait, make that 12 years so EMIs are smaller."*
   - *Expected:* Agent captures `tenure = 12 years` and does not ask tenure again.
2. **Diversion on Interest Rate:**
   - *User:* *"Before I answer that, what interest rate are you guys charging?"*
   - *Expected:* Agent does not invent a rate; explains the Senior Loan Expert will provide exact rates, then politely brings user back to the active checklist question.
3. **Contradictory Property Answer:**
   - *User:* *"It's residential... well actually it's agricultural farmland."*
   - *Expected:* Disqualifies based on final clarification.
4. **Vague Document Status:**
   - *User:* *"The original papers are somewhere, but my uncle might have them or maybe I only have copies."*
   - *Expected:* Agent clarifies: *"Just to confirm, will you be able to produce the physical original title deeds for verification?"* If user says no $\rightarrow$ Disqualify.
