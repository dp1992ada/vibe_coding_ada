# Routes

Public:
- `/` — Landing page with hero, organization form, volunteer form, and donation panel (anchors: `#register-org`, `#volunteer`, `#donate`).

Planned / Protected (not yet implemented):
- `/dashboard` — Admin dashboard (protected)
- `/dashboard/organizations` — Manage organizations (protected)
- `/dashboard/volunteers` — Manage volunteers (protected)
- `/dashboard/donations` — Manage donations (protected)

API Endpoints:
- `POST /api/organizations` — Create a new organization (public). Inserts into `organizations` table.
- `POST /api/volunteers` — Create a new volunteer (public). Inserts into `volunteers` table.
- `POST /api/donations` — Create a new donation intent (public). Inserts into `donations` table with status `pending`.
- `POST /api/webhooks/payments` — (planned) Payment gateway webhook receiver to mark donations `completed`.


Public Pages
- `/` — Landing page (hero, organization form, volunteer form, donation panel). File: [src/app/page.tsx](src/app/page.tsx#L1-L400). Anchors: `#register-org`, `#volunteer`, `#donate`.

Shared layout
- `src/app/layout.tsx` — App root layout used by all pages. See [src/app/layout.tsx](src/app/layout.tsx#L1-L200).

Server Actions (used by forms)
- `registerOrganization(formData)` — defined in [src/app/actions.ts](src/app/actions.ts#L1-L200). Persists to Supabase, enqueues to BullMQ, and optionally sends email via Resend.
- `registerVolunteer(formData)` — defined in [src/app/actions.ts](src/app/actions.ts#L1-L200).

API Endpoints (App Router)
- `POST /api/organizations` — Handler: [src/app/api/organizations/route.ts](src/app/api/organizations/route.ts#L1-L200). Inserts into `organizations` table.
- `POST /api/volunteers` — Handler: [src/app/api/volunteers/route.ts](src/app/api/volunteers/route.ts#L1-L200). Inserts into `volunteers` table.
- `POST /api/donations` — Handler: [src/app/api/donations/route.ts](src/app/api/donations/route.ts#L1-L200). Inserts into `donations` table with `status` defaulting to `pending`.
- `POST /api/webhooks/payments` — Webhook receiver to mark donations `completed`. Handler: [src/app/api/webhooks/payments/route.ts](src/app/api/webhooks/payments/route.ts#L1-L200).

Planned / Protected Routes (not implemented)
- `/dashboard` — Admin dashboard (protected; requires auth/session).
- `/dashboard/organizations` — Manage organizations (protected).
- `/dashboard/volunteers` — Manage volunteers (protected).
- `/dashboard/donations` — Manage donations and reconcile payments (protected).

Implemented /dashboard skeleton
- `/dashboard` — Simple protected client page that redirects to `/` if unauthenticated. File: [src/app/dashboard/page.tsx](src/app/dashboard/page.tsx#L1-L200).

Testing Notes
- The in-page forms use server Actions (`src/app/actions.ts`) and will call Supabase using `NEXT_PUBLIC_SUPABASE_URL`/anon keys for client-side flows. For secure API or background jobs, set `SUPABASE_SERVICE_ROLE_KEY` in your environment and prefer server-side endpoints.
- Quick API curl examples are in `README.md` under "Submission Checklist & Local Run".

If you'd like, I can:
- Add a `/dashboard` skeleton with route protection using NextAuth or Supabase Auth.
- Implement `POST /api/webhooks/payments` to accept mock payment webhooks and mark donations `completed`.
