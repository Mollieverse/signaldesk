# SignalDesk — AI-Native Global Newsroom

Bloomberg-grade editorial interface. Autonomous news reporting powered by Claude AI.

---

## Deploy to Vercel in 3 steps

### Step 1 — Push to GitHub

```bash
cd signaldesk-deploy
git init
git add .
git commit -m "SignalDesk v2"
# Create a new repo on github.com, then:
git remote add origin https://github.com/YOUR_USERNAME/signaldesk.git
git push -u origin main
```

### Step 2 — Deploy on Vercel

1. Go to [vercel.com](https://vercel.com) → **Add New Project**
2. Import your GitHub repo
3. Leave all build settings as-is (Vercel auto-detects)
4. Click **Deploy**

### Step 3 — Add your API key

1. In Vercel dashboard → your project → **Settings** → **Environment Variables**
2. Add:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** `sk-ant-...` (your key from console.anthropic.com)
3. Click **Save**
4. Go to **Deployments** → **Redeploy** (so the env var takes effect)

**Done.** Your site is live at `https://signaldesk-xxx.vercel.app`

---

## Local development

```bash
# Install Vercel CLI
npm i -g vercel

# Create local env file
cp .env.example .env.local
# Edit .env.local and add your real ANTHROPIC_API_KEY

# Run locally (serves static + API functions)
vercel dev
# → http://localhost:3000
```

---

## Project structure

```
signaldesk-deploy/
├── public/
│   └── index.html        # Full app — homepage + article pages
├── api/
│   └── ask.js            # Serverless proxy → Anthropic API
├── vercel.json           # Routing: /api/* → functions, /* → static
├── package.json
└── .env.example          # Environment variable template
```

## How the "Ask this story" feature works

The frontend sends a `POST /api/ask` with `{ prompt: "..." }`.

The serverless function in `api/ask.js` adds the API key from the environment and forwards the request to Anthropic. The API key **never touches the browser**.

---

## Get an Anthropic API key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign in → **API Keys** → **Create Key**
3. Copy the `sk-ant-...` value
4. Add it to Vercel as `ANTHROPIC_API_KEY`
