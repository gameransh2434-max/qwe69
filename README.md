# QWE Community — Netlify Deployment

Pre-built, drag-and-drop Netlify package. No build step required.

## What's included

| Path | Contents |
|------|----------|
| `public/` | Pre-built React frontend (Vite output) |
| `netlify/functions/api.js` | Entire Express API bundled as a Netlify Function |
| `netlify.toml` | Routing: `/api/*` → function, `/*` → SPA |

## Drag-and-drop deploy

1. Go to [app.netlify.com](https://app.netlify.com)
2. Drag this **entire folder** onto the Netlify drop zone
   (or ZIP it and upload)
3. Netlify detects `netlify.toml` and routes automatically

## Set environment variables (required)

In Netlify → Site Settings → Environment Variables, add:

| Variable | Description |
|----------|-------------|
| `DATABASE_URL` | PostgreSQL connection string |
| `SESSION_SECRET` | Long random string for JWT signing |
| `SMTP_USER` | Gmail address for OTP emails |
| `SMTP_PASS` | Gmail App Password |

> **Free PostgreSQL options:** [Neon](https://neon.tech) · [Supabase](https://supabase.com) · [Railway](https://railway.app)

## First-time DB setup

After deploy, open a terminal and run these against your DB:

```bash
# Clone source or run locally with DATABASE_URL set
pnpm --filter @workspace/db run push
pnpm --filter @workspace/scripts run seed-rewards
pnpm --filter @workspace/scripts run seed-admin
```

Or use the SQL migrations from the source repo.

## Notes

- **World Chat** (WebSocket) is not available on Netlify serverless — it only works on dedicated servers
- The API function runs as Node.js 18 on Netlify
- All REST API endpoints (`/api/auth`, `/api/rewards`, `/api/claims`, etc.) work normally
