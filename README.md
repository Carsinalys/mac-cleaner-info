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
| `privacy.html` | Privacy policy — matches the App Privacy nutrition label (no data collected); also covers support emails |
| `terms.html` | Terms of use — points to Apple's Standard EULA and explains the deletion risks (use at your own risk, back up first) |
| `assets/styles.css` | Design tokens mirrored from the app's `DesignSystem.swift` (blue accent) |
| `assets/icon-*.png` | App icon, copy from `MacCleaner/Resources/Assets.xcassets/AppIcon.appiconset` |
| `assets/favicon-32.png` | Small favicon, derived from the app icon |
| `.nojekyll` | Serve files as-is, skip Jekyll processing |

## Before first deploy

- [ ] Copy the app icon PNGs into `assets/` (from `MacCleaner/Resources/`)
- [ ] Confirm the support email and reply-time promise are ones you can keep
- [ ] The pages name no individual: the publisher is "the developer shown as
      seller on the App Store product page". If you distribute in the EU as a
      trader, Apple itself publishes your name, address, phone and email on the
      EU product page (Digital Services Act) — that can't be avoided by the site.
- [ ] Keep Apple's Standard EULA in App Store Connect (App Information →
      License Agreement), or paste `terms.html` there as a custom EULA. A web
      page alone is not a contract; the EULA the buyer accepts is.

## Enabling GitHub Pages

1. Push to `main`.
2. Repository → **Settings** → **Pages**.
3. **Source:** Deploy from a branch. **Branch:** `main`, folder `/ (root)`. Save.
4. Wait for the first deploy, then confirm both URLs load over HTTPS.

## Paste into App Store Connect

| ASC field | Value |
|---|---|
| Support URL | `https://carsinalys.github.io/mac-cleaner-info/` |
| Privacy Policy URL | `https://carsinalys.github.io/mac-cleaner-info/privacy.html` |
| Marketing URL (optional) | leave empty, or reuse the support URL |

Apple checks that the support URL resolves, needs no login, works on a phone,
and offers a real contact method. All three are satisfied by `index.html`.

## Links from the app to this site

Guideline 5.1.1(i) requires the privacy policy to be linked **inside the app**
as well as in App Store Connect. The app links to these pages from:

- **Settings → About**: Visit Support Page, Privacy Policy, Terms of Use
- **Unlock Cleaning (purchase) sheet**: Terms of Use, Privacy Policy
- **Review and dry-run steps of every deletion**: Terms of Use

The URLs live in `AppInfo` (`supportURL`, `privacyPolicyURL`, `termsOfUseURL`)
in the app repo — change them there if the site moves.

**Do NOT** link to the marketing/sales page from anywhere inside the purchase
flow (that would be a Guideline 3.1.1 issue — steering to external purchases).
Linking from Settings to a **support** page that happens to also mention the
app is fine.

## Keeping it accurate

The page states facts that come from the app. Re-check them when the app
changes:

- **macOS 14 Sonoma** — `MACOSX_DEPLOYMENT_TARGET` in `MacCleaner/project.yml`.
- **No prices on the site** — the price differs per storefront and a wrong
  price is a Guideline 2.3.1 problem; the site says "one-time purchase" instead.
- **No safety guarantees** — describe safeguards, never promise that nothing
  can be lost. The app shows the same "you decide what is removed" notice in
  the review and dry-run steps.
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
