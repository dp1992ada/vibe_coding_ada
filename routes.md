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

Notes:
- The app uses server Actions (`src/app/actions.ts`) for in-app form submissions. The API endpoints above are implemented to give explicit route handlers for external integration and judging.
- Public vs Protected: all current pages are public. Dashboard routes are planned protected routes that will require authentication and server-side session validation.
