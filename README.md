
# AI Ops Request Triage & Routing

An AI-powered operations request triage and routing workflow built with Make.

## Overview

This workflow automates the initial handling of incoming operational requests.

Instead of manually reading every request, determining its category and urgency, and deciding where it should go, the workflow uses an LLM to classify the request and return a structured result.

The structured result is then validated and used to route the request to the appropriate operational path.

## Workflow

```text
Incoming Request
       ↓
Input Validation
       ↓
AI Classification
       ↓
Structured JSON Output
       ↓
JSON Parsing / Validation
       ↓
Routing Logic
       ↓
Team / Action Routing
       ↓
Notification
       ↓
Human Review when Required

What the AI Determines

For each request, the AI produces:

Category
Urgency
Confidence score
Whether human review is required
Summary
Sentiment
Extracted information
Recommended team
Recommended action

The workflow uses structured JSON output instead of relying on free-form AI responses.

Key Features
AI-powered request classification
Structured JSON output
JSON parsing and validation
Confidence scoring
Urgency detection
Human-review flagging
Conditional routing
Team-specific notifications
Modular workflow structure
Example
Input
{
  "request_id": "REQ-001",
  "requester_name": "John Doe",
  "requester_email": "john@example.com",
  "request_text": "The company laptop is unable to connect to the internal network and I need access restored as soon as possible."
}
AI Output
{
  "category": "IT",
  "urgency": "HIGH",
  "confidence_score": 0.95,
  "requires_human_review": false,
  "summary": "User is unable to connect a company laptop to the internal network.",
  "sentiment": "neutral",
  "extracted_information": "Company laptop; internal network connection issue.",
  "recommended_team": "IT_SUPPORT",
  "recommended_action": "Investigate the laptop's network configuration and restore internal network access."
}
Why Structured Output Matters

LLM responses can be unpredictable when they are returned as unrestricted text.

This workflow constrains the AI response to a defined structure and parses the result before routing decisions are made.

That makes the downstream automation more predictable and easier to maintain.

Human-in-the-Loop

The workflow does not attempt to automate every decision blindly.

Requests can be flagged for human review when the AI determines that human intervention is required.

This provides a control point for cases where automated handling should not be trusted.

Repository Structure
ai-ops-request-triage/
│
├── README.md
│
├── blueprint/
│   └── make-blueprint.json
│
├── examples/
│   ├── sample-request.json
│   └── sample-output.json
│
├── docs/
│   └── architecture.md
│
└── screenshots/
Demo

A public Make scenario demonstrating the workflow:

https://us2.make.com/public/shared-scenario/eK7puRBBWuD/ai-ops-request-triage-routing

Blueprint

The blueprint/ directory contains a sanitized Make blueprint for the workflow.

Private connection information and workspace-specific configuration have been removed. Connections must be configured again when importing the blueprint into a Make environment.

Setup
Import blueprint/make-blueprint.json into Make.
Reconnect the required integrations.
Configure the required notification channels.
Configure the AI/API credentials.
Test the workflow with the sample request.
Verify the structured output and routing behavior.
Replace the demo input with the desired production trigger.
Important

This repository contains demonstration data only.

No real customer information, API keys, authentication tokens, or private workspace credentials should be committed to the repository.

Limitations

This is a portfolio demonstration of an AI-powered triage and routing workflow.

Production deployments should additionally consider:

authentication
rate limiting
retry handling
logging
monitoring
provider/API failures
data privacy
access control
production-specific error handling
Project Type

AI Automation
Workflow Automation
LLM Integration
Operations Automation
Make

### Then commit it.

After that, **don't add anything else yet**.

Next we'll tackle the part that makes the repo visually credible: **the screenshots**. We'll decide exactly which 4–5 screenshots to take from your actual Make workflow and where to put them.
