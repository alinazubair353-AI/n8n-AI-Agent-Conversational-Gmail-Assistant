# n8n-AI-Agent-Conversational-Gmail-Assistant

## 📌 Overview
An autonomous AI Agent built in n8n that can **send emails, read recent Gmail messages, run custom code, and remember conversation context** — all through natural language chat. Unlike a fixed-step workflow, this agent decides for itself which tool to use based on what the user asks.

## 🧠 How It Works
```
Chat Trigger (When chat message received)
        ↓
    AI Agent  ←→  Google Gemini Chat Model (reasoning engine)
        ↓
   ┌────┴────┬─────────────┬──────────────┐
Memory   Send Email    Get Many       Code Tool
(Simple)  in Gmail     Messages       (custom JS)
                        in Gmail
```
<img width="1365" height="669" alt="image" src="https://github.com/user-attachments/assets/b4e8091c-5095-4ebd-96d2-04612becc389" />

The AI Agent sits at the center and dynamically picks the right tool depending on user intent — no manual branching or IF/Switch logic required.

## ⚙️ Components

| Node | Role |
|---|---|
| **When chat message received** | Trigger — starts the agent on every new chat message |
| **Google Gemini Chat Model** | The "brain" — interprets intent and generates responses |
| **Simple Memory** | Remembers prior messages in the same session (e.g., user's name, earlier context) |
| **Send a message in Gmail** | Tool — composes and sends a new email |
| **Get many messages in Gmail** | Tool — retrieves recent emails from the inbox without needing a manual message ID |
| **Code Tool** | Tool — runs custom JavaScript logic the agent can call mid-conversation |

## 💬 Example Conversations

**Sending an email:**
> User: `send a test email to baigalina463@gmail.com`
> Agent: Composes and sends the email using the Gmail Send tool.

**Reading recent emails:**
> User: `gmail is aysh4503@gmail.com get many message`
> Agent: Fetches and summarizes recent messages — sender, subject, and snippet — without requiring a manual message ID.

**Using memory:**
> User: `what is my name and how much can I earn in AI?`
> Agent: Recalls the name from earlier in the conversation and answers using the Code Tool for the earnings estimate.

## 🛠️ Setup Requirements
- n8n (self-hosted)
- Google Cloud Console project with **Gmail API** enabled
- OAuth2 credentials (Client ID + Secret) for Gmail
- Google Gemini API key

## 🔑 Key Learnings
- The difference between a fixed workflow and a true **AI Agent** (the agent reasons and chooses tools itself)
- How **Tool sub-nodes** must be connected through the AI Agent's dedicated `Tool` port — not just placed on the canvas
- Why "Get a message" (single, by ID) is harder to use than "Get many messages" for conversational use cases — IDs aren't human-readable, but bulk retrieval works out of the box
- How **Memory** nodes give an agent multi-turn context awareness
- Debugging real n8n errors: OAuth consent/test users, API enablement, tool connection mismatches, and rate limits

## ✅ Status
Fully functional — agent can send mail, retrieve recent mail, hold context, and execute custom logic, all from a single chat interface.

## 📝 Note
This project was built as a hands-on assignment while self-learning AI automation and n8n.
