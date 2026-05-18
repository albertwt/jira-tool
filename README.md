# Draftless — Jira Story Tool

A PDM tool for reviewing and generating Jira stories. Built with Claude AI.

**Features**
- Review tab: paste a draft story, get grooming-ready questions on AC and scope
- Generate tab: paste raw requirements (text, voice, attachments), get a structured story draft
- Voice input with 5-second silence auto-stop
- File attachments: screenshots, PDFs, Figma exports

---

## Deploy to Vercel (5 minutes)

### 1. Get your Anthropic API key
Go to [console.anthropic.com](https://console.anthropic.com) → API Keys → Create Key

### 2. Install Vercel CLI
```bash
npm install -g vercel
```

### 3. Deploy
```bash
cd draftless
vercel
```
Follow the prompts — pick a project name, accept defaults.

### 4. Add your API key as an environment variable
```bash
vercel env add ANTHROPIC_API_KEY
```
Paste your key when prompted. Then redeploy:
```bash
vercel --prod
```

That's it. Your tool is live at `https://your-project-name.vercel.app`

---

## Project structure

```
draftless/
├── api/
│   └── claude.js        ← serverless proxy (keeps API key server-side)
├── public/
│   └── index.html       ← the full tool UI
└── vercel.json          ← routing config
```

## How the proxy works

The frontend calls `/api/claude` instead of Anthropic directly.
The serverless function in `api/claude.js` attaches your secret API key
server-side and forwards the request. The key never ships to the browser.

---

## Cost

- **Vercel hosting** — free on the Hobby tier
- **Claude.ai Pro** — separate from this tool; covers your claude.ai chat access only
- **Anthropic API** — billed per token, separate from Pro. 
  Get a key at console.anthropic.com. For personal use, expect < $2/month.
  Each Generate or Review call ≈ $0.003–0.005 at Claude Sonnet pricing.

--
  
## Local development

```bash
vercel dev
```
Set `ANTHROPIC_API_KEY` in a `.env` file locally:
```
ANTHROPIC_API_KEY=sk-ant-...
```
