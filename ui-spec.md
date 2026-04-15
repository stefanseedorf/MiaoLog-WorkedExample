# MiaoLog — UI Specification

<!-- WHAT IS A UI SPEC?
A UI spec (User Interface Specification) describes what the app looks like and
how it behaves. A developer uses it to make decisions about colour, layout, and
interaction without guessing. An AI coding agent uses it as context to generate
code that matches your visual style — not a generic default. -->

This document covers: app identity, colour system, typography, layout rules,
key screens, and interaction patterns.

---

## App identity

MiaoLog has one job: make a small daily task (logging a cat feeding) feel
effortless and even enjoyable. The app should feel like something a student
would actually want to open — warm, personal, a little playful.

**Not:** Corporate, clinical, grey, dense with small text, form-heavy
**Yes:** Warm orange tones, generous white space, emoji used purposefully,
         instant feedback on every action, a sense of personality

The name 喵Log combines a Chinese onomatopoeia (喵 = meow) with an English word.
This bilingual identity reflects the student community it serves.
The interface can be English-first, but cat names and health notes will often be Chinese.

---

## Colour system

Define these once in `src/styles/main.css`. Vant reads its own variables automatically;
your custom components use the `--color-*` tokens.

```css
:root {
  /* ── Brand ── */
  --van-primary-color:         #f97316;  /* orange — warm, energetic, food-associated */
  --van-primary-color-light:   #fff7ed;  /* light orange tint for backgrounds */
  --van-primary-color-end:     #ea580c;  /* slightly darker orange for gradients */

  /* ── Status colours ── */
  --color-success:    #4ade80;  /* fed today, confirmation messages */
  --color-warning:    #fbbf24;  /* Watch health status, double-feed warning */
  --color-danger:     #f87171;  /* Urgent health status, error states */

  /* ── Surfaces ── */
  --color-bg:         #fffbf5;  /* page background — slightly warm white, not pure #fff */
  --color-surface:    #ffffff;  /* cards, modals, form fields */
  --color-border:     #e7e5e4;  /* card borders, dividers */

  /* ── Text ── */
  --color-text:       #1c1917;  /* primary text — warm black, not pure #000 */
  --color-text-muted: #78716c;  /* timestamps, secondary labels, hints */
  --color-text-on-primary: #ffffff;  /* white text on orange buttons */

  /* ── Shape ── */
  --van-border-radius-md:  12px;    /* cards, form fields */
  --van-border-radius-lg:  20px;    /* bottom sheets, modals */
  --radius-full:           9999px;  /* pill badges, avatar rings */
}
```

**Colour usage rules:**
- Orange (`--van-primary-color`) is used only for the primary action on each screen.
  Not for decorative elements. One orange thing per screen guides the eye to the next step.
- Green means "done / safe / fed". Red means "urgent / error". Yellow means "check this".
- Background is warm off-white (`#fffbf5`), not pure white — reduces screen glare on mobile.

---

## Typography

<!-- Google Fonts is blocked in mainland China. Use fonts.loli.net, which is a Google
     Fonts mirror that is accessible without a VPN. -->

**Primary font: Nunito**

Nunito is a rounded, friendly sans-serif. It reads clearly at small sizes on a phone
screen and has a slightly warm character — not corporate or cold.

```css
/* In index.html <head> — load before any content renders */
<link rel="preconnect" href="https://fonts.loli.net">
<link href="https://fonts.loli.net/css2?family=Nunito:wght@400;500;600;700&display=swap" rel="stylesheet">
```

**Fallback stack for Chinese characters:**

```css
font-family: 'Nunito', 'PingFang SC', 'Noto Sans CJK SC', system-ui, sans-serif;
```

PingFang SC is the system font on iOS and macOS; Noto Sans CJK SC covers Android.
Both display Chinese characters correctly. The Nunito fallback ensures Latin characters
look right even if the font fails to load.

**Type scale:**

| Use | Size | Weight | Example |
|---|---|---|---|
| Timestamps, meta labels | 12px | 400 | "2 hours ago" |
| Body text, list items | 14px | 400 | "Dry food · 30g" |
| Form labels, card content | 16px | 500 | "Food type" |
| Section headings | 18px | 600 | "Health Notes" |
| Page title, cat name | 22px | 700 | "Orange 🐱" |

---

## Layout principles

**Mobile-first.** Design for a 390px wide screen (iPhone 14 standard).
Test on a wide screen last, not first.

**Generous tap targets.** Every button, card, and list item must be at least 44px tall.
This is the Apple Human Interface Guideline minimum — fingers are not pixels.

