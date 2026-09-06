# Telegram Gmail AI Assistant

A conversational AI assistant built with **n8n**, **Telegram**, **Gmail**, and **OpenAI**. Instead of jumping between an inbox and search bar, the user can ask questions about Gmail from Telegram and let an AI agent decide which Gmail tools to use.

## What it does

- Accepts natural-language requests through a Telegram bot
- Searches Gmail using standard Gmail queries
- Reads the full content of a selected email when needed
- Sends emails from Gmail through the assistant
- Maintains short-term conversation context per Telegram chat
- Replies directly in Telegram

Examples:

> Find the latest emails from recruiters.

> Show me emails from the last 7 days about interviews.

> Read the full email from this sender.

> Draft an email to the recruiter.

Before sending an email, the agent is instructed to show the recipient, subject, and message and request confirmation unless the user has already explicitly instructed it to send.

## Architecture

```text
Telegram
   ↓
Telegram Trigger
   ↓
AI Agent ───────────────┐
   │                    │
   ├── OpenAI Model     │
   ├── Conversation     │
   │   Memory           │
   ├── Gmail Search     │
   ├── Gmail Read       │
   └── Gmail Send       │
   ↓                    │
Reply on Telegram ◄─────┘
```

## Tech stack

| Technology | Role |
|---|---|
| n8n | Workflow orchestration and AI-agent tool routing |
| Telegram Bot API | Conversational interface |
| OpenAI GPT-4o-mini | Natural-language reasoning |
| Gmail | Search, read and send email operations |
| Conversation Memory | Maintains recent chat context |

## Project structure

```text
telegram-gmail-ai-assistant/
├── README.md
├── workflow/
│   └── telegram-gmail-ai-assistant.json
└── docs/
    └── README.md
```

## Setup

### 1. Create a Telegram bot

Create a bot with Telegram's BotFather and connect the bot credential in n8n.

### 2. Connect Gmail in n8n

Create/connect a Gmail OAuth2 credential with the required Gmail permissions.

### 3. Configure the OpenAI model

Connect an OpenAI-compatible credential in n8n and select `gpt-4o-mini` for the chat model.

### 4. Import the workflow

Import:

`workflow/telegram-gmail-ai-assistant.json`

Then select your own credentials for Telegram and Gmail.

### 5. Test

Open the Telegram bot and send a request such as:

`Find emails from the last 7 days about interviews.`

The agent can use the Gmail search tool, retrieve a full email when necessary, and reply in the same Telegram chat.

## Security

This repository intentionally does **not** contain live API keys, bot tokens, OAuth tokens, or private email data. Replace the credential placeholders with your own n8n credentials.

## Why I built it

I wanted to move beyond a simple chatbot and understand how an AI agent can interact with real tools. The interesting part of this project is not just generating text; it is the workflow around the model: deciding when to search, when to fetch an email, when to send, and how to preserve conversation context.

## Future improvements

- Add an approval workflow for higher-risk email actions
- Add email categorisation and priority detection
- Add scheduled summaries for unread or important emails
- Add richer logging and failure handling
- Add support for additional communication channels

## Workflow file

The n8n export is available at [`workflow/telegram-gmail-ai-assistant.json`](workflow/telegram-gmail-ai-assistant.json).
