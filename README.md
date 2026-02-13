# PromptGallery Monorepo

A clean two-app layout so GitHub view is clear at a glance:

```text
prompt-gallrey/
├── frontend/   # React + Vite client
├── backend/    # Node API (AI scoring, Cloudinary signing, Supabase persistence)
├── DEPLOYMENT_SUPABASE.md
├── PROJECT_SCAN.md
├── REPOSITORY_AUDIT.md
└── REPO_STRUCTURE.md
```

## Run locally

### Frontend
```bash
npm run dev:frontend
```

### Backend
```bash
npm run dev:backend
```

### Build frontend
```bash
npm run build:frontend
```

## Root visibility check

```bash
rg --files
```

You should clearly see both `frontend/` and `backend/` folders.

## Deployment docs

- Full deploy + Supabase + Cloudinary: `DEPLOYMENT_SUPABASE.md`
- Architecture scan: `PROJECT_SCAN.md`
- Security/flaws audit: `REPOSITORY_AUDIT.md`
- Folder map: `REPO_STRUCTURE.md`


## Create a brand-new clean repo (fresh start)

If your current GitHub repo is messy, run:

```bash
bash scripts/create_clean_repo.sh ../prompt-gallrey-clean
```

Then push that new folder to a new GitHub repository:

```bash
cd ../prompt-gallrey-clean
git remote add origin <your-new-github-repo-url>
git push -u origin main
```
