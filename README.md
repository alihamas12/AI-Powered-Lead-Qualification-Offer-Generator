# AI-Powered Lead Qualification & Offer Generator (n8n)

![Workflow Overview](workflow_image.png)

## 🚀 Overview

This **n8n workflow** automates the sales process for service-based businesses (specifically tailored for a cleaning service). It monitors incoming emails, uses **AI (GPT-4o & Google Gemini)** to extract customer requirements, calculates pricing via **Excel**, and generates formal offers in **MOCO** (CRM).

## ✨ Features

* **Multi-LLM Integration:** Utilizes **GPT-4o** for complex logic/analysis and **Gemini 1.5 Flash** for fast data extraction.
* **Excel as Database:** Checks if a customer exists, updates existing rows, or appends new leads automatically.
* **Formula Calculation:** Writes data to Excel, waits for formulas to calculate the price, and reads the result back into n8n.
* **CRM Integration (MOCO):** Automatically creates customers and generates formal offers in the MOCO platform.
* **Email Automation:**
    * **Outlook & IMAP:** Triggers on new emails.
    * **Smart Drafting:** Drafts replies based on missing information or sends the final offer if data is complete.

## 🛠️ Tech Stack

* **Workflow Engine:** [n8n](https://n8n.io)
* **AI Models:** OpenAI GPT-4o, Google Gemini 1.5 Flash
* **Database/Calc:** Microsoft Excel (Online)
* **Email:** Microsoft Outlook & IMAP/SMTP
* **CRM/Invoicing:** MOCO

## 📋 Prerequisites

Before importing this workflow, ensure you have:

1.  **n8n Installed:** Self-hosted or Cloud version.
2.  **Microsoft 365 Account:** Access to Excel Online and Outlook.
3.  **API Keys:**
    * OpenAI API Key
    * Google Gemini API Key
    * MOCO API Token & Subdomain

## ⚙️ Setup & Configuration

1.  **Import the Workflow:**
    * Download the `.json` file from this repository.
    * In n8n, click **menu** > **Import from File**.

2.  **Configure Credentials:**
    * Set up your `Microsoft Excel` and `Microsoft Outlook` OAuth2 credentials in n8n.
    * Set up your `OpenAI` credential.

3.  **Update HTTP Request Nodes:**
    The workflow uses HTTP nodes for Gemini and MOCO. You must manually update these fields inside the nodes:
    * **Gemini Nodes:** Replace `PASTE_YOUR_GEMINI_API_KEY_HERE` with your actual key.
    * **MOCO Nodes:**
        * Replace `PASTE_YOUR_DOMAIN` with your MOCO subdomain.
        * Replace `PASTE_YOUR_MOCO_API_KEY` with your API token.

4.  **Excel Setup:**
    Ensure your Excel file has the following headers (or update the nodes to match your sheet):
    * `Square Meters`
    * `Customer Name`
    * `Email Address`
    * `Calculated Price` (Formula column)

## 🧩 Workflow Logic

1.  **Trigger:** Detects new email via Outlook or IMAP.
2.  **Lookup:** Checks Excel to see if the sender is an existing lead.
3.  **AI Extraction:**
    * If new: Extracts Name, SQM, and Requirements.
    * If existing: Checks for updates to requirements.
4.  **Calculation:** Syncs data to Excel and waits 3 seconds for Excel formulas to compute the price.
5.  **Execution:**
    * Creates Customer & Offer in MOCO.
    * Sends an email with the offer link OR creates a draft asking for missing details.

## 📄 License

This project is licensed under the MIT License.
