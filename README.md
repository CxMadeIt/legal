# CxMadeIt — app legal & support pages

One public site serving the Privacy Policy, Terms of Use and Support page for
every CxMadeIt app. App Store Connect requires a **publicly reachable URL** for
privacy policy and support — in-app text does not satisfy those fields.

Plain static HTML. No Jekyll, no build step, no dependencies (`.nojekyll` tells
GitHub Pages to serve the files as-is). Edit a file, push, it's live.

## Live URLs

Base: `https://cxmadeit.github.io/legal/`

| App | Privacy | Terms | Support |
|---|---|---|---|
| VitaMaxx | `/legal/vitamaxx/privacy/` | `/legal/vitamaxx/terms/` | `/legal/vitamaxx/support/` |
| Pomo Pomo Arcade | `/legal/pomopomoarcade/privacy/` | `/legal/pomopomoarcade/terms/` | `/legal/pomopomoarcade/support/` |

## First-time publish

```bash
cd ~/Documents/legal
gh repo create legal --public --source=. --remote=origin --push
```

Then GitHub → the `legal` repo → **Settings → Pages → Source: `main`, folder
`/ (root)`**. Live in about a minute.

The repo **must be public** — GitHub Pages from a private repo requires a paid
plan. Nothing here is sensitive; it's the same text that ships inside the apps.

## Adding an app

```bash
cp -R _template myapp
```

Then in `myapp/`, replace the placeholders:

- `APPNAME` — the app's display name
- `EFFECTIVE_DATE` — e.g. `July 6, 2026`
- `ONE-LINE TAGLINE` and the `lede` paragraphs
- The commented guidance in each section — write real copy, delete the notes

Add a row to the `cards` list in the root `index.html`, then `git push`.

## Rules of thumb

- **Every app needs a working delete path**, and the privacy policy must name
  the exact screen and button. This is the single most common App Review
  rejection for apps with no accounts.
- **Match the app.** These pages are a legal statement about what the software
  actually does. If an app adds analytics, a backend or accounts, update its
  privacy policy *and* its App Store privacy label in the same release.
- **Keep the in-app copy and the hosted copy in sync.** For VitaMaxx the source
  of truth is `VitaMaxx/Profile/LegalTexts.swift`; change both together.
- **Bump the effective date** whenever the substance changes.
- Health, finance and safety-adjacent apps: keep the "what this is not"
  section explicit. It's what keeps you clear of Guideline 1.4.1.
