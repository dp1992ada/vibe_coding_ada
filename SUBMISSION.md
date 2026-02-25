# Submission Form — Problem & Idea Clarity

**Problem & Target User:**
- **Problem:** Local animal-service organizations and volunteers lack a centralized, low-friction way to register services, recruit volunteers, and capture donation intents.
- **Target user:** Operators of small animal shelters, veterinary outreach programs, and individuals who want to volunteer or donate.

**Solution:**
- **What:** A lightweight platform (Padaams CSR) to register services, collect volunteer signups, and accept donation intents.
- **Primary outcome:** Faster matching of volunteers to local services and a simple donation intake flow for non-profits.

**Why it’s different / better:**
- **Low friction:** Public forms that write directly to a managed Supabase DB and optional confirmation emails (Resend) reduce onboarding overhead.
- **Background processing:** Queues (BullMQ + Redis) allow verification and enrichment without blocking the user flow.

**One-sentence value proposition:**
- **Value:** Connect local animal-service organizations with volunteers and donors through simple public intake forms and background verification.

**Core user journey (3–4 steps):**
1. Visitor lands on `/` and chooses to `Add Service`, `Volunteer`, or `Donate`.
2. Visitor completes a short public form (organization or volunteer) which writes to Supabase and enqueues verification.
3. System sends an optional confirmation email and staff reviews the new entry (via planned dashboard).
4. Donations are created as `pending` donation intents and later reconciled via payment webhooks (planned).

**How to test the core feature locally:**
- Start dev server:

```bash
npm install
npm run dev
```

- Open `http://localhost:3000` and use the anchors `#register-org`, `#volunteer`, or `#donate` to exercise forms.
- Or use the API curl examples in `README.md` to POST to `/api/organizations`, `/api/volunteers`, `/api/donations`.
- To persist data, run the SQL in `supabase_schema.sql` in a Supabase project and set env vars in `.env.local`:

```
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
RESEND_API_KEY=your-resend-key
REDIS_URL=redis://...
```

**Known limitations (for judges):**
- No protected admin dashboard yet — review and moderation is manual.
- Payment gateway integration is mocked; `donations` are created as `pending` and need a webhook to mark `completed`.
- Background worker consumers for the BullMQ queues are not bundled in this repo; they require a Redis instance and worker process.

**Deliverables included in this repo:**
- `routes.md` — Human-readable route manifest.
- `README.md` — Run instructions and API examples.
- `supabase_schema.sql` — SQL schema to create `organizations`, `volunteers`, and `donations` tables.
- `src/app/page.tsx` — Landing page with forms.
- `src/app/actions.ts` — Server Actions used by forms (persists to Supabase, enqueues jobs, optional email).
- `src/app/api/*/route.ts` — API endpoints for `organizations`, `volunteers`, and `donations`.

**What to send to your instructor (recommended):**
- Live URL (Vercel) if deployed.
- Landing page screenshot (PNG/JPG) showing product name, tagline, and primary CTA.
- This `SUBMISSION.md` plus `routes.md` and a GitHub repo link.
