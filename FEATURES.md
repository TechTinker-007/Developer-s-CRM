# Features

## Authentication & roles
- Email/password sign-in via Supabase Auth (no self-service signup by default).
- Two roles, enforced server-side via Row Level Security:
  - **CEO** — full access, including deleting leads, firms, staff, and members.
  - **Sales** — day-to-day access (create/update leads, log activity, register CPs) without delete rights.

## Lead management
- Kanban-style lead board across statuses: Open, Site Visited, Booked, Rejected.
- Rich lead detail: customer info, configuration, budget tier, property type, sector, entry type (Walk-in / Channel Partner).
- Follow-up scheduling with date/time reminders.
- Site visit counter and notes/activity log per lead.
- Duplicate/conflict detection: warns when a phone number is already tied to an active Channel Partner lock-in period elsewhere.

## Channel Partner (CP) management
- CP firm registration with multiple staff members per firm.
- Per-lead lock-in period tracking (start/expiry dates) tied to a CP firm and staff member.
- Automatic conflict checking against existing lock-ins when adding a new CP lead.
- Expired lock-ins are surfaced for follow-up/reassignment.

## Dead leads & reassignment
- Rejected/dead leads are tracked separately with a reason and timestamp.
- One-click reassignment of a dead lead back into the active pipeline as a fresh Walk-in lead.

## Members (post-sale customers)
- Converts booked leads into tracked "members" with sale price, token amount, and loan amount.
- Monthly payment schedule with paid/bounced tracking per installment.
- Automatic penalty interest calculation on late/bounced payments.
- Notes per member for loan status, documentation, etc.

## Dashboard & reporting
- At-a-glance metrics: lead counts by status, conversion trends, upcoming follow-ups.
- Calendar view with clickable task/follow-up pills.
- Logged Data page for reviewing historical activity across leads/firms/dead leads.

## Search & navigation
- Global search across leads, phone numbers, CP firms, and CP staff, with instant dropdown results and conflict warnings inline.
- Sidebar filters: locality, property type, budget tier, entry type, CP firm/staff, date range, status.
- Sort controls and quick-action icons on lead rows.
- Mobile-friendly Projects/Leads list view.

## Real-time collaboration
- Live updates across all connected users via Supabase Realtime — leads, firms, dead leads, and members sync automatically without a page refresh.
- Optimistic UI updates with automatic conflict resolution notices when a record is changed by someone else mid-edit.

## Polish
- Custom empty-state and celebration illustrations.
- Toast notifications for key actions.
- Responsive layout for desktop and mobile.

## Intentionally out of scope (for now)
- Multi-currency support
- Live cursors or multiplayer presence indicators
- Table or Gantt chart views
- Project/lead templates
- Single sign-on (SSO)
- Offline mode / PWA support

These aren't oversights — they're scoping decisions to keep the product lean and easy to audit as a single-file, no-bundler app. Some may be revisited in future phases.
