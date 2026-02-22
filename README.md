# Calibre9 — Category Intelligence Dashboard

A proxy server that securely forwards requests from the dashboard to the Anthropic API, bypassing browser CORS restrictions.

---

## Files

| File | Purpose |
|------|---------|
| `server.js` | Express proxy server |
| `calibre9-dashboard.html` | The dashboard (served as a static file) |
| `package.json` | Node dependencies |
| `.env.example` | Environment variable template |

---

## Local Setup

```bash
# 1. Install dependencies
npm install

# 2. Create your .env file
cp .env.example .env

# 3. Add your Anthropic API key to .env
#    ANTHROPIC_API_KEY=sk-ant-...

# 4. Start the server
npm start

# 5. Open the dashboard
#    http://localhost:3000/calibre9-dashboard.html
```

---

## Deploy to Railway (recommended — free tier)

1. Push this folder to a GitHub repo
2. Go to [railway.app](https://railway.app) → New Project → Deploy from GitHub
3. Select your repo
4. Go to **Variables** and add:
   - `ANTHROPIC_API_KEY` = your key
5. Railway will auto-detect Node and deploy
6. Your dashboard will be live at the Railway URL + `/calibre9-dashboard.html`

---

## Deploy to Render (free tier)

1. Push to GitHub
2. Go to [render.com](https://render.com) → New → Web Service
3. Connect your repo
4. Set **Build Command**: `npm install`
5. Set **Start Command**: `npm start`
6. Add environment variable: `ANTHROPIC_API_KEY`
7. Deploy — live at your Render URL + `/calibre9-dashboard.html`

---

## Deploy to Fly.io

```bash
npm install -g flyctl
fly auth login
fly launch
fly secrets set ANTHROPIC_API_KEY=sk-ant-...
fly deploy
```

---

## Security Notes

- Your API key is **never exposed to the browser** — it lives only on the server
- CORS is enabled for all origins by default; restrict this in production if needed by replacing `app.use(cors())` with:
  ```js
  app.use(cors({ origin: "https://yourdomain.com" }));
  ```
[README.md](https://github.com/user-attachments/files/25472990/README.md)
