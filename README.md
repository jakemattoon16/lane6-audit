# Lane6 Revenue Leak Auditor

Internal tool for auditing RIA firms and generating branded PDF reports. Multi-step form → Claude AI analysis → 9-page PDF report.

## Setup

### 1. Install dependencies

```bash
cd lane6-auditor
npm install            # root (concurrently)
cd client && npm install
cd ../server && npm install
```

### 2. Configure API key

Edit `server/.env`:
```
ANTHROPIC_API_KEY=your_key_here
CLAUDE_MODEL=claude-sonnet-4-5
PORT=3001
```

Get your key at: console.anthropic.com

### 3. Run

```bash
# From the project root:
npm run dev
```

This starts:
- Backend: http://localhost:3001
- Frontend: http://localhost:5173

Open http://localhost:5173 in your browser.

## How it works

1. Fill out the 6-step audit form on behalf of a prospect
2. Click **Generate Report** — Claude analyzes all answers
3. View scores on-screen (expandable category details)
4. Click **Download PDF Report** — gets a branded 9-page PDF

## PDF Report Structure

| Page | Content |
|------|---------|
| 1 | Cover — firm name, leak score gauge, date |
| 2 | Executive summary + category score table |
| 3–7 | One page per category (leaks, why it costs money, Lane6 fixes) |
| 8 | 30/60/90 day implementation roadmap |
| 9 | Why Lane6 + strategy call CTA |

## Stack

- **Frontend:** React 18, Vite, Tailwind CSS
- **Backend:** Node.js, Express
- **AI:** Anthropic Claude (claude-sonnet-4-5)
- **PDF:** Puppeteer (headless Chrome)
- **State:** Stateless per session — nothing persisted

## Notes

- Puppeteer downloads Chromium on first `npm install` (~170MB)
- PDF generation takes 5–15 seconds depending on machine speed
- Claude analysis takes 10–30 seconds
- No database — all data is in-memory per request
