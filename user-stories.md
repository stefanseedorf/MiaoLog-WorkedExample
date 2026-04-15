# MiaoLog — User Stories

<!-- WHAT IS A USER STORY?
A user story describes one thing a real user needs to do.
Format: "As a [role], I want [action], so that [outcome]."
It focuses on the user's goal — not on how the code works. -->

<!-- WHAT ARE DONE CONDITIONS?
Done conditions (also called acceptance criteria) are the things that must be true
for a feature to count as finished. They are your checklist — and your stop signal
when working with an AI coding agent.
Paste them directly into your AI prompt: "Build this feature. Stop when all these
conditions are true." -->

---

## Story 1 — Log a feeding

**As a volunteer feeder,** I want to record who fed which cat, when, and how much,
so that other volunteers can check before feeding again.

**Done conditions:**
- [ ] Volunteer can select a cat from a list (name + photo or emoji)
- [ ] Volunteer can choose food type from a dropdown (Dry / Wet / Treats)
- [ ] Volunteer can enter amount in grams (number field, required)
- [ ] Volunteer can add an optional note (text field, max 200 characters)
- [ ] After tapping Submit, the feeding appears in the cat's log within 2 seconds
- [ ] A green confirmation message appears: "✓ Feeding logged for [cat name]"
- [ ] If the same cat was fed in the last 10 minutes, a warning appears before saving:
      "⚠️ [Cat name] was fed 8 minutes ago. Log anyway?"

---

## Story 2 — Check last feeding

**As a volunteer feeder,** I want to see when a cat was last fed before I feed it,
so that I do not feed it twice.

**Done conditions:**
- [ ] Volunteer can see the most recent feeding entry for any cat in under 5 taps from the home screen
- [ ] The entry shows: who fed (volunteer name), when (relative time — "2 hours ago"), what was given (food type and amount)
- [ ] If no feeding has been logged today, the entry shows "Not fed today" clearly in red
- [ ] If a feeding was logged within the last 2 hours, the card shows "Recently fed" in green

---

## Story 3 — Report a health note

**As a volunteer feeder,** I want to leave a note about a cat's health,
so that the coordinator knows something is wrong.

**Done conditions:**
- [ ] Volunteer can open any cat's profile and tap "Add health note"
- [ ] Volunteer selects severity: OK / Watch / Urgent (required)
- [ ] Volunteer writes a description (text field, required, max 500 characters)
- [ ] The note is saved with the current date and the volunteer's name
- [ ] Urgent notes show a red badge 🚨 on the cat's card in the home list
- [ ] Watch notes show a yellow badge ⚠️ on the cat's card
- [ ] OK notes are visible in the health tab but do not show a badge

---

## Story 4 — Coordinator daily status

**As a group coordinator,** I want to see the feeding status of all cats today,
so that I can make sure every cat has been fed before end of day.

**Done conditions:**
- [ ] Coordinator sees a list of all cats with today's feeding status: Fed / Not fed
- [ ] Cats that have NOT been fed today appear at the top of the list
- [ ] Cats with an Urgent health note appear above other unfed cats
- [ ] Coordinator can tap any cat to see its full feeding log and health notes
- [ ] The list updates with one tap (pull-to-refresh) — no manual page reload required
- [ ] If all cats are fed, a message shows: "✓ All cats fed today"

---

## Story 5 — Volunteer profile (stretch goal)

**As a volunteer feeder,** I want to see my own feeding history,
so that I can check how many sessions I have contributed this month.

**Done conditions:**
- [ ] Volunteer can see a list of their own feeding entries, newest first
- [ ] Each entry shows: cat name, date, food given
- [ ] A count shows total feedings this month: "You have logged 14 feedings this month"

*This story is a stretch goal. Build Stories 1–4 first.*
