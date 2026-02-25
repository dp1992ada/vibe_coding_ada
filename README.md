This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.

## Submission Checklist & Local Run

Follow these steps to run the app locally and produce deliverables for grading:

- Install deps and run dev server:

```bash
npm install
npm run dev
```

- Open http://localhost:3000 to view the landing page. The page includes forms for:
	- Organization registration (anchor `#register-org`)
	- Volunteer registration (anchor `#volunteer`)
	- Donation intent (anchor `#donate`)

- Routes manifest: see [routes.md](routes.md) for a human-readable route map (public vs protected, API endpoints).

- API endpoints (examples):

Create an organization (curl):

```bash
curl -X POST http://localhost:3000/api/organizations \
	-H "Content-Type: application/json" \
	-d '{"name":"Test Org","email":"test@example.com","whatsapp":"+911234567890","street":"1 Main St","city":"City","state":"State","zipcode":"000000","service_category":"shelter","animal_types":"dogs","description":"Test"}'
```

Create a volunteer (curl):

```bash
curl -X POST http://localhost:3000/api/volunteers \
	-H "Content-Type: application/json" \
	-d '{"first_name":"Jane","last_name":"Doe","email":"jane@example.com","whatsapp":"+911234567891","city":"City","service_category_interest":"veterinary"}'
```

Create a donation intent (curl):

```bash
curl -X POST http://localhost:3000/api/donations \
	-H "Content-Type: application/json" \
	-d '{"amount":100.00,"type":"one-time","gateway":"gpay"}'
```

Notes:
- The SQL schema lives in `supabase_schema.sql` — run it in your Supabase project's SQL editor to create the required tables.
- For full functionality (email, queues, OAuth), set env vars in Vercel or a `.env.local` file:

```
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
RESEND_API_KEY=your-resend-key
REDIS_URL=redis://... (for BullMQ)
```

What to send to your instructor (zip or Vercel link):
- Live deployment URL (Vercel)
- Landing page screenshot (PNG/JPG)
- `routes.md` (already added)
- Public GitHub repo link
- Short submission answers: problem statement, target user, one-sentence value prop, primary user journey (3–4 steps)

