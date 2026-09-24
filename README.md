# Portfolio

Personal site built with the Next.js App Router, TypeScript and Supabase — including a self-hosted admin panel that edits every section without a redeploy.

## Why it exists

Most portfolios hardcode their content in JSX, so any copy change means a commit and a deploy. This one keeps every section in `content/*.json` as the seed and in Supabase as the live source, editable from `/admin`.

## Stack

- **Next.js** (App Router) + **TypeScript**
- **Supabase** — content storage and image uploads
- Cookie-based auth with middleware-protected `/admin` routes
- Deployed on Netlify

## Structure

```
app/            Public pages and API routes
app/admin/      Admin panel, one editor per section
components/     Section components (Hero, Work, Stack, Lab, …)
content/        Seed content as JSON
lib/            Supabase client, auth and content helpers
supabase/       SQL migrations
```

## Running locally

```bash
pnpm install
cp .env.example .env.local   # Supabase URL + keys, admin credentials
pnpm dev
```

Open http://localhost:3000, and http://localhost:3000/admin for the editor.

## Admin panel

`/admin` is guarded by `middleware.ts`. Each section has its own editor that writes through `app/api/content/[section]`, with image uploads going to Supabase storage via `app/api/upload`.
