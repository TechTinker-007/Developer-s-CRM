# Real Estate CRM

A fast, single-file real estate lead management dashboard — built for sales teams who need a pipeline, channel partner tracking, and post-sale member management without the overhead of a full CRM suite.

🔗 **Live app:** [(https://developer-s-crm.vercel.app/)](https://developer-s-crm.vercel.app/)
🔒 Read the [Security](#security) section before sharing a demo link publicly — it explains exactly what is and isn't protectable in an app like this, and what this repo does about it.

---

## What Real Estate CRM Is

Real Estate CRM helps sales teams move a lead from first contact through to a booked sale, then keeps tracking it as a paying member. It's built as a single static `index.html` — React 18 loaded via CDN, compiled in-browser with Babel, no bundler — backed directly by Supabase (Postgres + Auth + Realtime). The goal is a tool that's fast to deploy, easy to audit, and dependable as it grows, with access control enforced by the database itself rather than the UI.

## Core Features

### 📋 Lead Management
A Kanban-style board moves leads across Open → Site Visited → Booked → Rejected, with rich detail per lead — customer info, configuration, budget tier, property type, sector, and entry type (Walk-in / Channel Partner). Follow-ups are scheduled with date/time reminders, and each lead keeps a site visit counter and activity log.

### 🤝 Channel Partner (CP) Management
CP firms register with multiple staff members, and each CP lead carries a lock-in period tied to a specific firm and staff member. The app automatically flags conflicts when a phone number is already locked in elsewhere — catching a common source of disputes before it becomes a problem — and surfaces expired lock-ins for follow-up or reassignment.

### 🔁 Dead Leads & Reassignment
Rejected leads are tracked separately with a reason and timestamp, and can be reassigned back into the active pipeline as a fresh Walk-in lead with one click.

### 💰 Members (Post-Sale Tracking)
Booked leads convert into tracked members with sale price, token amount, and loan amount. A monthly EMI schedule tracks paid/bounced installments, with automatic penalty interest calculation on late payments and free-text notes for loan status and documentation.

### 📊 Dashboard & Reporting
At-a-glance metrics cover lead counts by status, conversion trends, and upcoming follow-ups, alongside a calendar view with clickable follow-up pills and a Logged Data page for reviewing historical activity.

### 🔍 Search & Navigation
Global search spans leads, phone numbers, CP firms, and CP staff, with instant results and inline conflict warnings. Sidebar filters cover locality, property type, budget tier, entry type, CP firm/staff, date range, and status.

### ⚡ Real-Time Collaboration
Powered by Supabase Realtime, leads, firms, dead leads, and members sync across every connected user automatically — no refresh required — with optimistic UI updates and conflict-resolution notices when a record is edited by someone else mid-update.

### 🔐 Authentication & Roles
Email/password sign-in via Supabase Auth (no self-service signup by default). Two roles are enforced server-side via Row Level Security: **CEO** (full access, including deletes) and **Sales** (day-to-day access, no delete rights).

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18 (CDN + Babel, no bundler) |
| Backend / Database | Supabase (Postgres + Auth + Realtime) |
| Hosting | Vercel static hosting |


## Status

Real Estate CRM is actively developed in scoped, additive batches — new features ship without breaking what already works. The live deployment link above always reflects the current version.

## License

All Rights Reserved. See [LICENSE](./LICENSE) for details. Access to a public demo is provided solely for evaluation purposes and does not grant any rights to the underlying source code.
