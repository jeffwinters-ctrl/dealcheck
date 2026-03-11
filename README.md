# DealCheck — AI Industrial Sales Coach

Your Anthropic API key lives on the server. Users never see it.

---

## Run locally

```bash
# 1. Install dependencies
npm install

# 2. Create your .env file
cp .env.example .env

# 3. Paste your Anthropic API key into .env
#    ANTHROPIC_API_KEY=sk-ant-api03-...

# 4. Start the server
npm start
# App runs at http://localhost:3000
```

---

## Deploy to Railway (easiest, free tier available)

1. Push this folder to a GitHub repo
2. Go to https://railway.app → New Project → Deploy from GitHub
3. Select your repo
4. Go to Variables → add: `ANTHROPIC_API_KEY` = your key
5. Railway auto-deploys. You get a public URL instantly.

---

## Deploy to Render (also free tier)

1. Push to GitHub
2. Go to https://render.com → New Web Service → connect repo
3. Build command: `npm install`
4. Start command: `node server.js`
5. Add environment variable: `ANTHROPIC_API_KEY` = your key

---

## Deploy to Heroku

```bash
heroku create your-dealcheck-app
heroku config:set ANTHROPIC_API_KEY=sk-ant-api03-...
git push heroku main
```

---

## File structure

```
dealcheck/
├── server.js          ← Express server + API proxy
├── public/
│   └── index.html     ← The full app (served as static)
├── .env               ← Your API key (never commit this)
├── .env.example       ← Template
├── .gitignore         ← Ignores .env and node_modules
└── package.json
```

## How it works

- `server.js` serves `public/index.html` as a static file
- When a rep completes the questionnaire, the browser POSTs deal data to `/api/analyze`
- The server adds your API key and forwards the request to Anthropic
- Claude writes the plays and health findings, server returns them to the browser
- Your key never touches the browser
