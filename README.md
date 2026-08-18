# ⚡ Autonomous Revenue Recovery Engine (E-Commerce)

An enterprise-grade, stateful cart recovery pipeline built in Make.com using custom webhooks, dynamic delay logic, Google Gemini API personalization, and automated email delivery.

![Autonomous Revenue Recovery Engine Canvas](./autonomous-revenue-recovery-engine-canvas.png)
*Figure 1: Make.com scenario canvas showing webhook trigger, stateful delay tools, Gemini HTTP module, and mail routing.*

---

## 🎯 Business Problem
E-commerce brands lose up to **70% of abandoned carts** due to generic, ill-timed follow-up templates and fragile linear automations. Unhandled API rate limits, duplicate webhook events, and a lack of dynamic state checks result in awkward emails sent to customers who already purchased, damaged domain reputations, and thousands of dollars in lost monthly revenue.

---

## 🚀 Solution Overview
This production-grade Make.com engine acts as a state-aware cart recovery gatekeeper:

1. **Webhook Ingestion & Payload Capture:** Instantly captures abandoned cart payloads containing customer details, cart items, total cart value, and delay parameters.
2. **Stateful Delay & Purchase Evaluation:** Holds scenario execution using Make `Tools (Sleep/Delay)` to allow time for customer action, then dynamically verifies if the cart was already purchased before firing outreach.
3. **Branching Logic Routing:**
   * **`1st Cart Purchased`:** Instantly halts outreach if purchase status evaluates to true, protecting customer experience.
   * **`1st Email Present?`:** Routes unpurchased carts into the personalized AI generation pipeline.
4. **Gemini API Personalization Engine:** Calls the Google Gemini API (`v1beta` HTTP REST endpoint) with dynamic prompt injection (cart items, cart value, wait time) to generate high-converting, personalized recovery copy.
5. **Text Parsing & Custom Mail Dispatch:** Leverages standard `Text Parser` to extract generated email bodies and subjects, then fires recovery emails via `Custom Mail`.

---

## 💰 Business Impact & ROI
* **📈 Higher Recovery Conversion:** Dynamic AI copy tailored to exact cart items dramatically outperforms static generic templates, directly increasing recovered checkout revenue.
* **🛡️ Brand Reputation & Customer Experience Protection:** Stateful delay gates prevent redundant "buy this" emails from being dispatched to customers who already completed their checkout.
* **⚙️ Zero-Maintenance Reliability:** Autonomous state handling eliminates manual campaign intervention and pipeline triage for growing e-commerce stores.

---

## 🧪 Live Execution Proof & Payload Verification

### 1. Successful Make.com Execution History
![Execution Log Success](./execution-log-success.png)
*Figure 2: Execution log proving 100% successful runs across all scenario paths and delay states.*

### 2. Node Input / Output JSON Data Payload & AI Prompt Analysis
![Gemini Prompt Payload](./gemini-prompt-payload.png)
*Figure 3: Structured Gemini API request payload showing system instructions, cart context, and prompt variable injection.*

---

## 🛠️ Tech Stack & Integrations
* **Orchestration Platform:** Make.com (Enterprise Standard)
* **AI Engine:** Google Gemini API (REST HTTP)
* **Modules Used:** Custom Webhooks, Tools (Sleep/Delay), Text Parser, Custom Mail

---

## ⚡ Platform Agnostic Deployment (Make.com vs. n8n)

While this blueprint is built for rapid deployment in Make.com, I also engineer and migrate this exact architecture to **self-hosted n8n**:

* **💰 80%+ Operational Cost Reduction:** Eliminates Make.com operation limit tiers by executing unlimited runs on self-hosted n8n infrastructure.
* **🛡️ Zero Data Privacy & Vendor Lock-in Risks:** Full end-to-end control over execution logs, customer data, and API keys.
* **⚡ Native Error Triggers & DLQs:** Built-in sub-workflow error isolation and dead-letter queue routing for enterprise-scale volume.

---

## ⚙️ How to Import
1. Download the `_Autonomous Revenue Recovery Engine (E-Commerce).blueprint.json` file from this repository.
2. Open Make.com → Scenarios → **Import Blueprint**.
3. Insert your `GEMINI_API_KEY` parameter inside the HTTP module URL.
4. Configure your SMTP/Custom Mail credentials and activate the webhook endpoint.

---

## 📈 Engineering Roadmap & Milestone
* **Roadmap Phase:** Phase 2 (Automation Engineering)
* **Sprint Tracker:** Sprint 4 — AI Integration, API Keys & Structured AI Outputs
* **Build Milestone:** Completed (Day 62/153)
