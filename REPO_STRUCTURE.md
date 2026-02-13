# Repository Structure (Updated)

Aap ki request ke mutabiq repository now cleanly split hai:

```text
.
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── context/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── App.tsx
│   │   └── index.tsx
│   ├── package.json
│   ├── package-lock.json
│   ├── tsconfig.json
│   ├── vite.config.ts
│   └── index.html
├── backend/
│   ├── src/
│   │   ├── engine/
│   │   ├── lib/
│   │   └── server.js
│   └── package.json
├── package.json (root workspace scripts)
├── PROJECT_SCAN.md
├── REPOSITORY_AUDIT.md
└── README.md
```

## Quick Run

### Frontend
```bash
npm run dev:frontend
```

### Backend
```bash
npm run dev:backend
```
