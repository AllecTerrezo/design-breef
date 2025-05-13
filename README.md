## **Designer Brief – AI/Automation Architect**
Project: Design Brief Orchestrator (n8n + OpenAI + Google + Freshdesk + Trello)
This automation simulates how Deer Designer can receive, enrich, classify, and route design briefs submitted by clients through a Google Form — using AI + automation + memory to streamline messy real-world workflows.

## 🛠 **Tools Used**
n8n: Visual automation orchestrator

OpenAI (GPT-3.5-TURBO): To rewrite, extract insights, and classify briefs

Google Forms & Sheets: Client request intake and memory storage

Freshdesk: Support ticket creation

Trello (via email): Task card creation

SMTP (Gmail): Email notifications and Trello integration


    A[Google Form → Google Sheets Trigger]
    B[Memory Rows (historical log)]
    C[Merge Sheets Input]
    D[Filter Memory by Email]
    E[OpenAI Prompt (with memory context)]
    F{OpenAI Output Valid?}
    G[Alert Error Email to Team]
    H[Edit Fields → Is Prod?]
    I[Skip Ticket/Card/Log]
    J[Create Freshdesk Ticket]
    K[Send Email to Trello]
    L[Send Summary Email to Team]
    M[Log to Google Sheets]

    A --> B --> C --> D --> E --> F
    F -- No --> G
    F -- Yes --> H
    H -- No --> I
    H -- Yes --> J --> K --> L --> M

## 🧠 **GPT Prompt Features**
The AI returns a structured JSON with:

cleaned_description: Rewritten version of the client input

missing_info: Clarifying questions or missing data

suggested_priority: Adjusted based on complexity + input

suggested_deadline: Estimated effort in days

task_type: Classified into categories (e.g., Social Post, Landing Page)

It also receives past requests from the same client as memory context to improve accuracy and consistency.

## 🔄 **Modes: Test vs Production**
A toggle (Set node: mode = "test" or "production") controls execution:

Test mode: Only runs AI processing

Production mode: Sends emails, creates tickets/cards, logs history

## ❌ **Error Handling**
If GPT fails to return a valid response, the system:

Skips routing

Sends a detailed error alert email to the team

## 🗂 **Log Register**
Each processed request is logged in Google Sheets with:

Timestamp

Client name + email

Cleaned description

Missing info

Task type

Suggested priority

Suggested deadline

## ✅ **Summary**
This solution demonstrates a scalable, smart design brief orchestrator that integrates AI and automation to improve operational efficiency, enrich data, and notify teams, all using low-code tools with best practices in modular design, memory, error handling, and logic switching.
