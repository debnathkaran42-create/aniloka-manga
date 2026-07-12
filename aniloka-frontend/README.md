# AniLoka — Manga Reading Platform

A static, mobile-only manga reading site. Pure HTML5 + CSS3 + vanilla
JavaScript (ES6+) — no frameworks, no build step, no Node required.
Works directly in **Spck Editor** (or any static file host/server).

Auth, "database", ads, and payments currently run on **local, simulated
logic** (see "What's simulated" below) so the whole app works end-to-end
right now, with clear notes on where to plug in real services later.

---

## Opening this in Spck Editor

1. Unzip this folder.
2. In Spck Editor: **Open Folder** → select the unzipped `aniloka` folder.
3. Tap `index.html` → **Run** (Spck's built-in live server / preview).
4. Use the preview on your phone (or Spck's device preview) — this build
   is designed mobile-only, so it will look best on a phone-sized screen.

No install step, no `npm install` — every file is plain HTML/CSS/JS.

---

## Folder structure

```
aniloka/
├── index.html            Splash screen (entry point)
├── login.html             Log in
├── signup.html            Sign up
├── home.html               Home feed (rails, hero, genres)
├── manga-details.html       Manga info + chapter list + reviews
├── reader.html               The manga reader
├── search.html                 Search + filters
├── profile.html                 Profile, library tabs, settings
├── library.html                  Favorites / reading / completed / etc.
├── premium.html                   Plans + simulated checkout
├── admin.html                      Admin panel (manga/chapters/users/ads/premium/homepage)
├── css/                             One stylesheet per page + main.css (shared)
├── js/                               One script per page + shared data.js / auth.js / main.js
├── data/genres.json                  Reference copy of the genre list
└── images/
    ├── manga/covers/                  <manga-id>.jpg
    ├── manga/banners/                  <manga-id>.jpg
    ├── manga/chapters/<id>/<ch-id>/     1.jpg, 2.jpg, ...
    └── assets/                          misc site assets
```

---

## How data works right now

Everything reads/writes through the `DB` object in `js/data.js`, which
wraps `localStorage`. This means:

- Manga/chapters you add in the **Admin Panel** persist in your browser's
  local storage — they will **not** sync across devices/browsers.
- User accounts, favorites, bookmarks, and reading progress are all
  per-browser too.
- Two placeholder titles — **"Manga 1"** and **"Manga 2"** — are seeded
  in `js/data.js` (`SEED_MANGA`) so pages aren't empty while you test.
  Edit them from the Admin Panel, or rename in the source directly.

When you're ready for a real multi-device database, keep every method
name in `DB` the same and swap the bodies for calls to your backend of
choice (Firebase Firestore, Supabase, your own API, etc.) — no other
page needs to change.

---

## What's simulated (and how to go live later)

| Feature | Right now | To go live |
|---|---|---|
| Login / Signup | Local, plaintext in `localStorage` (`js/auth.js`) | Swap `AUTH` methods for real backend/Firebase Auth calls |
| Payments (Premium) | Simulated checkout, no real charge (`js/premium.js`) | Replace `confirmPurchase()` with a Stripe Checkout/Payment Link redirect |
| Ads | Styled placeholder boxes (`.ad-slot` in `css/main.css`) | Swap in your ad network's real script + unit IDs once your domain is approved |
| Manga page images | Placeholder boxes showing the expected file path | Drop matching images into `images/manga/chapters/...` |

## Admin Panel

Go to `admin.html`. Demo login:

```
Email:    aniloka@admin.com
Password: KarnaTejas67
```

Change these in `js/admin.js` (`ADMIN_CREDENTIALS`) before sharing this
project with anyone else — this is a simple hardcoded check, not real
security, since there's no backend to enforce permissions yet.

From the Admin Panel you can:
- Add / edit / delete manga (cover & banner are **file paths**, not uploads —
  you place the actual image files into `images/manga/...` yourself)
- Add / edit / delete chapters (set a page count; the form shows you the
  exact folder path to drop page images into)
- Grant/revoke Premium for any user
- Toggle ads on/off site-wide
- Choose the homepage's featured (hero) manga

## Genres

Genres are a placeholder list (`Genre 1`...`Genre 8`) in `js/data.js`
(the `GENRES` array) and mirrored in `data/genres.json` for reference.
Replace the array in `js/data.js` with your real list — search, the
admin genre checklist, and the homepage genre strip all read from it
automatically.
