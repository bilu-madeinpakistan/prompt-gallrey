# Deployment + Supabase + Cloudinary Setup Guide

## What I need from you (secrets)

Please provide these values:

- `SUPABASE_URL`
- `SUPABASE_SERVICE_ROLE_KEY`
- `CLOUDINARY_CLOUD_NAME`
- `CLOUDINARY_API_KEY`
- `CLOUDINARY_API_SECRET`
- deployed backend URL (for frontend `VITE_BACKEND_URL`)

## 1) Recommended hosting stack

- **Frontend**: Vercel / Netlify / Cloudflare Pages
- **Backend**: Railway / Render / Fly.io
- **Database**: Supabase
- **Image storage**: Cloudinary


## No-card deployment options (important)

Agar card nahi hai, then practical zero-card stack:

- **Frontend**: Cloudflare Pages (free, no card in many regions)
- **Backend**: 
  - Option A: **Koyeb free** (availability region/account-dependent)
  - Option B: **Deno Deploy + Supabase Edge Functions** (serverless path)
  - Option C: **Oracle Cloud Always Free VM** (no card onboarding depends on region)

If Render/Fly/Railway card maang rahe hain, fastest path is:
1. Frontend on Cloudflare Pages.
2. Backend ko temporary self-host on VPS/Always-Free VM.
3. Later migrate to paid managed host.

## 2) Supabase SQL schema

```sql
create table if not exists public.prompt_analysis_events (
  id bigint generated always as identity primary key,
  created_at timestamptz not null default now(),
  prompt text not null,
  precision_score double precision not null,
  vulnerability_risk double precision not null,
  novelty double precision not null,
  coherence double precision not null,
  entropy double precision not null,
  latency_bonus double precision not null
);

create table if not exists public.prompt_rank_events (
  id bigint generated always as identity primary key,
  created_at timestamptz not null default now(),
  items_count integer not null
);

create table if not exists public.gallery_posts (
  id bigint generated always as identity primary key,
  created_at timestamptz not null default now(),
  author_name text not null,
  author_avatar text,
  image_url text not null,
  prompt text not null,
  model text not null,
  category text not null,
  precision_score double precision,
  vulnerability_risk double precision
);
```

## 3) Backend env vars

```bash
PORT=8080
SUPABASE_URL=https://<project-ref>.supabase.co
SUPABASE_SERVICE_ROLE_KEY=<service-role-key>
CLOUDINARY_CLOUD_NAME=<cloud-name>
CLOUDINARY_API_KEY=<api-key>
CLOUDINARY_API_SECRET=<api-secret>
ALLOWED_ORIGINS=https://<your-frontend-domain>
RATE_LIMIT_WINDOW_MS=60000
RATE_LIMIT_MAX_REQUESTS=120
```

## 4) Frontend env var

```bash
VITE_BACKEND_URL=https://<your-backend-domain>
```

## 5) Runtime flow now implemented

1. Upload page runs AI analysis (`/api/v1/analyze`).
2. Publish button requests Cloudinary signed params (`/api/v1/cloudinary/signature`).
3. Browser uploads image to Cloudinary.
4. Frontend sends post metadata to backend (`/api/v1/posts`).
5. Backend writes post/event rows into Supabase (non-blocking).

## 6) Health + verification

- `GET /health` now reports both `supabase` and `cloudinary` configuration state.
- Test endpoints:
  - `POST /api/v1/analyze`
  - `POST /api/v1/rank`
  - `POST /api/v1/cloudinary/signature`
  - `POST /api/v1/posts`


## 7) Backend deployed URL kahan se milta hai?

Backend deploy karne ke baad hosting provider aapko public URL deta hai:

- **Render**: service dashboard -> top par URL (e.g. `https://promptgallery-api.onrender.com`)
- **Railway**: project -> service -> `Networking` tab -> generated domain
- **Fly.io**: app name se URL (`https://<app-name>.fly.dev`)

Isi URL ko frontend env me set karein:

```bash
VITE_BACKEND_URL=https://<your-backend-domain>
```

Then frontend ko redeploy karo.
