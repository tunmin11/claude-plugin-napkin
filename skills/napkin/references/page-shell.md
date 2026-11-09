# Page shell: one artifact per topic, pages stacked inside

Every topic is **one** artifact. Each napkin page is its own HTML file, and a small shell
(`index.html`) shows a strip of all pages with the newest one open.

```
index.html                  ← the shell (published as the artifact's page)
pages/01-overview.html      ← page 1
pages/02-how-it-fits.html   ← page 2 (newest → opens by default)
```

## Rules

- **Adding a page never rewrites an old page.** You change exactly two things: add the new file,
  and append one entry to the `PAGES` array in `index.html`.
- **Same topic, same artifact.** Republish the same `index.html` path, so the artifact keeps its URL.
- **New topic, new artifact.** Never pile unrelated topics into one.
- Page files use two-digit numbers and a short slug: `03-try-it.html`.

## Publishing

**With the Artifact tool:**
- **First page:** publish `index.html` as the page, with
  `files: { "pages/01-<slug>.html": "<local path>" }`. Pick a fitting `icon`.
- **Adding a page:** edit the `PAGES` array, then republish the same `index.html` `file_path` and
  pass **only the new page** in `files`. Files you leave out are kept as they are.
- **The title** is the shell's `<title>`. Pass the same text as the publish `title`, so the topic can be found again later.
- **Coming back in a new conversation:**
  1. Run `action: "list"` and match the topic against artifact titles. If two match, or the match is
     unclear, ask once. Never overwrite on a guess.
  2. `read` that artifact's `url` to get the current `index.html`. Save it locally, append the new
     line to `PAGES`, and write the new page file.
  3. Publish with **`url` set to that artifact** (not a new artifact), `file_path` = your local
     `index.html`, and `files` = only the new page. Without `url`, you'd create a duplicate topic.

**Without the Artifact tool:** write the same tree to `./learn/<topic-slug>/` and tell the user to
open `./learn/<topic-slug>/index.html`. If that folder already exists, add a page to it, but only
when it's clearly the same topic (check its `<title>`). If you're not sure, ask once.

## Every page (each file in `pages/`)

- Is a full document: `<!doctype html>`, `<meta charset="utf-8">`, the viewport meta, and its own `<style>`.
- Defines color tokens on `:root` and handles dark mode the same way the shell does (copy the token block).
- Works at phone width (390px): 16px side gutter, no horizontal page scroll, and tap targets ≥ 40px.
  These guardrails go in every page's CSS:
  ```css
  *, *::before, *::after { box-sizing: border-box; }
  svg, img, canvas, table { max-width: 100%; }
  body { overflow-wrap: anywhere; }
  /* grids: never a fixed column count, let them wrap */
  .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 12px; }
  /* flex rows: wrap, and let children shrink */
  .row { display: flex; flex-wrap: wrap; gap: 8px; } .row > * { min-width: 0; }
  ```
  Before handing over, scan your CSS for `repeat(<number>, …)`, fixed `width:` in px over 340, and
  `white-space: nowrap`. Each one is a sideways-scroll bug on a phone.
- Is self-contained. Scripts may come only from cdnjs.cloudflare.com / cdn.jsdelivr.net/npm /
  unpkg.com with exact versions, and fonts only from Google Fonts. Draw with inline SVG; no external images.
- Has something to **do**, such as a click, toggle, tick, slider or reveal.
- Ends with a **sources footer**:
  ```html
  <footer class="sources">
    <p>Facts checked on YYYY-MM-DD</p>   <!-- today's real date. Or: "Not web-checked: built from your files / general knowledge" -->
    <ol><li><a href="…">Source title</a>: what it was used for</li></ol>
  </footer>
  ```
- Wraps every `localStorage` read and write in `try/catch`, so the page still renders without storage.

## Shell template

Copy it, then change `PAGES`, `<title>`, and, if the user writes in another language, `lang`,
the `latest` label, the `aria-label` and the iframe `title`, so the whole frame speaks their language.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Compound Interest</title>
<style>
  :root { --bg:#faf7f0; --ink:#2b2a27; --muted:#7a756b; --line:#e3dccb; --accent:#c2410c; --chip:#fff; }
  @media (prefers-color-scheme: dark) {
    :root:not([data-theme="light"]) { --bg:#1c1b19; --ink:#ece7dc; --muted:#a39d90; --line:#3b3934; --accent:#fb8a4c; --chip:#262522; }
  }
  :root[data-theme="dark"] { --bg:#1c1b19; --ink:#ece7dc; --muted:#a39d90; --line:#3b3934; --accent:#fb8a4c; --chip:#262522; }
  html, body { margin:0; height:100%; background:var(--bg); color:var(--ink); font:15px/1.4 system-ui, sans-serif; }
  body { display:flex; flex-direction:column; }
  nav { display:flex; gap:8px; padding:10px 16px; border-bottom:1px dashed var(--line); overflow-x:auto; }
  nav button { flex:none; min-height:40px; padding:6px 12px; border:1px solid var(--line); border-radius:999px;
               background:var(--chip); color:var(--ink); font:inherit; cursor:pointer; white-space:nowrap; }
  nav button[aria-current="page"] { border-color:var(--accent); color:var(--accent); font-weight:600; }
  nav small { margin-left:6px; color:var(--accent); font-size:11px; text-transform:uppercase; letter-spacing:.05em; }
  iframe { flex:1; width:100%; border:0; background:var(--bg); }
</style>
</head>
<body>
<nav id="strip" aria-label="Pages in this napkin"></nav>
<iframe id="view" title="Napkin page"></iframe>
<script>
  // Add one line here per new page. Never edit or remove older lines.
  const PAGES = [
    { file: "pages/01-overview.html", title: "Overview" },
  ];
  const KEY = "napkin:" + document.title;
  const strip = document.getElementById("strip"), view = document.getElementById("view");
  const latest = PAGES.length - 1;
  function show(i) {
    view.src = PAGES[i].file;
    strip.querySelectorAll("button").forEach((b, j) =>
      j === i ? b.setAttribute("aria-current", "page") : b.removeAttribute("aria-current"));
    try { sessionStorage.setItem(KEY, String(i)); } catch (e) { /* storage blocked: fine, just don't remember */ }
  }
  PAGES.forEach((p, i) => {
    const b = document.createElement("button");
    b.textContent = (i + 1) + " · " + p.title;
    if (i === latest) b.insertAdjacentHTML("beforeend", "<small>latest</small>");
    b.onclick = () => show(i);
    strip.append(b);
  });
  let start = latest;
  try { const s = Number(sessionStorage.getItem(KEY)); if (s >= 0 && s < PAGES.length && sessionStorage.getItem(KEY) !== null) start = s; } catch (e) { /* use latest */ }
  show(start);
</script>
</body>
</html>
```

The shell remembers the open page only for the current browser session, so a fresh visit always
lands on the newest page.
