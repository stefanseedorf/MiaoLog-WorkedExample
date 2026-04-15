# MiaoLog — User Roles

<!-- WHAT IS A USER ROLE?
A user role defines who uses the product and what they are allowed to do.
Defining roles before you build prevents mistakes — for example, building
a screen that any user can access when it should only be available to an administrator.
The AI agent reads this file to know what to allow and what to restrict. -->

Two roles use MiaoLog. Every feature belongs to one or both.

## Role overview

| Role | Who they are | Typical number per group |
|---|---|---|
| **Volunteer Feeder** | A student volunteer who feeds one or more campus cats | ~18 |
| **Group Coordinator** | A student who manages the group and monitors all cats | 1–2 |

---

## Volunteer Feeder

**Goal:** Complete the feeding task quickly and leave a clear record for other volunteers.

**Can do:**
- View the list of all cats and today's feeding status for each
- Log a feeding for any cat: food type, amount, optional note
- View the full feeding history for any cat
- Add a health note to any cat with a severity level: OK / Watch / Urgent
- View their own past feeding entries

**Cannot do:**
- Edit or delete any feeding entry or health note after saving — entries are permanent
- Access the coordinator dashboard
- Change a cat's profile (name, photo, location)
- See the full feeding history of other volunteers

---

## Group Coordinator

**Goal:** Confirm all cats are fed every day and act immediately on health alerts.

The coordinator is also a volunteer — they feed cats too. All Volunteer Feeder
permissions apply. The coordinator has additional access on top.

**Additional permissions:**
- Access the coordinator dashboard: feeding status for every cat today
- View all Urgent and Watch health alerts in one place
- View the full feeding history across all volunteers (not just their own)
- Edit cat profiles: name, photo, location, notes

**Cannot do:**
- Delete historical feeding records or health notes — the audit trail is permanent

---

## Rules for the AI agent

Apply these to every feature you build:

1. **Default to Volunteer Feeder permissions.** Any feature not listed under Coordinator is available to all users.
2. **Coordinator-only screens must check the role.** If `user.role !== 'coordinator'`, show a locked state — not an error, not a blank screen.
3. **The coordinator is also a volunteer.** Do not remove feeding or health note features from the coordinator view.
4. **Entries are append-only.** No editing or deleting after save. Do not add edit or delete buttons to feeding or health note lists.
5. **When in doubt about permissions, ask before generating.** Do not guess.
