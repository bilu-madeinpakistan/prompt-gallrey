# Repository Scan + Flaws Report

## Critical / High-priority flaws found

1. **Auth was previously localStorage-only and scattered across UI**.
   - Risk: tamperable session flag, hard to migrate to enterprise auth.
   - Status: improved by centralized auth context in frontend.

2. **No dedicated backend service existed**.
   - Risk: all ranking and business logic exposed in client, easy reverse-engineering/tampering.
   - Status: addressed by new `backend/` service with server-side analysis/ranking endpoints.

3. **Project layout was flat (hard to scale)**.
   - Risk: difficult ownership boundaries, hard onboarding for large teams.
   - Status: reorganized into `frontend/` and `backend/` top-level folders.

4. **Missing clear API boundary for AI/ranking**.
   - Risk: no clean contract between UI and intelligence layer.
   - Status: added `/api/v1/analyze` and `/api/v1/rank`.

5. **Frontend entry mismatch risk after restructuring**.
   - Status: fixed by explicit Vite entry script in `frontend/index.html`.

## New structure

- `frontend/` → full React/Vite app.
- `backend/` → AI-focused scoring/ranking server with mathematical scoring engine.
- `REPOSITORY_AUDIT.md` + `PROJECT_SCAN.md` → fast onboarding docs.

## Suggested next steps

- Connect frontend feed and upload flow to backend APIs.
- Add Redis queue + worker for heavy async model scoring.
- Add JWT-based auth and role permissions.
- Add observability: tracing, metrics, structured logs.
- Add rate limiting and WAF policies before production exposure.
