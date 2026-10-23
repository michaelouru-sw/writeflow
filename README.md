# WriteFlow

Writing project manager with publication-style tracking. Static app: runs free on GitHub Pages, stores files and data in your own Google Drive.

## Features
- Writings: grants, consultancy bids, awards and nominations, fellowships, articles, conference papers, research, book chapters, books, thesis chapters, case studies, reports, blogs and op-eds, course design
- Type-specific pipelines (e.g. Idea → Drafting → Submitted → Under review → Revisions → Accepted → Published)
- Call-driven flow for grants, bids, awards, fellowships and conference papers: Call identified → Go/no-go → Concept note/EOI → Drafting → Internal review → Final checks → Submitted → outcome. Each stage gets a target date between today and the deadline (shown on the stage bar), tasks are tied to stages, the app suggests moving on when a stage's tasks are done, warns when behind schedule and re-plans dates. Add the call link in Overview
- Board (drag between stages), list, papers-only dashboard (deadlines and what needs attention, no task rows)
- Tasks per writing; due dates are set automatically between today and the deadline (heavier tasks get more time, weekends avoided, submit task on the deadline). Dates you set yourself are never overwritten; *Auto-set dates* fills new tasks, and changing the deadline re-spreads automatic ones
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

## How work flows
- Every writing starts from a call you have already decided to pursue (no go/no-go step). Add it with the call link, deadline and what the call requires: full paper/proposal, extended abstract, abstract only, or abstract then full paper. The task list fits that choice and can be changed later.
- Only deadlines, decision dates and review responses reach reminders, the dashboard, notifications and Google Calendar. Tasks stay inside each writing, showing the current stage first; later steps and done tasks are collapsed.
- **Reuse:** when a writing is rejected, *Reuse for another call* (also on the dashboard) creates a new writing with the latest files, reviewer comments and a short task list. The original links to it.
- Less-used pages sit under **More** in the sidebar. Reviews and Submissions tabs appear once a writing is submitted.

## Public view (share a read-only dashboard)
- Anyone with the link sees the dashboard, upcoming and overdue items, pending tasks, stages, reviews and file names. No sign-in.
- To open a file, a visitor must sign in to Google (Drive asks them). It only opens if you shared that file or folder with their account. Use a writing's Team tab, *Share Drive folder*.
- Setup: Cloud Console → Credentials → *API key*, restrict it to **Google Drive API** and to the website `https://michaelouru-sw.github.io/*`. Settings → *Public view* → tick *Share a public view* → paste key → *Save and publish*. Copy the link.
- It publishes a sanitised `writeflow-public.json` (link-readable) in your WriteFlow Drive folder, refreshed on each sync. Notes, people and amounts are excluded unless you tick them. Tick *Hide from the public view* in a writing's Overview to leave it out. *Stop sharing* revokes the link.

## Co-authors
- **Automatic:** writings shared with you load on their own (at sign-in, every few minutes, and when you return to the tab) and appear on the dashboard, All writings and Calendar, marked "shared by". Nothing to click.
- **Invite link:** adding a team member with an email gives them editor access and Drive emails them a WriteFlow link. *Invite* on the Team row copies the link or opens an email. The link carries your Client ID, so they need no setup: they sign in with the invited Google account and land on Shared with me.
- **No setup for others:** add a `config.json` next to `index.html` containing `{"clientId":"YOUR-ID.apps.googleusercontent.com"}`. Anyone opening the site then just clicks *Sign in with Google*; their writings are stored in their own Drive. Invite links also carry the Client ID.
- While the consent screen is in Testing mode, add each invitee under *Audience → Test users* in Google Cloud, or Google blocks their sign-in.
- Add a team member who has an email: they get **editor** access to that writing's Drive folder and an invite email. Removing them revokes it.
- The co-author opens WriteFlow, signs in, and sees the writing under **Shared with me**: tick tasks, add tasks, comment, open files. Changes sync back to the lead's copy every few minutes and on each save.
- A shared writing keeps a small `_writeflow.json` in its folder. Notes, funding amounts and other writings stay private.

## Planning and writing tools
- **This week:** tasks spread over 7 days (adjust per-day load), words needed per day, copy or email a digest.
- **Scan Gmail:** turns recent review, decision and call emails into tasks. Enable the **Gmail API** in your Cloud project and sign in again to approve read-only Gmail access.
- **Venues:** call deadlines with best-fit writing, fit score from keywords, publisher checklists (Springer, IGI Global, AECT, Web of Conferences; confirm against current author guidelines).
- **Boilerplate** library and a **bid pack** checklist for proposals.
- **Files:** compare two versions of a document (words added and removed); link each reviewer comment to the version that fixed it.
- **Check tab:** word limit, required sections, blind-review terms, and a call-requirements checklist. **Research tab:** ethics to write-up tracker.
- **Insights:** acceptance rate, time to decision by venue, funding by year, promotion tracker (enter policy minimums; target is minimum times the multiplier), reuse map (set *Derived from* in Overview).
- **Search** across everything. Public links can have an expiry date.

## Write with Claude
- Settings → paste your Anthropic API key (kept in this browser only). Open any writing → **Write with Claude**.
- Give it a short brief and the call (upload PDF/Word/text, pick a file already in the writing, or paste). Click **Write proposal**: it reads the call, builds the structure and word limits it asks for, then writes each section using your brief, team, funding amount and Boilerplate library.
- Facts it does not have become `[ADD: …]` placeholders (counted for you). Edit any section, **Rewrite** one with an instruction, then **Save to Drive as Google Doc** (added as a version) or download Word.
- **No API key (Claude Pro only)?** Click *Copy prompt for Claude chat*, paste it into claude.ai (attach the call PDF if prompted), then paste the reply into *Paste a reply from Claude chat* and click *Import as draft*. Same editing and save-to-Drive after that.
- The call, brief and boilerplate are sent to Anthropic with your key and cost API usage. Verify every claim and reference, and check whether the funder allows AI-assisted writing.

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
- Sign-in is remembered in this browser. Google access tokens last about an hour; WriteFlow refreshes them silently in the background. If Google needs interaction, a **Reconnect** button appears (one click). Browser-only OAuth cannot hold a permanent credential, and while the consent screen is in Testing mode Google may ask you to re-approve about every 7 days. Tokens sit in this browser's localStorage, so use it only on devices you trust.
- *Sign out* syncs to Drive, then clears this browser's local copy.
- The sign-in gate protects your Drive data and clears the cache on sign-out; it is not a substitute for locking your device.

## Notes
- Each writing gets a subfolder: `WriteFlow/<title>/`.
- Removing a version from the list never deletes the Drive file.
- Access tokens last ~1 hour; click *Connect Drive* if sync shows "reconnect".
- Keep OAuth in *Testing* mode for personal use (no Google verification needed; test users re-consent about every 7 days).
