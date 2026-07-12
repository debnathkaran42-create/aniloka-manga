# AniLoka — Complete Package (re-verified working build)

Every feature below was tested end-to-end in a real browser right before
this zip was created: signup, admin shortcut login, premium purchase ->
payment.html -> QR code -> UTR submit -> admin approve -> premium unlocked.

## If something says "not connected" / "not a function" again
That means old files are still sitting in your Spck project. Do this:
1. Delete your entire old AniLoka project folder in Spck — don't merge/copy
   over it.
2. Extract this zip fresh, open `aniloka-frontend/` as a brand new project
   in Spck.
3. Fully close and reopen the Spck preview tab before testing.

Copying individual files by hand is what's been causing these mismatches —
starting from a clean extract of this zip avoids it entirely.

## Two folders
**aniloka-frontend/** — the site itself, works now in Spck.
**aniloka-backend/** — optional real server, needs real Node hosting (not Spck).

## Admin login shortcut
On the normal `login.html` form (not admin.html), enter:
- Email: `aniloka@admin.com`
- Password: `KarnaTejas67`
It logs you straight into the admin panel, no second login step.
