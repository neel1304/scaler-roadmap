# Scaler Roadmap Engine — Local Setup

A profile-to-program career roadmap generator. Upload résumé → pick course → get a session-ready PDF roadmap.

---

## 🚀 Quick start (5 minutes)

### 1. Install Node.js (if you don't have it)
Check first:
```bash
node --version
```
If you see `v18.x` or higher, you're good. Otherwise grab it from https://nodejs.org (LTS version).

### 2. Get your Anthropic API key
- Go to https://console.anthropic.com
- Sign in → **API Keys** → **Create Key**
- Copy the key (starts with `sk-ant-...`)
- Add ~$5 credit (testing this app costs cents)

### 3. Add your key to `.env`
Open the `.env` file in this folder and replace the placeholder:
```
ANTHROPIC_API_KEY=sk-ant-your-actual-key-here
```

### 4. Install dependencies
From inside this folder, run:
```bash
npm install
```
**Heads up:** this downloads Chromium (~170MB) for the PDF engine. First install can take 1–2 minutes — that's normal.

### 5. Start the server
```bash
npm start
```

You should see:
```
🚀 Scaler Roadmap server running
   Frontend:    http://localhost:3000
```

### 6. Open the app
Visit **http://localhost:3000** in your browser. Done.

---

## 📁 What's in this folder

```
scaler-roadmap/
├── server.js          ← Backend (holds API key, calls Claude)
├── package.json       ← Dependencies
├── .env               ← Your API key (NEVER share this file)
├── public/
│   └── index.html     ← Frontend (upload + UI)
└── README.md          ← This file
```

---

## 🛑 Common issues

**"ANTHROPIC_API_KEY missing"**
→ You forgot to paste your real key in `.env`. Open it and replace the placeholder.

**"Cannot find module 'express'"**
→ You skipped `npm install`. Run it from inside the folder.

**Port 3000 already in use**
→ Change `PORT=3000` in `.env` to `PORT=3001` (or any free port).

**API call returns 401 Unauthorized**
→ Your API key is wrong, or the account has no credit. Check console.anthropic.com.

**API call returns 400 / model error**
→ The model name may have changed. Open `server.js`, find `model: "claude-sonnet-4-5"` and update if needed (check https://docs.anthropic.com for current model IDs).

**PDF text extraction fails**
→ The résumé is a scanned image, not a text PDF. Re-export from LinkedIn or save with text layer.

---

## 🔒 Security note

- **Never commit `.env` to git.** Add `.env` to `.gitignore` if you push this anywhere.
- The API key lives only on your machine. The frontend never sees it.
- For team/production deployment, host this on Render, Railway, Fly, or your own server.

---

## 🎯 To deploy this for your team

Easiest option: **Render** (free tier works).
1. Push this folder to a GitHub repo (with `.env` in `.gitignore`).
2. New Web Service on Render → connect repo.
3. Build command: `npm install` · Start command: `npm start`.
4. Add `ANTHROPIC_API_KEY` as an environment variable in Render's dashboard.
5. Done — get a public URL.
