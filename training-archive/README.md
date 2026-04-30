# Training Archive

A standalone web viewer for your Final Surge training history.

## What's in the box

- `index.html` — the viewer (standalone, no build step, no dependencies beyond Google Fonts)
- `archive.json` — your training data (259 sessions, 9 months, 305 comments)

## Running locally

These two files must live in the same folder. The viewer fetches `archive.json` over HTTP, so you can't just double-click the HTML file in Finder — Safari will block the fetch as a CORS violation.

### Quickest way to view locally

Open Terminal, navigate to the folder containing both files, and run:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

## Hosting on GitHub Pages

Since you already have your S&C tracker on Pages, drop these into a sibling folder:

```
your-repo/
├── strength-tracker/    (existing)
│   └── index.html
└── training-archive/    (new)
    ├── index.html
    └── archive.json
```

Commit and push. It'll be live at `https://yourname.github.io/your-repo/training-archive/`.

## Updating the archive

When you eventually stop with Cat (or whenever you want to refresh), re-run the extraction script (`finalsurge-extract-final.js`) in the Final Surge browser console. It downloads a new `final-surge-archive-YYYY-MM-DD-final.json`. Rename that to `archive.json` and replace the existing one.

## Features

**Search tab (default)** — full-text search across exercise names, descriptions, and comments. Filter by session type. Filter to "with comments" or your favourites.

**Browse tab** — chronological week-by-week view, most recent first. Useful for "what was I doing in mid-October?"

**Statistics tab** — weekly volume, session frequency, most-mentioned exercises, comment activity over time.

**Favourites** — click the star on any session card. Saved in browser localStorage. The "★ Favourites" filter on the Search tab shows just the starred sessions.

## Notes

- Favourites are stored per-browser via localStorage. They won't sync between devices and they'll be lost if you clear site data. If you want cross-device sync later, this is the obvious thing to upgrade — likely via Supabase given your existing setup.
- HR data is shown when present; some early walks/runs have no HR.
- "Strides" runs are detected as intervals and have lap splits captured. Easy/recovery runs do not.
- The exercise frequency chart on the Stats page uses simple keyword matching across descriptions. It picks up most common exercises but isn't exhaustive — strange or coach-specific names won't appear.
