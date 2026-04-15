# MiaoLog — Product Description

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

## The problem it solves

Before MiaoLog, the volunteer group used a WeChat group chat to confirm feedings.
Messages got buried. The coordinator had to scroll through days of chat history.
Health notes were forgotten. Cats were sometimes fed twice and sometimes not at all.

MiaoLog creates one shared log — one place to write, one place to check.

## Who uses it

| Role | What they do in the app |
|---|---|
| **Volunteer feeder** | Opens the app, finds their cat, logs a feeding in under 30 seconds |
| **Group coordinator** | Sees feeding status for all cats today, spots health alerts, contacts volunteers |

There are approximately 20 volunteers and 1–2 coordinators per group.
Most are undergraduate students. Most use the app on an iPhone or Android phone.

## Constraints — things that shape every decision

**Must work without a VPN.**
All tools must be accessible from a Chinese university network.
No Firebase, no Google APIs, no tools that require a VPN to reach.

**Mobile browser only.**
Volunteers are walking around campus. They will not download an app.
The product opens as a URL. It works in Safari, Chrome, and the WeChat in-app browser.

**Free tier.**
The team has no budget. All tools must have a free tier that is enough for
approximately 20 active users and a few hundred records per week.

**Chinese and English.**
Interface text can be in English. Cat names and health notes will often be in Chinese.
The app must display Chinese characters correctly.

## What MiaoLog is NOT

- Not a full veterinary record system (no medical history, no adoption tracking)
- Not a messaging app (volunteers still use WeChat to communicate)
- Not a desktop app (desktop is a secondary consideration; phone comes first)
- Not a public website (only registered volunteers can write data)
