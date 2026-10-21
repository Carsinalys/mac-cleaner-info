# MacCleaner — support & privacy site

Static support surface for the macOS app **MacCleaner**, hosted on GitHub Pages.
It satisfies the two URLs App Store Connect requires (see
`mac-cleaner/docs/app-store-listing-copy.md` § 8).

No build step, no dependencies, no JavaScript required to read the contact
information — plain HTML + one stylesheet, so App Review's crawler always sees
the support email.

## Files

| Path | Purpose |
|---|---|
| `index.html` | Support page — contact, getting started, features, troubleshooting, FAQ |
| `privacy.html` | Privacy policy — matches the App Privacy nutrition label (no data collected) |
| `assets/styles.css` | Design tokens mirrored from the app's `DesignSystem.swift` (blue accent) |
| `assets/icon-*.png` | App icon, copy from `MacCleaner/Resources/Assets.xcassets/AppIcon.appiconset` |
| `assets/favicon-32.png` | Small favicon, derived from the app icon |
| `.nojekyll` | Serve files as-is, skip Jekyll processing |

## Before first deploy

- [ ] Copy the app icon PNGs into `assets/` (from `MacCleaner/Resources/`)
- [ ] Confirm the support email and reply-time promise are ones you can keep
- [ ] A postal address is offered "on request" in `privacy.html`. Some
      jurisdictions require it published; add it if yours does.

## Enabling GitHub Pages

1. Push to `main`.
2. Repository → **Settings** → **Pages**.
3. **Source:** Deploy from a branch. **Branch:** `main`, folder `/ (root)`. Save.
4. Wait for the first deploy, then confirm both URLs load over HTTPS.

## Paste into App Store Connect

| ASC field | Value |
|---|---|
| Support URL | `https://carsinalys.github.io/mac-cleaner/` |
| Privacy Policy URL | `https://carsinalys.github.io/mac-cleaner/privacy.html` |
| Marketing URL (optional) | leave empty, or reuse the support URL |

Apple checks that the support URL resolves, needs no login, works on a phone,
and offers a real contact method. All three are satisfied by `index.html`.

## Links from the app to this site

Apple doesn't require an in-app link to the landing page, but for a good user
experience you can add one. Review-safe placements:

- **Settings → About section**: add a "Visit Support Page" link
  (opens `https://carsinalys.github.io/mac-cleaner/`)
- **Onboarding view**: optionally link "Learn more about privacy"
  (opens `privacy.html`)
- **FAQ answers that reference the privacy policy** could link to the
  hosted page instead of only describing it

**Do NOT** link to the marketing/sales page from anywhere inside the purchase
flow (that would be a Guideline 3.1.1 issue — steering to external purchases).
Linking from Settings to a **support** page that happens to also mention the
app is fine.

## Keeping it accurate

The page states facts that come from the app. Re-check them when the app
changes:

- **macOS 14 Sonoma** — `MACOSX_DEPLOYMENT_TARGET` in `MacCleaner/project.yml`.
- **$9.99 lifetime** — the IAP price in App Store Connect.
- Feature names match the app's tabs (Overview, Cleanup, Uninstaller, Duplicates, Visualizer, Settings).
- The page deliberately does **not** claim "best" anything, RAM/memory
  optimization, or specific reclaimed-space numbers.

Update the "Page last updated" date in both footers when you change content, so
the page doesn't read as abandoned.

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000/
```
