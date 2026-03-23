# Sentry Retell — Miss Dawn QSC Dispatch

Retell AI conversation flow and agent configuration for **Miss Dawn**, the QSC AI dispatcher.

## Overview

Miss Dawn is a voice AI dispatcher for Quality Service Company (QSC) field technicians. She handles:

- **Post-job debriefs** — 8-question structured debrief with silent coaching flags
- **Help desk lookups** — pricebook, schedule, customer, equipment, invoice, estimate
- **Escalations** — flags issues for office follow-up via ServiceTitan tasks

## Architecture

```
Retell AI (Miss Dawn agent)
  └── Conversation Flow (5 nodes)
        ├── Greeting → identify tech by caller ID
        ├── Help Desk → 7 lookup tools
        ├── Job Debrief → 8 questions + save + escalate
        ├── Escalate → flag for office
        └── End Call
  └── 10 Custom Tools → Taylor AI Worker (Cloudflare)
        ├── /api/quinn/identify-tech
        ├── /api/quinn/appointments
        ├── /api/quinn/job
        ├── /api/quinn/customer-search
        ├── /api/quinn/pricebook
        ├── /api/quinn/equipment
        ├── /api/quinn/invoice
        ├── /api/quinn/estimate
        ├── /api/quinn/save-debrief
        └── /api/quinn/escalate
```

## Files

| File | Description |
|------|-------------|
| `agent.json` | Retell agent settings (voice, model, keywords, post-call analysis) |
| `conversation-flow.json` | Full conversation flow with nodes, edges, tools, and prompts |

## Agent Details

- **Agent ID:** `agent_042204c3bac2eecc1fa37d2ffa`
- **Flow ID:** `conversation_flow_e6fe1560f922`
- **Voice:** 11labs-Kathrine (en-US)
- **Model:** GPT-4.1-mini (cascading)
- **Max call:** 8 minutes
- **Webhook:** `taylor-ai.lpeluso.workers.dev/api/quinn/webhook`

## Deployment

Agent is managed via Retell AI dashboard and API. Backend endpoints run on the Taylor AI Cloudflare Worker.

## Status

- Agent + flow: configured
- Backend endpoints: deployed
- Phone number: not yet assigned
- Published: no
