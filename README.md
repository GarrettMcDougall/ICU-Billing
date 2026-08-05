# ICU Billing Guide (Ontario)

A single-file, mobile-friendly quick-reference for Ontario OHIP billing in the ICU/CCU —
per-diem team fees, FFS critical care, consult/assessment codes by base specialty
(Emergency Medicine, Internal Medicine, Anesthesiology), procedures, dialysis/CRRT,
CritiCall & phone consults, special visit premiums, and more.

**Live in your browser — nothing to install.** Open `index.html` directly, or host it
(see below) and bookmark it on your phone for point-of-care use.

## Features

- **Search** — filter every code/description across all sections at once
- **Favourites (★)** — tap the star on any row to pin it to a "Favourites" section at
  the top; persists locally between visits
- **Base-specialty toggle** — Consult/Assess codes switch between EM, Internal
  Medicine, and Anesthesiology, remembering your choice
- **Collapsible (i) info panels** — tap the circled *i* on select rows for the
  underlying payment rule, without cluttering the main list
- **Procedural sedation calculator** — builds the "C"-suffix sedation code set
  (base + time + ASA class + age band + modifiers + evening/night premium) with a
  searchable procedure library, and a "Copy codes" button
- **Auto-update check** — if you host this and bump `version.txt`, open tabs will
  show a one-tap "Update now" banner (see [Deploying updates](#deploying-updates))

All data is stored **only in the browser's local storage** — favourites and your
specialty choice never leave the device, and nothing is sent to a server.

## ⚠️ Before you rely on this

This is a **personal reference tool**, not an official publication. Fee values are
manually compiled from:

- the Ontario *Schedule of Benefits: Physician Services* (amendment effective
  March 3, 2025), and
- the Ministry of Health *Fee Code Table 4: Value Changes to Fee Schedule Codes*
  (effective April 1, 2026)

Fees change at least annually, codes get added/retired, and interpretation rules are
occasionally clarified or reversed by the Ministry. **Verify anything that affects an
actual claim against the current Schedule of Benefits or your billing agent** —
especially anything tagged "SOB" (fee not confirmed) in the guide itself.

This tool is not affiliated with, endorsed by, or reviewed by the Ontario Ministry of
Health, OHIP, or the OMA.

## Using it yourself

**Simplest option:** download `index.html` and open it in any browser. Works fully
offline once loaded.

**To share a link with others (recommended):**

1. Push this repo to GitHub (see below).
2. Settings → Pages → deploy from the `main` branch, root folder.
3. GitHub gives you a URL like `https://yourname.github.io/icu-billing-guide/` —
   share that. Anyone can open it, and it works great saved to a phone home screen
   (Safari/Chrome → Share → *Add to Home Screen*).

## Deploying updates

When you edit `index.html` to fix a fee or add a code:

1. Bump the version string in **two places** so they match:
   - The `LOCAL_VERSION` constant near the bottom of the `<script>` block
   - The footer text (`<span id="verstamp">`)
2. Overwrite `version.txt` in the repo root with that same new version string.
3. Commit and push both files together.

Anyone with the page already open will see an "A newer version is available — Update
now" banner within a few seconds of it going live. This only works when the file is
hosted somewhere reachable (e.g. GitHub Pages) — a locally-opened file has no
`version.txt` to check against and the update check simply fails silently.

## Repo structure

```
.
├── index.html      the entire app — markup, styles, and logic in one file
├── version.txt      current version string, checked by index.html for updates
├── README.md        this file
└── LICENSE
```

There's no build step, no dependencies, and no backend. It's plain HTML/CSS/JS.

## Contributing / editing

Everything lives in one `<script>` block in `index.html`:

- `SPECIALTIES` — the per-specialty Consult/Assess code tables
- `SECTIONS` — every other section, in nav order
- Each row is `{ code, desc, price }`, optionally with `moreInfo` (adds a collapsible
  (i) button) — omit `price` to show a muted "SOB" tag instead of a dollar figure
- `sub: '...'` inserts a small section label; `info: '...'` and `note: '...'` insert
  always-visible blue/red callouts

No JS framework, no build tooling — edit the object literals directly and refresh.

## License

Code (the HTML/CSS/JS structure) is released under the [MIT License](LICENSE) — do
whatever you like with it.

The billing content itself (code descriptions, fees, payment rules) is derived from
public Ontario government and professional-association publications and is provided
as-is for informational purposes; see the disclaimer above before relying on it.
