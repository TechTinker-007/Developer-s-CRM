# Changelog — Real Estate Builder CRM

The story of this app so far: from a bare lead list to a role-secured, real-time sales platform. Every phase below builds directly on the one before it — nothing was ripped out to get here.

---

## 🌱 Phase 1 — Foundation
*"Just get leads on a screen."*

- Basic lead list: name, phone number, locality
- Manual status field (no real pipeline yet)
- Single shared login, no roles, no backend — everything lived in the browser

**Standard at this point:** a glorified spreadsheet with a nicer font.

---

## 🌿 Phase 2 — Real Pipeline
*"Leads need a journey, not just a label."*

- Kanban-style board: **Open → Site Visited → Booked → Rejected**
- Rich lead detail added: configuration, budget tier, property type, sector, entry type
- Follow-up scheduling with date/time reminders
- Site-visit counter and per-lead notes/activity log

**Level up:** leads stopped being static rows and started having a life cycle.

---

## 🌳 Phase 3 — Channel Partner Intelligence
*"Real estate sales run on referrals — the CRM needed to understand that."*

- CP firm registration with multiple staff members per firm
- Per-lead lock-in period tied to a specific firm + staff member
- **Automatic conflict detection** — flags when a phone number is already locked with another Channel Partner, catching commission disputes before they happen
- Expired lock-ins surfaced automatically for follow-up/reassignment

**Level up:** the CRM started catching business problems before humans noticed them.

---

## 🔁 Phase 4 — Nothing Gets Lost
*"A rejected lead isn't a dead end, it's just paused."*

- Dead/rejected leads tracked separately with reason + timestamp
- One-click reassignment of a dead lead back into the active pipeline as a fresh Walk-in lead
- Logged Data page for reviewing historical activity across leads, firms, and dead leads

**Level up:** the funnel became reversible instead of one-way.

---

## 💰 Phase 5 — Beyond the Sale
*"Booking a lead is the middle of the story, not the end."*

- Booked leads convert into tracked **Members**
- Sale price, token amount, and loan amount recorded per member
- Monthly EMI schedule with paid/bounced installment tracking
- **Automatic penalty interest calculation** on late or bounced payments
- Free-text notes per member for loan status and documentation

**Level up:** the app followed the money all the way to loan closure, not just to "Booked."

---

## 📊 Phase 6 — Visibility at a Glance
*"If you can't see the pipeline, you can't run the business."*

- Dashboard with lead counts by status and conversion trends
- Calendar view with clickable follow-up pills
- Global search across leads, phone numbers, CP firms, and CP staff — with inline conflict warnings
- Sidebar filters: locality, property type, budget tier, entry type, CP firm/staff, date range, status
- Mobile-friendly Leads list view

**Level up:** from "check every card manually" to "answer any question in one glance."

---

## ⚡ Phase 7 — Real-Time, Multi-User
*"One team, one live pipeline — not five out-of-sync tabs."*

- Supabase Realtime wired in: leads, firms, dead leads, and members sync instantly across every connected user, no refresh needed
- Optimistic UI updates for instant feel
- Conflict-resolution notices when two people edit the same record at once

**Level up:** the CRM stopped being single-player.

---

## 🔐 Phase 8 — Actually Secure
*"Client-side role checks are a suggestion, not security."*

- Full migration to **Supabase Auth** — email/password sign-in, no client-side passwords
- Server-side `profiles` table as the single source of truth for identity and role
- Two enforced roles:
  - **CEO** — full access, including deleting leads, firms, staff, and members
  - **Sales** — day-to-day operational access, no delete rights
- **Row Level Security (RLS)** enforced at the database layer, so permissions can't be spoofed from the browser — even with devtools open
- Delete actions routed through guarded Postgres functions rather than raw client deletes

**Level up:** from "the UI hides the delete button" to "the database itself refuses the request."

---

## ✨ Where It Stands Now

A single-file, no-bundler React app that:
- Runs an entire real estate sales pipeline end-to-end — lead → site visit → booking → post-sale EMI tracking
- Catches Channel Partner conflicts automatically
- Updates live across every user in real time
- Enforces CEO vs. Sales permissions at the database level, not just in the UI
- Ships as one auditable `index.html`, deployed straight to Vercel

**Intentionally not yet built** (by design, to stay lean): multi-currency support, live cursors/presence, table/Gantt views, project templates, SSO, offline/PWA mode. These are scoping decisions, not gaps — future phases can pick any of them up.

---

*This changelog reflects the app's actual feature trajectory based on its current codebase and docs. Update phase names/order if your real build history differed.*
