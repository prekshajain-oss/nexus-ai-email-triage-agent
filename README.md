# AI Portfolio & Client Triage Assistant 🤖✉️

An intelligent, automated triage system built to manage inbound client requests. This agent acts as a first line of communication, filtering out spam, answering routine pricing questions via RAG (Retrieval-Augmented Generation), and instantly escalating high-value custom projects to human review.

## 🎯 Project Overview
Freelance developers and tech consultants waste hours filtering through inbound emails, separating serious inquiries from spam or basic FAQ requests. 

This project solves that by orchestrating an AI agent that:
* **Monitors** a dedicated business inbox.
* **Classifies** the intent of the sender.
* **Retrieves** accurate pricing and technical stack data from a closed PDF knowledge base.
* **Executes** conditional actions based on a calculated confidence score.

## ⚙️ Architecture & Tech Stack
* **Orchestration:** Zapier Agents (Beta)
* **Trigger:** Gmail API (New Inbound Email)
* **Knowledge Retrieval (RAG):** Context-constrained to specific uploaded business PDFs.
* **Conditional Actions:** * Gmail API (Create Draft Reply)
  * WhatsApp API (Send Push Notification)

## 🧠 Core Logic & Prompt Engineering
The system relies on strict prompt engineering to prevent hallucinations and ensure professional communication. The AI is constrained by a confidence scoring system (1-10).

**The Decision Matrix:**
* **Confidence >= 7:** AI successfully found the answer in the knowledge base. It drafts a localized email reply in Gmail for a quick human approval click.
* **Confidence < 7 (or Custom Project Intent):** AI halts generation to prevent errors and sends an immediate WhatsApp push notification alerting the human to intervene.
* **Spam/Irrelevant:** AI ignores the email completely, saving token costs and inbox clutter.

*(View the exact system instructions in the `prompt-engineering/system-prompt.txt` file).*

## 📂 Knowledge Base Documents
The AI is restricted to pulling facts exclusively from these two domain-specific documents (available in the `knowledge-base/` folder):
1. `Nexus_Services_Pricing.pdf`: Contains hourly rates, fixed-package pricing, and retainer agreements.
2. `Nexus_Portfolio_FAQ.pdf`: Contains the technical stack (Python, React, Node.js, AI APIs), past project summaries, and standard timelines.

## 🚀 How to Replicate
1. Create a Zapier account and navigate to the **Agents** tab.
2. Set the trigger to monitor a specific Gmail inbox.
3. Upload the PDFs from the `knowledge-base` folder into the Agent's Knowledge Data Sources.
4. Paste the prompt from `system-prompt.txt` into the Instructions box.
5. Connect your Gmail and WhatsApp accounts in the Tools section using the `/` command.
