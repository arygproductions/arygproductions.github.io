# Aryg Apps — Documentation Hub

Live site: **https://arygproductions.com**
Also reachable at: https://www.arygproductions.com and https://arygproductions.github.io

A single-page website that acts as a hub linking to Aryg Productions' apps —
their documentation and GitHub repositories. Built as one static HTML file,
hosted free on GitHub Pages, on a custom domain bought at Porkbun, with
automatic HTTPS.

This README is the handoff document for the next developer. It explains how
everything fits together and how to make changes safely.

---

## 1. Tech stack (intentionally simple)

- **One static file**: `index.html` contains all HTML, CSS, and JavaScript.
  No build step, no framework, no dependencies, no package manager.
- **Hosting**: GitHub Pages (free), serving the `main` branch of the repo
  `arygproductions/arygproductions.github.io`.
- **Domain/DNS**: registered and managed at **Porkbun**.
- **HTTPS**: issued automatically by GitHub Pages (Let's Encrypt). Nothing to renew.

If you can edit a text file and drag it onto a web page, you can maintain this site.

---

## 2. Repository contents

| File            | Purpose |
|-----------------|---------|
| `index.html`    | The entire website (content + styling + logic). |
| `sitemap.xml`   | Lists pages for search engines. Update `<lastmod>` when content changes. |
| `robots.txt`    | Allows crawling; points crawlers to the sitemap. |
| `CNAME`         | Contains `arygproductions.com`. Tells GitHub Pages the custom domain. **Do not delete.** |
| `README.md`     | This document. |
| `EDIT-ME-GUIDE.md` | Beginner-friendly guide to editing content. |

---

## 3. How content is structured (editing the apps)

All app cards are generated from a single JavaScript array near the bottom of
`index.html`, marked with a big comment banner:

```js
const APPS = [
  {
    name: "Omzulink",
    icon: "🔗",
    desc: "Send files and quick messages between your phone and your Mac over your own Wi-Fi ...",
    tags: ["macOS", "Android", "iOS", "Wi-Fi"],
    docs: "https://github.com/arygproductions/Omzulink#readme",
    github: "https://github.com/arygproductions/Omzulink",
    download: "https://github.com/arygproductions/Omzulink/releases/latest"
  }
];
```

To **add an app**, copy a `{ ... }` block, paste it after the previous one
(comma-separated), and edit the fields. Optional fields — `docs`, `github`, and
`download` — can be `""` (or omitted) if not applicable. `download` renders a
highlighted **Download (Mac)** button (used here for the signed `.dmg` on the
GitHub Releases page). See `EDIT-ME-GUIDE.md` for a gentler walkthrough.

Branding lives in the header/footer of `index.html`:
- Small label (badge): `Aryg Productions`
- Main heading (`<h1>`): `Aryg Apps`
- Footer: `Built by Aryg Productions`

---

## 4. How to deploy a change

GitHub Pages auto-deploys whenever `main` changes. The web-based flow (no git
required):

1. Edit `index.html` (or any file) locally.
2. Go to the repo: https://github.com/arygproductions/arygproductions.github.io
3. **Add file → Upload files**, drag the changed file in (same filename
   overwrites), and **Commit changes** to the `main` branch.
4. Wait ~1 minute. The live site at https://arygproductions.com updates itself.

If you use git locally instead, `git push` to `main` does the same thing.

---

## 5. Hosting details (GitHub Pages)

- Repo: `arygproductions/arygproductions.github.io` (public).
- The repo name `<user>.github.io` makes it the account's root Pages site.
- Settings → Pages: Source = "Deploy from a branch", Branch = `main` / `(root)`.
- Custom domain field = `arygproductions.com`; "Enforce HTTPS" is enabled.
- The `CNAME` file in the repo mirrors that custom-domain setting — keep them in sync.

---

## 6. Domain & DNS (Porkbun)

Registrar: **Porkbun**, domain `arygproductions.com` (auto-renew on).
DNS is managed at Porkbun → Domain → DNS. Current records:

| Type  | Host (name) | Value | Why |
|-------|-------------|-------|-----|
| A     | (blank/root)| 185.199.108.153 | GitHub Pages |
| A     | (blank/root)| 185.199.109.153 | GitHub Pages |
| A     | (blank/root)| 185.199.110.153 | GitHub Pages |
| A     | (blank/root)| 185.199.111.153 | GitHub Pages |
| CNAME | www         | arygproductions.github.io | Makes www work / redirect to apex |
| TXT   | (blank/root)| google-site-verification=SS2sqGe43VAWawXprwXcicStt9x-lYPCTYT5k23EASo | Google Search Console ownership. **Do not delete.** |

Notes:
- The four GitHub A records are the official GitHub Pages apex IPs. If GitHub
  ever changes them, update here (see GitHub Pages docs: "Managing a custom domain").
- The TXT record is a public verification token (safe to expose), but removing
  it un-verifies Google Search Console access.
- When editing DNS in Porkbun's bulk editor, keep **"Do not delete existing
  records"** checked unless you intend to replace the whole zone.

### Gotcha that bit us during setup
Newly registered Porkbun domains ship with a free **"Link in Bio" URL forward**
that hijacks the root domain (it resolves to Porkbun's parking IPs like
`44.230.85.241`). It must be cancelled (Porkbun → Domain → the "website" icon →
"cancel service") so the GitHub A records take effect. If the site ever starts
showing a Porkbun parking page, check this first.

---

## 7. HTTPS

GitHub Pages provisions and renews a free certificate automatically once DNS
points at GitHub. After any custom-domain change it can take a few minutes to
an hour for the cert (including the `www` variant) to issue. A brief
"certificate invalid" warning during that window is normal — never bypass it,
just wait. `https://arygproductions.com` is the canonical address.

---

## 8. SEO / search

Already in place:
- `<title>`, meta `description`, `canonical`, Open Graph, and Twitter tags in `index.html`.
- JSON-LD structured data (`Organization` + `WebSite`) identifying the brand
  "Aryg Productions" and linking to the GitHub account.
- `sitemap.xml` and `robots.txt`.
- **Google Search Console**: domain property `arygproductions.com` verified (via
  the DNS TXT record above); `sitemap.xml` submitted; homepage indexing requested.

Maintenance:
- When you add/redesign pages, update `sitemap.xml` (`<loc>` and `<lastmod>`)
  and re-submit it in Search Console if needed.
- Indexing a brand-new site takes days to weeks. The unique term
  "arygproductions" should rank well once indexed; the generic "arya production"
  is a crowded term and is not targeted organically.
- Inbound links (the app's GitHub README, store listings, social profiles
  pointing to arygproductions.com) speed up trust and indexing.

---

## 9. Accounts involved (credentials NOT stored here)

- **Porkbun** — domain & DNS.
- **GitHub** (`arygproductions`) — code hosting & GitHub Pages.
- **Google Search Console** — indexing/visibility.

Logins are held by the owner. Nothing secret is stored in this repo.

---

## 10. Quick troubleshooting

| Symptom | Likely cause / fix |
|---------|--------------------|
| Site shows a Porkbun "parking" page | Re-enabled Link-in-Bio forward, or A records changed — see §6. |
| `www` shows "connection not private" | Cert for `www` not issued yet — wait up to ~1 hr after DNS/domain changes. |
| Change not appearing | Pages still deploying (~1 min); or browser cache — hard refresh. |
| Search Console lost access | The Google TXT record was removed from DNS — re-add it (§6). |
| Custom domain reverted in Pages | The `CNAME` file was deleted/overwritten — it must contain `arygproductions.com`. |
