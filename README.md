# Daylog — synced version

Same app, plus Google sign-in and cloud sync. One file, no build step, no server
of your own. Your Firebase project (`daylog-dbb57`) is already wired in.

## Deploy it (GitHub Pages)

1. New GitHub repo, e.g. `daylog`.
2. Upload `index.html` and this README to the repo root.
3. Settings → Pages → Source: **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. Live at `https://<your-username>.github.io/daylog/` in about a minute.

## Two things to switch on in Firebase (one-time)

**1. Authorize your domain.** Firebase console → Authentication → Settings →
Authorized domains → Add domain → `<your-username>.github.io`.
Without this, Google sign-in is rejected.

**2. Lock the database to each user.** Firestore Database → Rules → paste this → Publish:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```

That means only you can read or write your own log — nobody else, even though
the page itself is public.

## Using it

- Open the URL, **Continue with Google**. Log your day.
- Open the same URL on your laptop, sign in with the same Google account —
  everything's there, including a running timer.
- On your phone: Share → **Add to Home Screen**. It opens like an app.
- The status pill next to the date reads *Synced*, *Offline — queued*, or *This device*.

**Offline:** entries and ticks are saved locally and pushed when you reconnect.
Merging is per item, so a day edited on two devices keeps both sets of bullets
rather than one overwriting the other.

**"Just use this device"** on the sign-in screen skips the cloud entirely —
everything stays in that browser. You can sign in later from Insights and what
you already logged gets uploaded.

## Notes

- Google sign-in only works over http/https (GitHub Pages, or a local server).
  Opening `index.html` straight off your disk will offer device-only mode instead.
- The `apiKey` in this file is meant to be public; the security rules above are
  what protect your data.
- Insights → **Download backup** writes a JSON file; **Restore backup** merges it
  back in. Worth doing occasionally regardless of sync.
- Free tier limits are far beyond one person's daily log.
