# PromptGallery - Updated Project Scan

## Repository Layout

- `frontend/` → React + Vite + TypeScript client application.
- `backend/` → high-performance AI scoring/ranking API service (Node.js HTTP, no external deps).
- `REPOSITORY_AUDIT.md` → full flaws report and hardening roadmap.

## Frontend quick map

- `frontend/src/App.tsx` → router + guarded navigation flow.
- `frontend/src/context/AuthContext.tsx` → centralized auth state.
- `frontend/src/pages/*` → UI pages.
- `frontend/src/components/*` → reusable UI components.
- `frontend/src/services/*` → frontend services and mock data.

## Backend quick map

- `backend/src/server.js` → API entrypoint.
- `backend/src/engine/math.js` → math primitives (cosine, sigmoid, softmax, zscore).
- `backend/src/engine/scoring.js` → prompt analysis + risk/precision scoring + batch ranking.
- `backend/src/lib/http.js` → request parsing + JSON response helpers.

## Run commands

### Frontend
```bash
cd frontend
npm install
npm run dev
npm run build
```

### Backend
```bash
cd backend
npm run dev
```

## APIs

- `GET /health`
- `POST /api/v1/analyze`
- `POST /api/v1/rank`
