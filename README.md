# Daylog

A daily work-summary app. Folders hold projects, projects hold tasks and subtasks.
Log by timer, by ticking a task, or by typing bullets — the day writes itself up,
with charts and a sendable summary.

Single file, no build step, no server. `index.html` is the whole app.

## Run it locally

Open `index.html` in any browser. That's it.

## Put it online (GitHub Pages — free)

1. Create a new repository on GitHub, e.g. `daylog`.
2. Upload `index.html` (and this README) to the repo root — drag and drop works.
3. Repo → **Settings** → **Pages**.
4. Under "Build and deployment", Source = **Deploy from a branch**, Branch = `main`, folder = `/ (root)`. Save.
5. Wait about a minute. Your app is live at `https://<your-username>.github.io/daylog/`.

Open that URL on your phone and use "Add to Home Screen" — it behaves like an installed app.

## Where your data lives

In the browser, on the device you're using. Nothing is sent anywhere.

That means:

- Data survives closing the tab, reloading, and restarting the phone.
- It does **not** move between devices on its own.
- To move it: **Insights → Download backup**, then **Restore backup** on the other device.
- Same-browser rule: data saved in Safari won't show up in Chrome.

Erasing browser site data for this URL erases the log — keep backups if it matters.

## Making it sync across devices

That needs a server and accounts, which a static page can't do alone. The usual
route: add a hosted database (Supabase and Firebase both have free tiers), an
email or Google sign-in, and write entries to that instead of local storage.
The screens for it — sign-in, sync status, offline queue, conflict merge — are
already designed in the companion design file.
