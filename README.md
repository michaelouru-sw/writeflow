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
- In-app file viewer: PDF, Word (.docx), Google Docs/Sheets/Slides (as PDF), images, text, video/audio; other types fall back to Drive's own preview. Switch between versions of the same document inside the viewer
- Pipeline rail per writing (click a stage to move it), light/dark/auto theme, mobile layout, press N for a new writing
- Bulk select on All writings: set stage or delete many at once (with Undo)
- People: contacts, team roles per writing, task assignment
- Venues: journal/funder shortlist; after a rejection the Submissions tab suggests where to send next
- Funding pipeline: amount, chance, expected value, decision dates
- Writing log: log words, daily streak, 14-day chart
- DOI lookup (Crossref) fills the citation; publication list export (Word or copy)
- Assistant (optional): summarise reviews, draft responses, check a file against requirements, using your own Anthropic API key (kept in this browser only)
- Reminders: optional desktop notifications, Google Calendar sync with a 9am reminder the day before
- Daily Drive backups (last 14 kept) with restore; installable offline app (PWA) with an offline copy mode
- Sync: data saved as `writeflow-data.json` in Drive, so any device sees the same state; JSON export/import as backup

## Public view (share a read-only dashboard)
- Anyone with the link sees the dashboard, upcoming and overdue items, pending tasks, stages, reviews and file names. No sign-in.
- To open a file, a visitor must sign in to Google (Drive asks them). It only opens if you shared that file or folder with their account. Use a writing's Team tab, *Share Drive folder*.
- Setup: Cloud Console → Credentials → *API key*, restrict it to **Google Drive API** and to the website `https://michaelouru-sw.github.io/*`. Settings → *Public view* → tick *Share a public view* → paste key → *Save and publish*. Copy the link.
- It publishes a sanitised `writeflow-public.json` (link-readable) in your WriteFlow Drive folder, refreshed on each sync. Notes, people and amounts are excluded unless you tick them. Tick *Hide from the public view* in a writing's Overview to leave it out. *Stop sharing* revokes the link.

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

## Optional extras
- **Google Calendar sync:** enable the *Google Calendar API* in your Cloud project (APIs & Services → Library). Sign in again to approve calendar access, then Calendar → *Sync to Google Calendar*. Completed items are not removed from the calendar.
- **Assistant:** Settings → paste an Anthropic API key. Text you send goes to Anthropic with your key; the key is never synced to Drive.
- **Install as an app:** use your browser's *Install* option on the site. Offline, use *Open offline copy* on the sign-in screen; changes sync when you reconnect.

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
