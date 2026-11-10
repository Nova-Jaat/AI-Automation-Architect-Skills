# Production Delivery Standard Operating Procedure (SOP)

This SOP details the exact execution checklist from client signing to final handover, ensuring zero post-launch bugs and maximum client satisfaction.

---

## Phase 1: Client Onboarding & Access Gathering (Day 1 - 2)
1. **Welcome Email & Form**:
   - Send onboarding intake form requesting:
     - Primary and backup technical contact info.
     - Brand guidelines, tone of voice samples (if content/copy automations).
     - Test accounts / scoped API keys.
2. **Credential Security**:
   - Never collect passwords via plain email.
   - Use password managers (1Password / Bitwarden share links) or request limited-permission API tokens with read/write access strictly to the target workspaces.
3. **Internal Project Setup**:
   - Create client directory in agency workspace (`/clients/[client_name]/`).
   - Initialize Git repository or versioned n8n instance.

---

## Phase 2: Build & Staging Sprint (Days 3 - 7)
1. **Mock Data Testing**:
   - Never test initially on live production databases.
   - Generate a batch of 10-20 synthetic test leads/records with edge cases:
     - Missing email fields.
     - International phone number formats.
     - Special characters / emojis in names.
     - Invalid domains.
2. **Deterministic Step Verification**:
   - Verify every JSON transformation produces expected typed values.
3. **LLM Evaluation & Temperature Tuning**:
   - Run prompts against 10 diverse examples.
   - Measure failure rate (hallucinations, refusal to follow JSON structure, formatting errors).
   - Add system guardrails and fallback values for empty responses.

---

## Phase 3: Integration & End-to-End Testing (Days 8 - 10)
1. **Sandbox / Staging Deployment**:
   - Connect to client's sandbox CRM environment or a staging Airtable table.
   - Trigger 5 live webhook events.
   - Validate timestamps, tag assignments, and notification alerts.
2. **Error Boundary & Alert Testing**:
   - Intentionally trigger a failed API call (e.g., provide bad token or invalid email).
   - Verify that the error node catches the failure, sends an alert to the developer Slack channel, and does not crash the server.

---

## Phase 4: Production Go-Live & Client Handover (Days 11 - 12)
1. **Cutover to Production**:
   - Switch webhook endpoints to live production URLs.
   - Monitor the first 50 live events in real-time.
2. **Client Handover Meeting (45-60 min)**:
   - Walk through the visual map of how data moves.
   - Show where leads land and how their team interacts with the system.
   - Deliver the Client User Guide & Loom walkthrough recording.
3. **Retainer Transition Pitch**:
   - Provide the 14-day warranty period.
   - Transition seamlessly into the ongoing maintenance & optimization retainer.

