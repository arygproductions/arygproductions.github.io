# How to edit your website (beginner guide)

Your whole website is **one file**: `index.html`. This guide shows you how to
change it safely. (For the technical/hosting details, see `README.md`.)

Open the file two ways:
- **To view it:** double-click `index.html` → it opens in your web browser.
- **To edit it:** right-click `index.html` → *Open With* → **TextEdit** (Mac) or
  **Notepad** (Windows). Or use the free editor [VS Code](https://code.visualstudio.com/).

After any change: **save the file**, then **publish it** (see the last section)
to update the live site at https://arygproductions.com.

---

## 1. Change your name / headline

Near the top of `index.html`, find the `SITE SETTINGS` block:

```
<span class="badge">Aryg Productions</span>
<h1>Aryg Apps</h1>
<p class="tagline">One place for all my projects ...</p>
```

- The small label is the `badge` (currently `Aryg Productions`).
- The big title is between `<h1>` and `</h1>` (currently `Aryg Apps`).
- The sentence under it is the `tagline`.

Type whatever you want between the tags. Don't delete the tags themselves.

---

## 2. Add or change an app (the main thing)

Find the section marked `THE ONLY LIST YOU NEED TO EDIT`. Each app is one block
inside `{ }`. Right now there is one app, Omzulink:

```
{
  name: "Omzulink",
  icon: "🔗",
  desc: "Send files and quick messages between your phone and your Mac ...",
  tags: ["macOS", "Android", "iOS", "Wi-Fi"],
  docs: "https://github.com/arygproductions/Omzulink#readme",
  github: "https://github.com/arygproductions/Omzulink",
  download: "https://github.com/arygproductions/Omzulink/releases/latest"
}
```

To **add an app**: copy the whole `{ ... }` block, paste it right after the
existing one, and put a comma between them, like this:

```
const APPS = [
  { ...first app... },
  { ...second app... }
];
```

To **edit an app**: change the text inside the quotes.
To **remove an app**: delete its `{ ... }` block.

Field meanings:
- `name` — the app's name.
- `icon` — any emoji (decoration only).
- `desc` — one or two sentences.
- `tags` — short labels in `[ ]`, e.g. `["iOS", "Swift"]` (optional).
- `docs` — link to documentation; use `""` if none yet.
- `github` — link to the repo; use `""` if none yet.
- `download` — link to a downloadable release (shows a highlighted **Download** button); use `""` if none.

Rules so you don't break it: keep the quotes `"`, keep a comma after each `}`
(except you can leave the last one off), and don't remove the square brackets `[ ]`.

You can't seriously break anything — if a change looks wrong, undo it
(Ctrl+Z / Cmd+Z), save, and publish again.

---

## 3. Publish your changes (make them live)

Your site lives in a GitHub repository, and it updates itself ~1 minute after
you upload a changed file.

1. Go to **https://github.com/arygproductions/arygproductions.github.io**
   (sign in as `arygproductions`).
2. Click **Add file → Upload files**.
3. Drag your edited `index.html` into the page (same filename replaces the old one).
4. Click the green **Commit changes** button (leave it on the `main` branch).
5. Wait about a minute, then refresh https://arygproductions.com to see it.

That's it. The custom domain, HTTPS, and search setup are already handled — you
only ever need to edit `index.html` and re-upload it.

---

## 4. Where everything else lives

You normally won't touch these, but for reference:
- `sitemap.xml`, `robots.txt` — help Google find the site.
- `CNAME` — connects the domain; don't delete it.
- `README.md` — full technical notes for a developer (domain, DNS, hosting, SEO).
