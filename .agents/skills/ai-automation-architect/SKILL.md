---
name: ai-automation-architect
description: >-
  Architect, build, test, and package professional-grade AI automations, n8n workflows, autonomous agent systems, and client delivery frameworks. Use when designing end-to-end automations, creating n8n blueprints, integrating LLMs with APIs and databases, or packaging AI solutions for business clients.
---

# AI Automation Architect & Systems Engineering Runbook

This skill equips the agent to act as a senior AI Automation Architect and Agency Lead. It provides operational blueprints for designing production n8n workflows, autonomous agents, data enrichment engines, and commercial client delivery.

## Core Architectural Principles

1. **Deterministic First, Probabilistic Second**: Never use an LLM for operations that can be resolved deterministically with standard code, regex, or direct API transformations. Use LLMs strictly for judgment, semantic extraction, synthesis, or creative generation.
2. **Idempotency & Deduplication**: Every automated workflow must be safe to rerun. Always check for existing records (by ID, hash, or primary key) before inserting or triggering downstream actions.
3. **Defensive Error Handling**: Always configure error triggers, retry policies with exponential backoff, and dead-letter queues or fallback alert channels (e.g., Slack / Telegram webhooks).
4. **Credential Isolation**: Keep all API keys, OAuth tokens, and secrets in environment variables or credential vaults. Never hardcode secrets in workflows or blueprints.

---

## Blueprint Development Workflow

### Step 1: Ingestion & Trigger Design
- **Webhooks**: Use HMAC validation or secret header tokens to verify incoming requests.
- **Polling / Cron**: When polling APIs, always maintain a persistent `last_processed_timestamp` or cursor state.
- **Event Filtering**: Discard irrelevant events as early as possible in the pipeline to conserve compute and API rate limits.

### Step 2: Data Normalization & Enrichment
- Sanitize and format data into a standardized JSON schema.
- Chain waterfall enrichment:
  - Step 2a: Query local cache or internal CRM/database.
  - Step 2b: Fallback to primary data provider (e.g., Apollo, Clearbit).
  - Step 2c: Fallback to secondary provider (e.g., Hunter, Dropcontact).

### Step 3: LLM Reasoning & Tool Invocation
- Use structured JSON outputs (via schema enforcement or Pydantic models).
- Inject few-shot examples into prompts for high-variance tasks.
- Enforce strict temperature control: `0.0 - 0.2` for classification/extraction, `0.7` for personalized copy.

### Step 4: Storage, CRM Sync & Downstream Dispatch
- Batch write operations where possible (Airtable, Notion, Postgres, HubSpot).
- Record an audit log containing execution ID, input payload hash, and outcome status.

---

## Detailed Playbook Reference

For advanced agent patterns, n8n node topologies, and prompt engineering frameworks, refer to:
- [Technical Architecture Playbook](./references/architecture-playbook.md)

