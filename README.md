# WriteFlow

Writing project manager with publication-style tracking. Static app: runs free on GitHub Pages, stores files and data in your own Google Drive.

## Features
- Writings: grants, articles, conference papers, research, book chapters, books, case studies, reports
- Type-specific pipelines (e.g. Idea → Drafting → Submitted → Under review → Revisions → Accepted → Published)
- Board (drag between stages), list, dashboard with deadlines
- Tasks per writing
- Versions: upload files to Drive, auto-numbered per document (Manuscript v1, v2…; Cover letter v1…)
- Reviews: rounds, reviewers, comment-by-comment responses, copyable response letter
- Submissions log (venue, status, decision)
- File library across all writings
- Checklist templates per type, editable task dates, calendar view with .ics export, response-to-reviewers Word export
- Import: scan an existing Drive folder tree; each project folder becomes a writing with its files as versions
- Google sign-in gate and multiple Drive accounts: each writing is tied to one account; the primary account holds the app data file
- Sync: data saved as `writeflow-data.json` in Drive, so any device sees the same state; JSON export/import as backup

## 1. Deploy on GitHub Pages
1. Create a repo (e.g. `writeflow`), upload `index.html` to the root.
2. Settings → Pages → Source: *Deploy from a branch* → `main` / root → Save.
3. Site URL: `https://michaelouru-sw.github.io/writeflow/`

The repo holds only code. Your data lives in your browser and Drive, so a public repo is safe.

## 2. Connect Google Drive (one-time, free)
1. console.cloud.google.com → create project `WriteFlow`.
2. APIs & Services → Library → enable **Google Drive API**.
3. OAuth consent screen → External → add your Gmail as a **Test user**.
4. Credentials → Create credentials → **OAuth client ID** → Web application.
   - Authorized JavaScript origins: `https://michaelouru-sw.github.io` (add `http://localhost:8000` for local testing)
5. Copy the Client ID → WriteFlow → ⚙ Settings → paste → Save → **Connect Drive**.

Scope used: `drive` (full Drive access, needed to browse existing files and folders). Keep the OAuth app in Testing mode and only add yourself as test user.

## Accounts & sign-in
- Open the site, click *Sign in with Google*. The first account becomes primary (stores `writeflow-data.json`).
- Settings → *Add Google account* to link more Drives (e.g. work, company, personal). Pick the account per writing on creation, in Overview, or per import.
- *Sign out* syncs to Drive, then clears this browser's local copy.
- The sign-in gate protects your Drive data and clears the cache on sign-out; it is not a substitute for locking your device.

## Notes
- Each writing gets a subfolder: `WriteFlow/<title>/`.
- Removing a version from the list never deletes the Drive file.
- Access tokens last ~1 hour; click *Connect Drive* if sync shows "reconnect".
- Keep OAuth in *Testing* mode for personal use (no Google verification needed; test users re-consent about every 7 days).
