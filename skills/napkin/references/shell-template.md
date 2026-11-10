# Shell template

Load this only when creating a new topic, or upgrading an old v1 topic. On later pages, edit
only the `PAGES` array in the existing `index.html`.


Copy it, then change `PAGES`, `<title>`, and, if the user writes in another language, `lang`,
the `latest` label, the `aria-label` and the iframe `title`, so the whole frame speaks their language.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Compound Interest</title>
<link rel="stylesheet" href="napkin.css">
<style>
  html, body { height: 100%; }
  body { display: flex; flex-direction: column; }
  nav { display: flex; gap: 10px; padding: 10px 16px; border-bottom: 1.5px dashed var(--grid); overflow-x: auto; background: var(--paper); }
  nav button { flex: none; min-height: 40px; padding: 4px 14px; border: 1.5px solid var(--ink); border-radius: 999px 999px 999px 999px / 60% 70% 60% 70%;
               background: var(--card); color: var(--ink); font: 600 20px/1 var(--hand); cursor: pointer; }
  nav button[aria-current="page"] { background: var(--note); color: var(--note-ink); transform: rotate(-1.5deg); }
  nav small { margin-left: 6px; color: var(--accent); font: 700 11px var(--body); text-transform: uppercase; letter-spacing: .05em; }
  iframe { flex: 1; width: 100%; border: 0; background: var(--paper); }
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
  try { const s = sessionStorage.getItem(KEY); if (s !== null && +s >= 0 && +s < PAGES.length) start = +s; } catch (e) { /* use latest */ }
  show(start);
</script>
</body>
</html>
```

The shell remembers the open page only for the current browser session, so a fresh visit always
lands on the newest page.