**One primary action per screen.** The orange button tells the user what to do next.
If two things are equally orange, nothing stands out.

**Bottom navigation, not top navigation.** On a phone, thumbs reach the bottom
more easily than the top. Use Vant's `van-tabbar` for the main navigation.

**Safe areas.** On iPhones with a notch or Dynamic Island, add padding at the top
and bottom using `padding-top: env(safe-area-inset-top)`.
Vant handles this automatically for its own components.

---

## Emoji system

MiaoLog uses emoji as functional icons — no icon library to install or import.

| Emoji | Meaning | Where used |
|---|---|---|
| 🐱 | Cat (generic / placeholder) | Cat list header, empty state |
| 🐟 | Feeding / log entry | Log button, feeding list items |
| 💊 | Health note | Health tab, health section header |
| ✅ | Fed today | Cat card status badge |
| ⚠️ | Watch health status | Cat card badge, health note |
| 🚨 | Urgent health status | Cat card badge, alert banner |
| ⏰ | Time / last fed | Timestamp label |
| 👤 | Volunteer name | "Fed by" label |
| 📊 | Coordinator dashboard | Tab bar icon |

**Rule:** one emoji per label, always paired with visible text.
Do not use emoji for decoration — only for meaning.
This makes the interface readable even if the emoji renders differently on different phones.

---

## Key screens

### Screen 1 — Cat list (home)

**Purpose:** Let a volunteer see all cats at a glance and find the one they need quickly.

**Layout:**

```
┌─────────────────────────────────────┐
│ 喵Log                    [Wed Apr 9] │  ← simple status bar, date top right
├─────────────────────────────────────┤
│ ╔═══════════════════════════════╗   │
│ ║ 🚨 Mini — Urgent health note  ║   │  ← Urgent cards always at top, red border
│ ║ Calico · Canteen  · Not fed   ║   │
│ ╚═══════════════════════════════╝   │
│ ┌───────────────────────────────┐   │
│ │ 🐱 Orange            Not fed  │   │  ← Unfed cats second, default border
│ │ Tabby · North Campus          │   │
│ └───────────────────────────────┘   │
│ ┌───────────────────────────────┐   │
│ │ 🐱 Spot           ✅ Fed 2h   │   │  ← Fed cats last, success colour
│ │ Grey · South Library    ⚠️    │   │  ← Watch badge alongside fed status
│ └───────────────────────────────┘   │
│                                     │
│   [🐱 Cats]  [🐟 Log]  [📊 Status] │  ← Vant tab bar — fixed at bottom
└─────────────────────────────────────┘
```

**Vant components to use:** `van-cell-group`, `van-cell`, `van-badge`, `van-tabbar`

---

### Screen 2 — Log feeding (tab bar middle)

**Purpose:** Record a feeding in under 30 seconds.
The middle tab bar button is the primary daily action — make it fast.

**Layout:**

```
┌─────────────────────────────────────┐
│ ← Log a feeding                     │  ← back button (Vant van-nav-bar)
├─────────────────────────────────────┤
│                                     │
│  Cat                                │
│  ┌─────────────────────────────┐    │
│  │ Orange 🐱              ▼   │    │  ← van-field with van-picker
│  └─────────────────────────────┘    │
│                                     │
│  Food type                          │
│  ┌─────────────────────────────┐    │
│  │ Dry food               ▼   │    │  ← dropdown: Dry / Wet / Treats
│  └─────────────────────────────┘    │
│                                     │
│  Amount (grams)                     │
│  ┌─────────────────────────────┐    │
│  │ 30                          │    │  ← number input
│  └─────────────────────────────┘    │
│                                     │
│  Note (optional)                    │
│  ┌─────────────────────────────┐    │
│  │                             │    │  ← text area, 2 rows
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  🐟  Log feeding            │    │  ← PRIMARY ACTION: full-width, orange, 52px
│  └─────────────────────────────┘    │
│                                     │
│   [🐱 Cats]  [🐟 Log]  [📊 Status] │
└─────────────────────────────────────┘
```

After submit: green banner slides in from top — "✓ Feeding logged for Orange"
Banner auto-dismisses after 2.5 seconds. Screen returns to cat list.

**Vant components:** `van-nav-bar`, `van-form`, `van-field`, `van-picker`, `van-button`

---

### Screen 3 — Cat profile

**Purpose:** Show the full history for one cat. Entry point: tap a cat card on home.

**Layout:**

