
# Architecture

## Overview

The AI Ops Request Triage & Routing workflow automatically analyzes incoming operational requests, determines their category and urgency, validates the AI response, and routes the request to the appropriate team.

## Workflow

Incoming Request
        |
        v
Input Validation
        |
        v
AI Classification
        |
        v
Structured JSON Output
        |
        v
JSON Parsing / Validation
        |
        v
Routing Logic
   /       |       \
 IT    Operations   Support
   \       |       /
        |
        v
Notification / Action
        |
        v
Human Review when Required

## AI Classification

The LLM receives the incoming request and returns a structured response containing:

- Category
- Urgency
- Confidence score
- Human-review requirement
- Summary
- Sentiment
- Extracted information
- Recommended team
- Recommended action

The workflow uses structured output rather than relying on free-form AI responses.

## Validation

The AI response is parsed and validated before downstream routing.

This prevents malformed or unexpected model output from being passed directly into later automation steps.

## Routing

Routing decisions are based on the structured classification.

Examples include:

- IT-related requests → IT support
- Operational requests → Operations
- Support-related requests → Support
- High-risk or uncertain requests → Human review

## Human Review

Requests can be flagged for human review when the AI determines that additional human intervention is required.

This keeps the AI responsible for classification and routing while preserving a human decision point for cases that should not be handled automatically.

## Design Principles

- Structured AI output
- Validation before downstream actions
- Conditional routing
- Human-in-the-loop escalation
- Modular workflow design
- Clear separation between classification and execution
- No real customer data in this repository
