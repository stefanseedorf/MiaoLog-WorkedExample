# MiaoLog — Product Requirements

<!-- WHAT IS THIS FILE?
This file describes what MiaoLog is, who uses it, and what it must do.
It is the main context file for your AI coding agent — read it first at the
start of every session. It answers:
  1. What problem are we solving?
  2. Who are the users and what are their goals?
  3. What must the product do — and what must it NOT do? -->

---

## What it is

MiaoLog (喵Log — 喵 means "meow" in Chinese) is a mobile web app
for the campus cat volunteer programme at XJTLU Suzhou.

Volunteers use it on their phones to record when they fed a campus cat
and to leave health notes. The group coordinator uses it to check which
cats have been fed today and to see any health alerts — all in one place.

<!-- WHAT IS A MOBILE WEB APP?
A mobile web app is a website designed to look and feel like an app on your phone.
Users open it in their browser (Safari, Chrome, or the WeChat browser) — no download needed.
It is different from a native app (like WeChat or TikTok) which must be installed. -->

---

## The problem

The volunteer group currently uses a WeChat group chat to confirm feedings.
This causes three specific problems:

1. **No shared record.** Messages get buried. There is no single place to check whether a cat has been fed today.
2. **No accountability.** The coordinator cannot see at a glance which cats are fed and which are not.
3. **Health concerns get lost.** A volunteer notices something wrong and mentions it once. It disappears in the chat.

The result: cats are sometimes fed twice, sometimes not at all. Health concerns go unnoticed.

---

## Users

Full role definitions and permission rules are in `user-roles.md`.

| Role | Primary goal | How many |
|---|---|---|
| **Volunteer Feeder** | Log a feeding in under 30 seconds; check if a cat has already been fed | ~18 per group |
| **Group Coordinator** | See all cats' status at once; act on health alerts | 1–2 per group |

Most users are undergraduate students on an iPhone or Android phone.

---

## Core requirements

These are the things the product MUST do. Build these before anything else.
Do not move on to optional features until every item here works end-to-end.

| # | Requirement | Role |
|---|---|---|
| R1 | Volunteer can log a feeding: cat, food type, amount, optional note | Volunteer |
| R2 | Volunteer can see when a cat was last fed, and by whom | Volunteer |
| R3 | If a cat was fed in the last 10 minutes, a warning appears before logging again | Volunteer |
| R4 | Volunteer can add a health note with severity: OK / Watch / Urgent | Volunteer |
| R5 | Urgent health notes show a visible alert on the cat's card — not just inside the health tab | Both |
| R6 | Coordinator can see all cats' feeding status for today on one screen | Coordinator |
| R7 | Cats not yet fed today appear at the top of the coordinator dashboard | Coordinator |
| R8 | The coordinator dashboard updates without a full page reload | Coordinator |

---

## Constraints

These apply to every feature. The AI agent must treat these as hard limits.

| Constraint | Detail |
|---|---|
| **Mobile-first** | Every screen is designed for a 390px wide phone viewport. Desktop is secondary. |
| **Speed** | A volunteer must be able to log a feeding in under 30 seconds from opening the app. |
| **Append-only data** | Feeding entries and health notes cannot be edited or deleted after saving. This is the audit trail. Do not add edit or delete UI unless explicitly asked. |
| **Runs in the browser** | No app to install. The product opens as a URL and works in Safari, Chrome, and the WeChat in-app browser. |
| **Free tier only** | All tools must have a free tier sufficient for ~20 active users and a few hundred records per week. |
| **Chinese text** | Cat names and health notes will often be in Chinese. The app must display Chinese characters correctly. |

---

## Out of scope

Do not build these. If a user story seems to require one of them, ask for clarification.

| Out of scope | Reason |
|---|---|
| Messaging or notifications between volunteers | WeChat handles communication — this app handles records only |
| Veterinary medical records, medication, adoption | Outside the volunteer programme's responsibilities |
| Native mobile app (iOS / Android) | Mobile browser is sufficient; no App Store deployment |
| Admin tools for managing user accounts | Use Supabase Studio dashboard directly |
| Offline mode or data sync | The app requires an internet connection |
| Multi-group or multi-campus support | One group, one campus for now |
| Public access | Only registered volunteers can write data |

---

## Definition of done

The product is ready to present when:

- [ ] All 8 core requirements (R1–R8) work end-to-end on a real mobile device
- [ ] At least 5 validation sessions are documented in the Validation Report
- [ ] The Technical Documentation describes the architecture, stack choices, and data model
- [ ] The app is deployed to a public URL that any assessor can open on their phone
