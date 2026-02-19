# System Design

## 1. Overview

The Agentic Personal AI Assistant is designed using a modular multi-agent architecture.  
The system separates responsibilities into independent workflows that communicate through structured routing.

The primary goal of the architecture is:

- Clear separation of responsibilities
- Error-safe task execution
- Contact validation before external actions
- Scalable workflow expansion

---

## 2. Architecture Style

This project follows a **Modular Multi-Agent Architecture**.

There are three main components:

1. Main Assistant (Orchestrator)
2. Email Agent (Communication Specialist)
3. Calendar Agent (Scheduling Specialist)

Each agent is implemented as an independent n8n workflow.

---

## 3. Main Assistant (Orchestrator Layer)

The Main Assistant is responsible for:

- Receiving input from Telegram (text or voice)
- Transcribing voice messages
- Using OpenAI for reasoning and intent detection
- Routing tasks to appropriate sub-agents
- Verifying contact information before execution

### Responsibilities

- Input handling
- Intent classification
- Tool selection
- Workflow delegation
- Memory management

This layer ensures that no email or calendar action is executed without proper validation.

---

## 4. Email Agent

The Email Agent handles all email-related operations.

### Capabilities

- Send emails
- Create email drafts
- Read multiple emails
- Fetch contact information from Google Sheets

### Design Principle

Before sending an email:
1. Contact name is validated via Google Sheets.
2. Email ID is retrieved from the database.
3. Gmail API is used only after verification.

This prevents:
- Sending emails to incorrect addresses
- Using fake or assumed email IDs
- Execution errors

---

## 5. Calendar Agent

The Calendar Agent manages scheduling operations.

### Capabilities

- Create events
- Create events with attendees
- Retrieve events
- Automatically assign default 60-minute duration if not specified

### Design Logic

- If attendee is provided → use event with attendee tool
- If no attendee is specified → create standard event
- If time range is unclear → system assumes logical defaults

This ensures smooth scheduling without user friction.

---

## 6. Data Flow

Step-by-step execution flow:

1. User sends message via Telegram.
2. Main Assistant processes input.
3. If email/calendar action is required:
   - Contact Database is checked first.
4. Task is routed to:
   - Email Agent OR
   - Calendar Agent
5. Execution result is returned to the user.

---

## 7. Memory Handling

The system uses session-based memory to:

- Maintain conversation context
- Handle follow-up questions
- Improve response consistency

Each Telegram user has an isolated session.

---

## 8. Error Handling Strategy

The system avoids unsafe execution by:

- Mandatory contact verification
- No fake email generation
- Structured tool routing
- Controlled workflow execution

If contact is not found:
- The system stops execution
- The user is notified

---

## 9. Scalability

The architecture is scalable.

New agents can be added for:

- Task management
- CRM integration
- Slack integration
- WhatsApp integration
- File management
- CRM automation

Because of modular design, each new capability can be implemented as a separate workflow without modifying the core architecture.

---

## 10. Design Philosophy

This project demonstrates:

- Agentic workflow orchestration
- Tool-based reasoning
- Modular automation design
- Safe execution principles
- Practical real-world AI integration

The system is designed not just as an automation script, but as a structured AI-powered orchestration platform.