```
┌─────────────────────────────────────┐
│ ←  Orange 🐱                        │  ← van-nav-bar with cat name
├─────────────────────────────────────┤
│                                     │
│     🐱                              │  ← large emoji or photo, centered
│   Orange                            │  ← cat name, 22px bold
│   Tabby · North Campus  ✅ Fed 2h   │  ← location + today's status
│                                     │
├──────────────────┬──────────────────┤
│  🐟 Feedings     │  💊 Health       │  ← van-tabs
├──────────────────┴──────────────────┤
│                                     │
│  🐟 Dry food · 30g                  │  ← feeding entry
│  👤 Li Wei · ⏰ 2 hours ago        │
│  ─────────────────────────────────  │
│  🐟 Wet food · 50g                  │
│  👤 Chen Mei · ⏰ Yesterday 6pm    │
│                                     │
│   [🐱 Cats]  [🐟 Log]  [📊 Status] │
└─────────────────────────────────────┘
```

**Vant components:** `van-nav-bar`, `van-tabs`, `van-list`, `van-cell`

---

### Screen 4 — Coordinator status

**Purpose:** One-screen overview of all cats' feeding status for today.

**Layout:**

```
┌─────────────────────────────────────┐
│ 📊 Today's status    Wed Apr 9      │
├─────────────────────────────────────┤
│  Not fed today (2)                  │  ← section header, red text
│  ┌───────────────────────────────┐  │
│  │ 🚨 Mini  ·  Not fed  · Urgent │  │  ← urgent first
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ 🐱 Orange  ·  Not fed        │  │
│  └───────────────────────────────┘  │
│                                     │
│  Fed today (1)                      │  ← section header, green text
│  ┌───────────────────────────────┐  │
│  │ 🐱 Spot  ·  ✅ Fed 2h ago    │  │
│  └───────────────────────────────┘  │
│                                     │
│                  ↓ Pull to refresh  │
│   [🐱 Cats]  [🐟 Log]  [📊 Status] │
└─────────────────────────────────────┘
```

**Vant components:** `van-pull-refresh`, `van-list`, `van-cell`, `van-tag`

---

## Interaction patterns

### Tap feedback
Every tappable element gives instant visual feedback.
Vant buttons do this automatically. For custom tappable elements:
```css
.tappable:active {
  transform: scale(0.97);
  transition: transform 0.1s ease-out;
}
```

### Form submission
While the form is submitting to Supabase, the submit button shows a loading spinner.
Vant's `van-button` has a `loading` prop for this — set it to `true` on submit, `false` on complete.

### Confirmation banner
After a successful action (log saved, note added), a green banner slides in from the top:

```css
.confirm-banner {
  background: var(--color-success);
  color: #fff;
  padding: 12px 16px;
  font-weight: 600;
  animation: slide-down 0.25s ease-out;
}
@keyframes slide-down {
  from { transform: translateY(-100%); opacity: 0; }
  to   { transform: translateY(0);     opacity: 1; }
}
```

Auto-dismiss after 2500ms.

### Double-feed warning
A Vant `van-dialog` (modal) appears if the same cat was fed in the last 10 minutes.
Two buttons: "Cancel" (secondary) and "Log anyway" (orange, primary).
This is an interruption — use it only when the data is genuinely at risk of duplication.

### Page transitions
Vue Router slide transition — new page slides in from the right, back slides from the left.
This makes the app feel like a native app, not a website reloading.

```css
.slide-left-enter-active,
.slide-left-leave-active {
  transition: transform 0.28s ease-out;
}
.slide-left-enter-from { transform: translateX(100%); }
.slide-left-leave-to   { transform: translateX(-30%); opacity: 0; }
```

---

## Empty states

Every list screen needs an empty state — a message for when there is no data yet.
Do not leave a blank screen. Empty states reduce confusion and suggest the next action.

| Screen | Empty state message |
|---|---|
| Cat list | "🐱 No cats added yet. Ask your coordinator to add cats to the group." |
| Feeding log | "🐟 No feedings logged today. Tap the Log tab to record a feeding." |
| Health notes | "💊 No health notes. If you notice something, add a note here." |
| Coordinator status | "✅ All cats are fed today!" (positive empty state when everything is done) |

---

## Accessibility checklist

- [ ] All buttons have an `aria-label` if they contain only an emoji or icon
- [ ] All form fields have a visible `<label>` element linked by `for` / `id`
- [ ] Text colour contrast ratio meets WCAG AA (4.5:1 for normal text)
- [ ] No information is conveyed by colour alone (add text label alongside status badge)
- [ ] Touch targets are at least 44 × 44px
- [ ] The app works when the phone is in large-text mode (no fixed-height text containers)
