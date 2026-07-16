# 📧 AI-Powered Gmail Summarizer Agent

An autonomous, agentic workflow built in n8n that automatically ingests, synthesizes, and logs unread emails into a centralized Google Doc report using Google's Gemini LLM. 

This project demonstrates the ability to orchestrate zero-touch AI pipelines, integrating cloud APIs with LangChain-based AI agents to eliminate manual inbox triage and surface critical deadlines.

## 🚀 Business Value & Motivation
Executives and team leads often lose hours daily triaging unread emails. By leveraging a large language model (LLM) within a scheduled automated pipeline, this agent acts as an autonomous Executive Assistant. It reads incoming data, groups related topics, highlights urgent action items, and generates a structured daily briefing—saving time and preventing missed deadlines.

## 🏗️ Workflow Architecture

The pipeline is built using a Directed Acyclic Graph (DAG) structure in n8n, utilizing the following nodes:

*   **⏱️ Schedule Trigger:** Initiates the workflow on a predefined interval (e.g., daily at 8:00 AM).
*   **📥 Data Ingestion (Gmail API):** Securely connects to the target inbox via OAuth2 to fetch the top 5 unread messages, filtering out noise.
*   **🔄 Data Aggregation:** Uses an Aggregate node to compile the isolated JSON text snippets from multiple emails into a single, unified text stream for the LLM context window.
*   **🧠 LangChain AI Agent:** A custom-prompted autonomous agent powered by **Google Gemini**. The agent is instructed to adopt an "Executive Assistant" persona.
*   **📝 Output Delivery (Google Docs API):** The synthesized report is pushed directly into a shared Google Doc, ensuring the end-user has a persistent, living log of daily summaries.

## ⚙️ Agentic Prompt Engineering
The Gemini-powered LangChain agent relies on a strict set of operational constraints to ensure the output is deterministic and formatted for enterprise use:

1.  **Paragraph Structuring:** Forces single-paragraph summaries per email.
2.  **Standardized Headers:** Prepends summaries with `Subject/Context: [Brief Topic]`.
3.  **Deadline Extraction:** Automatically identifies and **bolds** urgent deadlines or action items.
4.  **Topic Grouping:** Intelligently groups multiple emails discussing the same subject into a unified summary block.
5.  **Strict Output:** Strips all conversational AI filler (e.g., "Here is your summary") to push clean string data to the document.

## 🚀 How to Import and Run

### 1. Prerequisites
*   An active [n8n](https://n8n.io/) instance (Cloud or Self-Hosted).
*   Google Cloud Platform (GCP) credentials for **Gmail API** and **Google Docs API**.
*   An API Key for **Google Gemini (PaLM)**.

### 2. Installation
1. Download the `gmail_summarizer_agent.json` file from this repository.
2. Open your n8n workspace.
3. In the top right corner of the canvas, click **Import from File** and select the JSON file.

### 3. Configuration
1. Open the **Gmail** node and authenticate using your Google OAuth2 credentials.
2. Open the **Google Gemini Chat Model** node and input your Gemini API Key.
3. Open the **Google Docs** node, authenticate, and replace the `documentURL` parameter with the link to your own target Google Doc.
4. Activate the workflow!

## 🛠️ Tech Stack
*   **Orchestration:** n8n
*   **AI Framework:** LangChain (n8n native nodes)
*   **LLM:** Google Gemini
*   **Integrations:** Gmail API, Google Docs API
