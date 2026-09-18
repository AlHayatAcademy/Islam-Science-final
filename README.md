# اسلام اور سائنس — Course Website

A static, self-contained educational website for the "اسلام اور سائنس" (Islam & Science) course — 15 topics, each with a full article, short Q&A, and multiple-choice questions.

- Pure HTML / CSS / vanilla JS — no build step, no framework, no backend.
- Self-hosted fonts (Nafees Nastaleeq for Urdu body text, Amiri for Arabic Qur'anic quotations) — works fully offline.
- Fully responsive (mobile nav, topic dropdowns, single-column MCQ layout on small screens).
- All course content lives in `data/content.js` (a single JS file assigning `window.CONTENT`) — edit that file to update text without touching any markup or logic.

## Project structure

```
.
├── index.html          # single-page app shell (all 5 views)
├── css/style.css        # all styling, incl. @font-face declarations
├── js/app.js             # router + rendering logic (hash-based routing)
├── data/content.js       # all 15 topics: article + Q&A + MCQ content
├── fonts/                # self-hosted woff2 fonts (Nafees Nastaleeq, Amiri)
├── _headers              # Cloudflare Pages cache-control rules
└── README.md
```

## Run locally

No install needed. Either:

- Double-click `index.html` to open it directly in a browser, or
- Serve it (recommended, avoids any `file://` quirks):
  ```bash
  python3 -m http.server 8000
  # then open http://localhost:8000
  ```

## Deploy — GitHub (repo + optional GitHub Pages)

1. Create a new empty repository on GitHub (no README/license, since this folder already has them).
2. From this folder:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Islam & Science course website"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. (Optional) To host it for free on **GitHub Pages**: repo → Settings → Pages → Source: "Deploy from a branch" → Branch: `main` / root → Save. Your site will be live at `https://<your-username>.github.io/<your-repo>/` within a minute or two.

## Deploy — Cloudflare Pages

**Option A — via GitHub (recommended, auto-deploys on every push):**

1. Push this project to GitHub first (see above).
2. Go to the [Cloudflare dashboard](https://dash.cloudflare.com) → **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**.
3. Select your repository.
4. Build settings: leave **Build command** empty and **Build output directory** set to `/` (this is a static site — nothing to build).
5. Click **Save and Deploy**. Cloudflare gives you a `*.pages.dev` URL immediately; you can attach a custom domain afterwards under the project's **Custom domains** tab.

**Option B — direct upload with Wrangler CLI (no GitHub needed):**

```bash
npm install -g wrangler
wrangler login
wrangler pages deploy . --project-name=islam-aur-science
```

This uploads the current folder directly and gives you a live `*.pages.dev` URL.

The included `_headers` file (Cloudflare Pages' native way to set response headers) applies long-lived caching to the font and asset files, which Cloudflare Pages picks up automatically — no extra configuration needed.

## Editing content

All text lives in `data/content.js` as plain JavaScript objects — one entry per topic, with `article`, `qa`, and `mcq` arrays. No HTML editing is required to fix a typo or add a question; just edit that file and refresh.

## License

Code (HTML/CSS/JS) in this repository is provided under the MIT License — see `LICENSE`. The educational content (articles, questions and answers) is the author's original work, provided for the course's own use.
