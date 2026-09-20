# ClinicShift Roster

A cloud-style clinic staff shift roster & HR approval system — role-based dashboards, a monthly roster approval workflow, a live roster, shift-change requests, leave management, staffing-coverage shortage detection, an audit trail, and CSV reports. Single self-contained `index.html` file, seeded with 20 demo employees for a fictional clinic.

## Publish it on GitHub Pages (free, no build step)

1. Create a new repository on GitHub (e.g. `clinicshift-roster`), or use an existing one.
2. Add this `index.html` file to the **root** of the repository (or to a `/docs` folder — see step 4).
3. Commit and push it.
4. In the repo, go to **Settings → Pages**. Under "Build and deployment", set **Source: Deploy from a branch**, pick the branch (usually `main`) and the folder (`/root` or `/docs`, matching where you put `index.html`). Save.
5. GitHub will give you a URL like `https://<your-username>.github.io/<repo-name>/`. It usually goes live within a minute or two.
6. Share that link with your team.

No server, database sign-up, or build tooling is required — it's a single HTML file.

## Important: what "everyone" sees on GitHub Pages

This static version keeps its data in each visitor's own browser (`localStorage`), **not** in a shared database. That means:

- Each person who opens the link has their **own independent copy** of the roster — if HR edits and confirms a roster on their laptop, a manager opening the same link on their phone will **not** see that change automatically.
- Data survives page reloads and browser restarts for that one person, on that one device/browser, but clearing site data or switching browsers loses it.
- It's genuinely useful for: a single person maintaining the roster on one device, training/demoing the workflow, or a small team that agrees one person (HR) is the source of truth and periodically exports/shares data (see **Settings → Export All Data**) with everyone else.

**If you need one shared, real-time roster that every device sees the same live data for** — matching the "cloud database", "multi-user", "real-time" requirements in the original spec — you have two options:

1. **Use the Claude-hosted version** of this same app (the one already built for you in this conversation). It runs on a real shared cloud database, so HR, managers and employees on different devices all see the same live roster the moment it's published. This is the quickest path to true multi-user behavior with zero extra setup.
2. **Wire this static file to a free backend** such as Firebase Firestore or Supabase (both have generous free tiers). This involves adding that provider's SDK script tag and replacing the small set of `S.db`-guarded functions in the code (search for `doSaveState`, `saveMonth`, `ensureMonthLoaded`, `boot`) with calls to that backend instead of `localStorage`. The rest of the app (UI, workflow, validation) doesn't need to change. This is a real (if modest) engineering task, not a config toggle — happy to help build it out if you want to go this route.

## Files

- `index.html` — the entire application (demo data included, no external dependencies except Google Fonts).

## Local testing

Just open `index.html` directly in a browser, or serve the folder with any static file server (`python3 -m http.server`, VS Code "Live Server", etc.).
