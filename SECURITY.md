# Security changes made

This document summarizes what was fixed and what you still need to do yourself.

## What was wrong before

| Issue | Risk |
|---|---|
| Supabase RLS policy allowed `anon` full read/write on every table | Anyone with the (public-by-design) anon key — visible in page source — could read or edit **all** data directly via the Supabase API, without even opening the app |
| Login was two hardcoded passwords (`admin123`/`sales123`) in the JS bundle | Visible to anyone via View Source; not real authentication |
| Role (`CEO`/`Sales`) was stored only in `sessionStorage` | Editable from DevTools — anyone could grant themselves CEO/delete rights client-side |
| A `toggleRole()` function let a logged-in user flip their own role in one click | Trivial privilege escalation |

## What's fixed now

- [x] Real authentication via Supabase Auth (`supabaseClient.auth.signInWithPassword`)
- [x] Role stored server-side in a `profiles` table, looked up by `auth.uid()` after login
- [x] Row Level Security policies requiring an authenticated session for all reads/writes, and CEO role for deletes (`supabase_security_migration.sql`)
- [x] Removed the client-side role toggle entirely
- [x] Basic HTTP security headers + `noindex` added in `vercel.json`

## What you still need to do

- [ ] **Run `supabase_security_migration.sql`** in your Supabase project (this is the critical step — nothing above works without it)
- [ ] Create real user accounts for your team in the Supabase Dashboard (not self-signup, unless you want that)
- [ ] Promote your own account to `CEO` via the SQL snippet in the README
- [ ] Turn off public signup in Supabase Auth settings unless intentional
- [ ] Rotate the Supabase anon key if you believe it was already abused (Dashboard → Project Settings → API → "Reset" — note this also requires updating `index.html`)
- [ ] If salespeople should only see their *own* leads (not everyone's), add an `assigned_to` scoped policy — see comments in the migration file

## What this does **not** and cannot do

- It does not hide `index.html`'s source from people who load the page — that's not possible for a client-rendered app (see README § Security). A private Git repo does not change this once you share a live demo link.
- It does not replace normal engineering hygiene: keep the Supabase **service_role** key (different from the anon key) out of any client code, never commit it, and don't paste it into this app.
