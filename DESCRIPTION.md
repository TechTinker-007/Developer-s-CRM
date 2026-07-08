# Real Estate CRM

## Full Description

Real Estate CRM is a lightweight lead-management dashboard built for real estate sales teams who need a Kanban-style pipeline, Channel Partner (CP) tracking, and post-sale member management without the overhead of a full enterprise CRM.

The application is built as a single static `index.html`, with React loaded via CDN and compiled in the browser using Babel. It uses Supabase (Postgres, Authentication, and Realtime) as the backend, requiring no build step for deployment.

## Features

### Lead Management Pipeline

The core workflow follows a lead from first contact through to a booked sale through a Kanban-style pipeline:

- **Open**
- **Site Visited**
- **Booked**
- **Rejected**

Each lead stores detailed information including:

- Customer information
- Property configuration
- Budget tier
- Property type
- Entry type
- Follow-up scheduling

### Channel Partner (CP) Management

Channel Partner leads include a lock-in period tied to a specific CP firm and staff member.

The application automatically detects and flags conflicts when a phone number is already locked with another Channel Partner, helping prevent common commission disputes in real estate sales before they occur.

### Post-Sale Member Management

Once a lead is booked, it is converted into a tracked member with:

- Monthly EMI schedule
- Paid and bounced installment tracking
- Automatic penalty interest calculation for late payments

### Dashboard & Analytics

The dashboard provides:

- Lead counts
- Conversion trends
- Upcoming follow-ups
- Calendar view
- Global search across:
  - Leads
  - Phone numbers
  - Channel Partner firms
  - Channel Partner staff

### Security & Access Control

Access is role-based and enforced on the server using **Supabase Row Level Security (RLS)**.

Available roles include:

- **CEO**
  - Full access
  - Delete permissions

- **Sales**
  - Day-to-day operational access
  - No delete permissions

Security is enforced entirely through database policies rather than client-side checks.

### Realtime Collaboration

Using Supabase Realtime, every connected user immediately sees:

- Lead updates
- Status changes
- Member updates

The application also includes:

- Optimistic UI updates
- Conflict-resolution notifications when multiple users edit the same record simultaneously

## Architecture

The project is intentionally designed as a **single-file, no-bundler application** to make it:

- Easy to audit
- Simple to deploy
- Straightforward to self-host

Because the entire client application is publicly visible once deployed, the project relies on robust Supabase Row Level Security policies. This design decision makes the RLS policies a critical part of the application's security model (see the Security section in the README).

## Deployment

The application is deployed on Vercel and is actively maintained.

**Live Demo:** [https://developer-s-crm.vercel.app/]
