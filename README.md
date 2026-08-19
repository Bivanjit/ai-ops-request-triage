# AI Ops Request Triage & Routing


> AI-powered operational request classification and routing built with Make.


## Overview


This project automates the initial handling of incoming operational requests.


Instead of manually reviewing every request, determining its category and urgency, and deciding which team should handle it, the workflow uses an LLM to classify each request and return a structured result.


The structured result is validated and then used to route the request to the appropriate operational path.


## Problem


Operations teams often receive requests through forms, internal systems, email, or other channels.


Manual triage creates repetitive work:


- Reading every incoming request
- Identifying the request category
- Determining urgency
- Extracting important information
- Deciding which team should handle it
- Escalating uncertain requests


This workflow automates that initial decision layer.


## Solution


The automation receives an operational request through a webhook and processes it through a validation, classification, and routing pipeline.


The AI determines:


- Category
- Urgency
- Confidence score
- Human-review requirement
- Summary
- Sentiment
- Extracted information
- Recommended team
- Recommended action


The result is returned as structured JSON rather than unrestricted AI-generated text.


## Workflow


```text
Incoming Request
       ↓
Webhook
       ↓
Deduplication Check
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
Human Review When Required
```



## Key Features

- AI-powered request classification
- Urgency detection
- Confidence scoring
- Structured JSON output
- JSON parsing and validation
- Duplicate request detection
- Conditional routing
- Human-review flagging
- Team-specific routing
- Automated notifications
- Modular workflow architecture

## AI Classification

For every incoming request, the AI analyzes the request and produces a structured classification.
For every incoming request, the AI analyzes the request and produces a structured classification.
```

---

##The output includes:

Field	Purpose
category	Determines the type of request
urgency	Determines how urgently the request should be handled
confidence_score	Indicates confidence in the classification
requires_human_review	Flags requests requiring human intervention
summary	Provides a concise summary of the request
sentiment	Identifies the overall sentiment
extracted_information	Captures relevant information from the request
recommended_team	Determines the team that should handle it
recommended_action	Suggests the next operational action
Example

##Input
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
```

---
## Validation

The workflow does not pass unrestricted LLM output directly into downstream automation.

The AI response is parsed and validated before routing decisions are made.

This helps prevent malformed or unexpected model output from breaking downstream workflow logic.

## Deduplication

Incoming requests are checked for duplicate request IDs before continuing through the workflow.

This prevents the same request from being processed repeatedly when the same event is received more than once.

## Conditional Routing

After the AI response has been parsed and validated, the workflow uses conditional routing to determine the appropriate operational path.

The routing layer can use information such as:

- Request category
- Urgency
- Confidence
- Human-review requirement
- Recommended team

This allows the same workflow to support multiple operational paths without requiring separate workflows for every request type.

## Human-in-the-Loop

The workflow does not attempt to automate every decision blindly.

Requests can be flagged for human review when automated handling should not be trusted.

This creates a control point between AI classification and operational action.

## Architecture

The workflow separates the system into several logical stages:

1. Input handling
2. Duplicate detection
3. Input validation
4. AI reasoning
5. Structured data processing
6. Output validation
7. Conditional routing
8. Notification / action
9. Human escalation

This modular structure makes individual components easier to modify without redesigning the entire workflow.

## Repository Structure

```text
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
    ├── 01_full_workflow_architecture.png
    ├── 02_input_validation_and_deduplication.png
    ├── 03_ai_triage_structured_json.png
    ├── 04_human_review_routing.png
    ├── 05_deduplication_data_store.png
    ├── 06_execution_history_and_metrics.png
    └── 07_successful_run_history.png
