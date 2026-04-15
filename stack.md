# MiaoLog — Technology Stack

<!-- WHAT IS A STACK?
A "stack" is the complete list of tools your app is built with — like a recipe listing
all the ingredients before you start cooking. Once you choose your stack, every feature
you build uses those same tools. Changing the stack mid-project is expensive. -->

---

## The big picture

MiaoLog has two parts:

```
┌──────────────────────────┐        ┌──────────────────────────┐
│  FRONTEND                │  ───▶  │  BACKEND                 │
│  What the user sees      │        │  Where data is stored    │
│  Runs on the user's phone│  ◀───  │  Runs on a remote server │
│  Built with Vue 3        │        │  Supabase (PostgreSQL)   │
└──────────────────────────┘        └──────────────────────────┘
```

<!-- WHAT IS A FRONTEND?
The frontend is everything the user can see and tap.
It runs inside the browser on the user's phone.
It is built with three web languages:
  - HTML: the structure (headings, buttons, forms)
  - CSS: the look (colours, fonts, layout)
  - JavaScript: the behaviour (what happens when you tap a button) -->

<!-- WHAT IS A BACKEND?
The backend is the part the user never sees.
It stores data permanently (cat records, feeding logs, health notes).
It runs on a server — a computer that is always on and connected to the internet.
When the frontend needs data, it sends a request to the backend.
The backend sends the data back.
We do not build our own backend — we use Supabase, which runs it for us. -->

<!-- WHAT IS AN API?
An API (Application Programming Interface) is the way the frontend talks to the backend.
Think of it as a menu in a restaurant. The menu tells you what you can order.
You do not need to know how the kitchen works — you just pick from the menu.
Supabase generates an API automatically from our database tables. -->

---

## Frontend

### Vue 3 — the JavaScript framework

Vue is a JavaScript framework. It lets us build the interface as reusable pieces called
**components**. A "cat card" is one component. A "feeding form" is another. We combine
components to build screens.

We chose Vue 3 because the team already knows it.
If your team knows React, use React. The ideas are the same.

**Docs:** https://vuejs.org

### Vant 4 — the mobile component library

Vant is a complete set of ready-made mobile interface elements: buttons, forms, tab bars,
bottom sheets, pull-to-refresh lists, loading spinners. Every element is designed for
a phone screen with large tap targets and smooth animations.

Vant is made by Youzan, a Chinese e-commerce company. It is fully accessible from
mainland China without a VPN and widely used in Chinese mobile apps.

We chose Vant because:
- It handles the hard parts of mobile UI (swipe gestures, safe areas on iPhone, bottom nav)
- It works without a VPN
- It saves significant time compared to building components from scratch

**Docs:** https://vant-ui.github.io/vant/

### CSS custom properties — the design token system

Rather than using a second CSS framework on top of Vant, we define our brand colours
and sizes as CSS variables (also called "design tokens"). Vant reads these variables
and applies them automatically.

```css
/* Define once in main.css — everything else inherits */
:root {
  --van-primary-color: #f97316;   /* orange — our brand colour */
  --van-background: #fffbf5;      /* warm off-white background */
  --van-border-radius-md: 12px;   /* rounded cards */
}
```

### Vite — the build tool

<!-- WHAT IS A BUILD TOOL?
Your source code (Vue files, CSS, images) cannot be loaded directly by a browser.
A build tool "compiles" it — bundles all the files together and optimises them
so the browser can load the app quickly.
Vite also runs a local preview server so you can test on your laptop before deploying. -->

Vite is the standard build tool for Vue 3 projects. It is fast and requires
almost no configuration.

---

## Backend

### Supabase — database and API

<!-- WHAT IS A DATABASE?
A database stores data permanently and lets you search it quickly.
Think of it as a set of spreadsheets — each "table" is one spreadsheet.
MiaoLog has tables for: cats, feedings, health_notes, volunteers.
Unlike a real spreadsheet, a database can handle thousands of simultaneous users
and can link tables together (a feeding row links to a cat row and a volunteer row). -->

Supabase gives us:

| What | What it means |
|---|---|
| **PostgreSQL database** | A powerful table-based data store — cats, feedings, health notes |
| **Auto-generated REST API** | The frontend can read and write data without any server code |
| **Row-Level Security (RLS)** | Rules that control who can see or change which rows |
| **Realtime** | The frontend can subscribe to changes — useful for the coordinator dashboard |
| **Auth (optional)** | Handles volunteer login without us writing authentication code |

We chose Supabase because:
- Accessible from mainland China on a normal university network
- Free tier is enough (500 MB database, unlimited API requests on the free plan)
- No server code to write — the API is generated automatically
- The dashboard is easy to use for non-developers (useful for the coordinator)

**Docs:** https://supabase.com/docs

### Data model (simplified)

```
cats
  id · name · photo_url · location · notes

volunteers
  id · name · wechat_id · role (feeder | coordinator)

feedings
  id · cat_id → cats · volunteer_id → volunteers
  food_type · amount_g · note · created_at

health_notes
  id · cat_id → cats · volunteer_id → volunteers
  severity (ok | watch | urgent) · description · created_at
```

<!-- WHAT IS A DATA MODEL?
A data model is a diagram or list that shows what information you store and
how the pieces connect. An arrow (→) means "links to another table".
For example, a feeding row contains cat_id — this links it to the correct cat in the cats table.
You do not store the cat's name in the feeding row — you store the cat's ID,
then look up the name when you need it. This avoids duplication. -->

---

## Hosting

### Vercel — frontend deployment

<!-- WHAT IS DEPLOYMENT?
Deployment means putting your finished app on a server so anyone with the link can open it.
Before deployment, only you can see the app running on your laptop.
After deployment, it is public (or password-protected) at a URL like miaolog.vercel.app. -->

Vercel hosts the frontend (the HTML, CSS, and JavaScript files the browser loads).
It connects to our GitHub repository. Every time we push code to `main`, Vercel
builds and deploys automatically. The URL updates within 30 seconds.

We chose Vercel because:
- Free tier with no credit card
- Automatic deploys from GitHub
- Fast global CDN (works well from China)

---

## Summary

| Layer | Tool | Why |
|---|---|---|
| Frontend framework | Vue 3 | Team knows it |
| Mobile components | Vant 4 | Mobile-first, China-accessible, saves build time |
| Styling / branding | CSS custom properties | Theme Vant without a second framework |
| Build tool | Vite | Fast, works with Vue 3, near-zero config |
| Database + API | Supabase | Works in China, free, no server code needed |
| Hosting | Vercel | Free, auto-deploys from GitHub |
