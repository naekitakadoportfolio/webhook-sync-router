<p align="center"><img src="assets/banner.svg" alt="Webhook Sync Router" width="100%"></p>

<p align="center">
<img src="https://img.shields.io/badge/stack-Apps_Script_·_Webhooks_·_REST_API-14384E?style=flat-square">
<img src="https://img.shields.io/badge/data-fictional-89CDE7?style=flat-square">
<a href="https://sider.ai/agents/web-creator/share/695ea81100a621619985fdfb"><img src="https://img.shields.io/badge/Portfolio-Nae_Kitakado-1D4C93?style=flat-square"></a>
</p>

<p align="center"><a href="https://naekitakadoportfolio.github.io/webhook-sync-router/"><img src="https://img.shields.io/badge/%E2%96%B6%20Try%20the%20live%20demo-14384E?style=for-the-badge" alt="Live demo"></a></p>

# Webhook Sync Router

A multi-page operations console for an event-driven webhook router that keeps parent tasks and subtasks in sync across a project tool. It shows deduplication, per-route LIVE/SHADOW rollout, retries with backoff, dead letters, a searchable ledger and a built-in self-test suite.

> **Portfolio rebuild.** A from-scratch recreation of a production system I designed and run (Card sync engine). It uses **fictional data**, with no client names, code or branding.

## ✨ Features
- **Overview:** KPIs for events, writes, duplicates blocked, retry queue, dead letters and metered actions avoided
- **Event simulator:** fire any route, force HTTP 429, replay an event to prove idempotency, or send a burst of 10
- **Routes:** toggle each route LIVE ↔ SHADOW, with a parity warning before promotion
- **Tasks & subtasks explorer:** drill into any task, see subtask sync state and history, resync or simulate a desync, create tasks (fires the fill-fields route)
- **Retry & dead letters:** process the queue with exponential backoff; replay or discard dead letters
- **Ledger:** full event log with search and type filters
- **Self-tests:** a 7-assertion suite run against a snapshot, so tests never touch live data
- **Settings:** retries, backoff, simulated rate-limit %, and alert channel, all validated
- Light/dark theme, responsive layout, state saved in your browser, and one-click **Reset demo data**

## 🧭 Try it
1. Open *Event simulator*, tick **Force HTTP 429** and send → the event lands in *Retry & dead letters*
2. Click **Replay last event** → blocked by the dedup cache
3. Go to *Retry & dead letters* → **Process queue**
4. Open *Self-tests* → **Run all tests**

Open the **[live demo](https://naekitakadoportfolio.github.io/webhook-sync-router/)**.

## 🏗 Production architecture
| Layer | Production | This demo |
|---|---|---|
| Ingress | Apps Script `doPost` with `?route=` dispatch | In-page event simulator |
| Idempotency | Event-ID cache (CacheService) | `S.seen` list |
| Retries | Sheets queue + time-driven trigger | `S.retry` + Process button |
| Writes | Project tool REST API | In-memory task store |
| Alerts | Chat webhook | Activity log |
| Tests | Assurance.gs assertion suite | `runTests()` |

## 📁 Project structure
```
webhook-sync-router/
├── index.html        # built app (open this)
├── src/
│   ├── app.js        # state, views, business logic
│   └── app.json      # app config: nav, theme, storage key
├── assets/banner.svg
├── README.md
└── LICENSE
```

## 🚀 Run locally
No install needed. Open `index.html`, or:
```bash
python3 -m http.server 8000   # http://localhost:8000
```

## 🧩 Implementation notes
- `fire()` → dedup check → simulated rate limit → `apply()`
- `apply()` respects each route's mode; SHADOW records parity without mutating
- `drain()` retries with `backoff^tries` and moves events to dead letters after `maxRetries`
- `runTests()` snapshots state, runs assertions, then restores the snapshot

## 🗺 Roadmap
- Per-route rate limits
- Export ledger as CSV
- Signed webhook secret verification demo

---
<p align="center"><sub>Built by <b>Nae Kitakado</b>, AI Automation Consultant · <a href="https://www.linkedin.com/in/nae-k-203194265">LinkedIn</a> · <a href="https://sider.ai/agents/web-creator/share/695ea81100a621619985fdfb">Portfolio</a> · open to retainer &amp; part-time consulting</sub></p>
