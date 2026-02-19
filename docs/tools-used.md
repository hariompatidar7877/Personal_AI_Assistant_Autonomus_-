# Tools and Technologies Used

This project integrates multiple APIs and automation tools to create a modular AI-powered assistant.

---

## 1. n8n (Workflow Automation)

n8n is used as the core orchestration engine.

### Role in Project:
- Workflow automation
- Multi-agent routing
- Tool execution
- Credential management
- API integrations

Each agent (Main Assistant, Email Agent, Calendar Agent) is implemented as an independent n8n workflow.

---

## 2. OpenAI (GPT-4.1-mini)

OpenAI is used for:

- Natural language understanding
- Intent classification
- Tool selection
- Structured response generation
- Conversation memory handling

The model enables the system to interpret user instructions and decide which tool or agent to activate.

---

## 3. Gmail API

Used inside the Email Agent workflow.

### Capabilities:
- Send email
- Create draft
- Retrieve emails

Gmail OAuth2 authentication is required to securely connect to the user’s email account.

---

## 4. Google Sheets API

Used as a Contact Database.

### Purpose:
- Store contact names and email addresses
- Retrieve verified email IDs before sending emails
- Prevent incorrect or assumed email usage

This ensures safe and validated communication.

---

## 5. Google Calendar API

Used inside the Calendar Agent workflow.

### Capabilities:
- Create events
- Add attendees to events
- Retrieve events
- Handle time-based scheduling

If no duration is specified, the system automatically assumes a default duration of 60 minutes.

---

## 6. Telegram Bot API

Telegram acts as the user interface.

### Role:
- Accept text messages
- Accept voice messages
- Trigger workflows
- Deliver responses

Voice messages are transcribed before processing.

---

## 7. Memory Buffer (Session-Based Context)

The system uses session-based memory to:

- Maintain conversation continuity
- Handle follow-up queries
- Improve response relevance

Each Telegram user session is isolated to ensure clean context management.

---

## 8. OAuth2 Authentication

Secure authentication is implemented for:

- Gmail
- Google Sheets
- Google Calendar

This ensures secure API communication without exposing credentials.

---

## Summary

This project demonstrates real-world integration of:

- AI reasoning
- API orchestration
- Secure authentication
- Modular automation architecture

The combination of OpenAI with structured workflow automation enables safe, scalable, and intelligent task execution.
