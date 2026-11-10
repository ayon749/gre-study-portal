# GRE Compass — 84-day GregMat + PrepSwift study tracker

Static GitHub Pages website with Supabase Authentication + PostgreSQL for cloud-synced progress.
No hosting build step, Node.js server, or paid infrastructure required for light personal use (subject to providers' free-plan limits).

## 1. Create Supabase project
1. Sign in at https://supabase.com/dashboard and create a project.
2. Go to **SQL Editor**, paste `supabase/schema.sql`, and run it.
3. Open **Project Settings** → API / Data API and API Keys. Copy your **Project URL** and **publishable key** (or legacy anon key). Do NOT use a secret or service-role key.
4. Update `config.js` with those two values.
5. In **Authentication** → **Providers** → **Email**, enable email/password. If email confirmation is enabled, users must click the confirmation link.

## 2. Host through GitHub Pages (free)
1. Create a GitHub repository, e.g. `gre-study-portal`.
2. Upload `index.html`, `config.js`, `README.md`, `.nojekyll` and the `supabase` folder at repository root, or push the folder using `git`.
3. Go to **Settings → Pages → Build and deployment**; choose **Deploy from a branch**, branch **main**, folder **/(root)**, then Save.
4. Your site should be at `https://YOUR_GITHUB_USERNAME.github.io/gre-study-portal/` (replace the username/repo).
5. In **Supabase → Authentication → URL Configuration**, set **Site URL** to your GitHub Pages URL and add the same URL to **Redirect URLs** (use the trailing slash).
6. Open your GitHub Pages URL and create a GRE Compass account. Sign in and complete a task. The cloud badge should show **All changes saved**.

## Data and security
- Each account has one database record identified by its Supabase Auth user ID.
- Row Level Security ensures a signed-in user can only access their own study progress.
- `config.js` is public. The publishable/anon key is designed for browser use, but RLS must remain enabled.
- Never put Supabase service-role/secret keys into GitHub Pages or this project.
- Saved progress syncs between signed-in devices via Supabase.
- Requires internet access. It is not an offline-first app; don't close the tab while **Saving** / **Save failed** is shown.
- Optional export/import remains available. On first login, an existing offline progress record in the same browser can be imported.
- Simultaneous edits in two browsers use last-write-wins, so avoid editing the same tracker on two devices at once.

## Run locally
For test use a local web server, e.g. `python -m http.server 8000`, then open http://localhost:8000. Add localhost to Supabase redirect URLs if using email confirmation locally.

## Files
- `index.html` — full responsive dashboard and cloud-sync logic
- `config.js` — browser-visible Supabase project configuration
- `supabase/schema.sql` — Postgres table with per-user RLS policies
- `.nojekyll` — enables uncomplicated GitHub Pages serving
