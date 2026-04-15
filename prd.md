# MiaoLog — Product Requirements Document

<!-- WHAT IS A PRD?
A PRD (Product Requirements Document) describes what the product must do at a
higher level than individual user stories. It answers three questions:
  1. What problem are we solving?
  2. What must the product do — and what must it NOT do?
  3. Who decides if it is done?

The AI agent reads this to understand scope. Without it, the agent fills gaps
with its own assumptions — usually wrong ones. -->

---

## Problem statement

Campus cat volunteers coordinate their feeding schedule through a WeChat group chat.
The current system has three problems:

1. **No shared record.** Messages get buried in chat history. There is no single place to check whether a cat has been fed today.
2. **No accountability.** The coordinator cannot see at a glance which cats have been fed and which have not.
3. **Health concerns get lost.** A volunteer notices something wrong with a cat and mentions it once. It disappears in the chat. Nobody follows up.

**The result:** cats are sometimes fed twice, sometimes not at all. Health concerns go unnoticed.

---

## Users

Full role definitions and permission rules are in `roles.md`.

| Role | Primary goal |
|---|---|
| **Volunteer Feeder** (~18 per group) | Log a feeding in under 30 seconds; check if a cat has already been fed today |
| **Group Coordinator** (1–2 per group) | See all cats' status at once; receive and act on health alerts |

---

## Core requirements

These are the things the product MUST do. Build these first. Do not move on to
optional features until every item here works end-to-end.

| # | Requirement | Role |
|---|---|---|
| R1 | Volunteer can log a feeding: cat, food type, amount, optional note | Volunteer |
| R2 | Volunteer can see when a cat was last fed, and by whom | Volunteer |
| R3 | If a cat was fed in the last 10 minutes, a warning appears before logging again | Volunteer |
| R4 | Volunteer can add a health note with severity: OK / Watch / Urgent | Volunteer |
| R5 | Urgent health notes show a visible alert on the cat's card — not just in the health tab | Volunteer + Coordinator |
| R6 | Coordinator can see all cats' feeding status for today on one screen | Coordinator |
| R7 | Cats not yet fed today appear at the top of the coordinator dashboard | Coordinator |
| R8 | The coordinator dashboard updates without a full page reload | Coordinator |

---

## Non-functional requirements

These apply to every feature, not just individual ones. The AI agent must apply
these as constraints when generating any code.

| Requirement | Detail |
|---|---|
| **Mobile-first** | Every screen is designed for a 390px wide phone viewport. Desktop is secondary. |
| **Speed** | A volunteer must be able to log a feeding in under 30 seconds from opening the app. |
| **Append-only data** | Feeding entries and health notes cannot be edited or deleted after saving. This is the audit trail. Do not add edit or delete UI unless explicitly asked. |
| **Free tier only** | All tools must have a free tier sufficient for ~20 active users and a few hundred records per week. No paid APIs. |
| **No authentication complexity** | Use Supabase Auth with email or magic link only. Do not implement custom authentication logic. |

---

## Out of scope

Do not build these. They are excluded deliberately. If a user story seems to require
one of these, ask for clarification before generating code.

| Out of scope | Reason |
|---|---|
| Messaging or push notifications between volunteers | WeChat handles communication — this app handles records only |
| Veterinary medical records, medication tracking, adoption | Outside the volunteer programme's responsibilities |
| Native mobile app (iOS / Android) | A mobile web app is sufficient; no App Store deployment |
| Admin tools for managing user accounts | Use Supabase Studio dashboard directly |
| Offline mode or data sync | The app requires an internet connection |
| Multi-group or multi-campus support | One group, one campus — no multi-tenancy needed |

---

## Definition of done (project level)

The product is ready to present when:

- [ ] All 8 core requirements (R1–R8) work end-to-end on a real mobile device
- [ ] At least 5 validation sessions are documented in the Validation Report
- [ ] The Tech Documentation describes the architecture, stack choices, and data model
- [ ] The app is deployed to a public URL that any assessor can open on their phone
