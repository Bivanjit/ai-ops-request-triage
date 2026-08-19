
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
