# Real Estate CRM

A lightweight, single-file Real Estate lead management dashboard built with React and Supabase — no build step required.

**Live demo:** _add your deployment link here_

> ⚠️ Read the [Security](#security) section before sharing a demo link publicly. It explains exactly what is and isn't protectable in an app like this, and what this repo does about it.

---

## Features

See [FEATURES.md](./FEATURES.md) for the full, detailed feature list. In short:

- Lead pipeline (Open → Site Visited → Booked / Rejected) with a Kanban-style board
- Channel Partner (CP) firm & staff registration, with lock-in period conflict detection
- Member (post-sale customer) tracking with EMI/payment schedules and penalty interest calculation
- Dashboard analytics, calendar view, global search, CSV-style logged data export
- Real-time updates across users via Supabase Realtime
- Two roles — CEO (full access) and Sales (day-to-day access, no deletes)

## Tech stack

- **Frontend:** React 18 (loaded via CDN, compiled in-browser with Babel — one static `index.html`, no bundler)
- **Backend:** [Supabase](https://supabase.com) (Postgres + Auth + Realtime), accessed directly from the browser
- **Hosting:** Vercel static hosting (see `vercel.json`)

## Getting started

1. Create a free project at [supabase.com](https://supabase.com).
2. Create your app's tables (`leads`, `firms`, `dead_leads`, `members`) matching the shape used in `index.html`, or restore from your own schema/backup.
3. In the Supabase SQL editor, run **`supabase_security_migration.sql`** from this repo. This is required — see [Security](#security).
4. In `index.html`, set `SUPABASE_URL` and `SUPABASE_ANON_KEY` to your project's values (Dashboard → Project Settings → API). The anon/publishable key is meant to be public; see below for why that's safe here.
5. Create your own user: Dashboard → Authentication → Users → Add user. Then promote yourself to CEO:
   ```sql
   update public.profiles set role = 'CEO' where id =
     (select id from auth.users where email = 'you@company.com');
   ```
6. Turn off public self-signup unless you want it: Dashboard → Authentication → Providers → Email → "Allow new users to sign up" → off. Add teammates from the dashboard instead.
7. Open `index.html` in a browser (or deploy — see below). Sign in with the account you just created.

## Deploying

This repo is set up for [Vercel](https://vercel.com) static hosting out of the box (`vercel.json`). Push to a Git provider and import the repo in Vercel, or run `vercel deploy` from this folder. No build command or environment variables are needed since there's no build step — just make sure `SUPABASE_URL`/`SUPABASE_ANON_KEY` in `index.html` point at your project before deploying.

## Security

**Please read this before you share a live demo link.**

This is a client-only, single-page app: your browser downloads `index.html` and runs it directly — there is no server hiding any part of it. That means:

- **Anyone who can load the page can also view its full source** (right-click → View Page Source, or the Network/Sources tab in DevTools). Making the *Git repository* private does not change this — the deployed page itself is the source code, and it's public the moment someone can browse to it.
- The Supabase URL and anon/publishable key in `index.html` are **meant** to be visible client-side. That's how every Supabase (and Firebase) frontend app works. They are not secrets — they only grant whatever access your Row Level Security (RLS) policies allow.

**What actually matters for security here is not hiding the code — it's what the server (Supabase) allows that code to do.** This repo originally shipped with:
- An **open RLS policy** (`anon` role = full read/write access to every table), meaning anyone with the anon key — which is baked into the page — could read or modify all data directly via the Supabase REST API, without even opening the app.
- A **fake login screen** with two hardcoded passwords (`admin123` / `sales123`) baked into the JavaScript bundle, and a role that lived only in `sessionStorage` — trivially readable and editable from DevTools, and not checked by the server at all.

**What this repo now does about it:**
- Real authentication via **Supabase Auth** (email + password) — see `LoginPage` in `index.html`.
- A `profiles` table that stores each user's real, server-side role (`CEO` or `Sales`), set only by you via SQL/Dashboard.
- **Row Level Security policies** (`supabase_security_migration.sql`) that require a valid logged-in session for every read/write, and restrict deletes to CEOs — enforced by Postgres itself, not just hidden in the UI.

Run `supabase_security_migration.sql` against your project before deploying anywhere reachable by people you don't fully trust with the data. Until you do, treat any existing deployment as fully public read/write.

If you want stronger isolation (e.g. salespeople only ever seeing their own assigned leads, not everyone's), that requires additional RLS policies scoped by `assigned_to = auth.uid()` — see the comments in the migration file for where to extend this.

### What obfuscating/minifying the code would and wouldn't do

You can minify or obfuscate `index.html` to make casual copy-pasting more annoying, and this repo's build can be adapted to do that. It raises the bar slightly but **does not stop a determined person** — obfuscated JavaScript still has to run in the browser, which means it can always be deobfuscated, formatted, and read. Treat it as a minor deterrent, not a security control. The RLS + real-auth changes above are the part that actually protects your data.

## License

See [LICENSE](./LICENSE).
