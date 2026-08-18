# ⚡ Autonomous Revenue Recovery Engine (E-Commerce)

An enterprise-grade, stateful cart recovery pipeline built in Make.com using custom webhooks, dynamic delay logic, Google Gemini API personalization, Supabase state persistence, and automated email delivery.

![Autonomous Revenue Recovery Engine Canvas](./autonomous-revenue-recovery-engine-canvas.png)
*Figure 1: Make.com scenario canvas showing webhook trigger, stateful delay tools, Supabase logging, Gemini HTTP module, and mail routing.*

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
6. **Supabase Logging & State Persistence:** Writes scenario execution data and recovery state directly to database tables for audit logging.

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
* **Database & Memory:** Supabase (PostgreSQL Audit Logging)
* **AI Engine:** Google Gemini API (REST HTTP)
* **Modules Used:** Custom Webhooks, Tools (Sleep/Delay), Text Parser, Custom Mail, Supabase API

---

## 🧩 Module-by-Module Breakdown

Here is a plain-English breakdown of every node engineered into this pipeline and the specific business value each module delivers:

* **1. Custom Webhook (Payload Ingestion):**
  * **What it does:** Captures real-time abandoned checkout payloads (customer contact, cart items, subtotal, and delay parameters) the moment a shopper leaves the store.
  * **Value:** Serves as a reliable entry gate to ensure zero dropped cart events across high-traffic volume spikes.

* **2. Tools / Sleep & Delay (Stateful Wait Gate):**
  * **What it does:** Holds scenario execution for a configured duration (e.g., 30–60 minutes) to give shoppers adequate time to complete checkout naturally.
  * **Value:** Prevents premature, aggressive email triggers while shoppers are still actively completing their order.

* **3. Supabase / State Query (Real-Time Purchase Verification):**
  * **What it does:** Queries the database in real time following the wait period to check current customer purchase status and historical email logs.
  * **Value:** Enforces stateful verification before firing any outreach, protecting brand credibility and customer experience.

* **4. Router & Branching Filters (Deterministic Traffic Control):**
  * **What it does:** Evaluates queried database records and splits execution across three deterministic paths:
    * **`1st Cart Purchased`:** Instantly terminates the scenario if the customer completed their purchase during the delay window.
    * **`1st Email Present?`:** Routes unpurchased carts directly into the AI generation pipeline for first-touch recovery.
    * **`2nd Cart Abandoned`:** Directs long-standing abandoned carts into secondary recovery workflows.
  * **Value:** Guarantees paying buyers **never** receive redundant recovery emails, eliminating unsubscribes and spam complaints.

* **5. Gemini 1.5 Flash HTTP API (Contextual AI Generation):**
  * **What it does:** Sends exact cart context (items, cart value, customer name, delay duration) to Google Gemini API to generate tailored recovery copy.
  * **Value:** Replaces static templates with hyper-personalized messaging that significantly improves click-through and conversion rates.

* **6. Text Parser (Output Sanitization):**
  * **What it does:** Extracts clean subject lines and email bodies from raw AI API responses while stripping unneeded code artifacts.
  * **Value:** Ensures formatted, error-free copy reaches the recipient inbox every single time.

* **7. Custom Mail Dispatch (SMTP Outreach Delivery):**
  * **What it does:** Transmits the personalized recovery email directly to the customer using authenticated domain credentials.
  * **Value:** Maximizes domain inbox placement and drives high-intent buyers back to their saved cart.

* **8. Supabase / Execution Audit Log (Database Persistence):**
  * **What it does:** Writes workflow execution metrics, timestamped logs, and recovery email status back to Supabase tables.
  * **Value:** Creates an immutable audit trail for full operational tracking, reporting, and debugging.

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
4. Configure your Supabase database parameters and SMTP/Custom Mail credentials.
5. Activate the webhook endpoint.

---

## 📈 Engineering Roadmap & Milestone
* **Roadmap Phase:** Phase 2 (Automation Engineering)
* **Sprint Tracker:** Sprint 4 — AI Integration, API Keys & Structured AI Outputs
* **Build Milestone:** Completed (Day 62/153)
