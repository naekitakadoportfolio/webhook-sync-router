<p align="center"><img src="assets/banner.svg" alt="Webhook Sync Router" width="100%"></p>

<p align="center">
<img src="https://img.shields.io/badge/stack-Apps_Script_·_Webhooks_·_REST_API-14384E?style=flat-square">
<img src="https://img.shields.io/badge/data-fictional-89CDE7?style=flat-square">
<a href="https://sider.ai/agents/web-creator/share/695ea81100a621619985fdfb"><img src="https://img.shields.io/badge/Portfolio-Nae_Kitakado-1D4C93?style=flat-square"></a>
</p>

<p align="center"><a href="https://naekitakadoportfolio.github.io/webhook-sync-router/"><img src="https://img.shields.io/badge/%E2%96%B6%20Try%20the%20live%20demo-14384E?style=for-the-badge" alt="Live demo"></a></p>

# Webhook Sync Router

Simulates a production webhook router that keeps parent tasks and subtasks in sync. Fire events, simulate rate limits, replay duplicates and toggle routes between LIVE and SHADOW to see how it stays safe.

> **Portfolio rebuild.** This is a from-scratch recreation of a production system I designed and run, rebuilt with **fictional data** and no client names, code or branding. The live demo runs entirely in the browser.

## The problem
Third-party automation tools billed per task, and status changes on creative production tasks had to fan out to every subtask. Three no-code workflows handled this, consuming tens of thousands of billable tasks a month and occasionally looping or double-firing.

## Impact in production
Replaced the no-code workflows and metered platform automations with one webhook router of 10 routes (9 live, 1 in shadow). Writes became idempotent, failures retry automatically, and every route ships with self-test assertions.

## What it demonstrates
| Capability | How |
|---|---|
| Event-driven webhook routing | One endpoint, `?route=` dispatch to handler per event type |
| Idempotency | Event-ID dedup cache blocks double-fires |
| Resilience | 429 handling, retry queue with exponential backoff |
| Safe rollout | Per-route LIVE / SHADOW toggle with parity logging |
| Cost control | Counts metered actions avoided |
| Observability | Ledger of every event, write and retry |

## Production architecture
Webhook (task status updated) → Apps Script `doPost` router → route handler → REST API writes. Config in Script Properties, ledger and retry queue in Sheets, time-driven trigger drains retries, Slack alert on dead letters.

## Try it
Open the **[live demo](https://naekitakadoportfolio.github.io/webhook-sync-router/)** or run `index.html` locally. No install needed.

---
<p align="center"><sub>Built by <b>Nae Kitakado</b>, AI Automation Consultant · <a href="https://www.linkedin.com/in/nae-k-203194265">LinkedIn</a> · <a href="https://sider.ai/agents/web-creator/share/695ea81100a621619985fdfb">Portfolio</a> · open to retainer &amp; part-time consulting</sub></p>
