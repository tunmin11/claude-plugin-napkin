# Page shell: one artifact per topic, pages stacked inside

Every topic is **one** artifact. Each napkin page is its own HTML file. A small shell
(`index.html`) shows a strip of all pages with the newest one open.

```
index.html                  ← the shell (published as the artifact's page)
napkin.css                  ← shared look, from references/napkin-css.md (written once)
notes.md                    ← memory for Claude (not linked from the shell)
pages/01-overview.html      ← page 1
pages/02-how-it-fits.html   ← page 2 (newest → opens by default)
```

## Rules

- **Adding a page never rewrites an old page.** Add the new file, append one entry to `PAGES` in
  `index.html`, and append to `notes.md`. Nothing else changes.
- **Fix one part** ("redo the picture", "simpler step 3"): rewrite only that section of that one
  page file. Leave the rest of the file byte-for-byte as it was.
- **Same topic, same artifact.** Republish the same `index.html` path, so the artifact keeps its URL.
- **New topic, new artifact.** Never pile unrelated topics into one.
- Page files use two-digit numbers and a short slug: `03-try-it.html`.

## notes.md: memory for the next session

Written for Claude, not for people: compact lines, no prose. Read it first whenever you come back
to a topic. It saves re-reading files and re-asking questions.

```
# notes: <topic title>
## Sources
<relative path or URL> | <headings, comma-separated> | <mtime or size or short hash> | read: <full|map>
## Facts
F<n> | <claim in plain words> | "<quote, ≤ 25 words>" | <source + heading> | <ok|disagree|general knowledge|outdated>
## Learner
knows: … | for: … | metaphor world: … | language: …
## Pages
<NN> | <slug> | <title> | <angle> | <shape> | <metaphor or ->
```

- **Privacy:** anyone with the artifact link can open `notes.md` by its path. Keep only short
  quotes, paths **relative** to the folder the user gave (never absolute, never `~/…`), and the
  learner's quick answers. Never copy whole passages from their files.
- **Append only.** Add new lines. The only edit to old lines: change a fact's status to `outdated`
  when its file changed and the claim no longer holds.
- **Changed files:** on coming back, compare each source's recorded mtime/size/hash with the
  file now. Re-read only files that changed, or that the new angle needs.

## Publishing

**With the Artifact tool:**
- **First page:** write `napkin.css` (the block in `references/napkin-css.md`, unchanged),
  `notes.md` and the page. Publish `index.html` as the page with
  `files: { "napkin.css": "<local>", "notes.md": "<local>", "pages/01-<slug>.html": "<local>" }`.
  Pick a fitting `icon`. Pass the shell's `<title>` as `title`.
- **Adding a page:** append to `PAGES` and to `notes.md`, then republish the same `index.html`
  `file_path` with `files` = the new page and `notes.md` only. Files you leave out are kept.
- **Fix one part:** republish with `files` = that page and `notes.md` only.
- **Coming back in a new conversation:**
  1. `action: "list"`, match the topic against artifact titles. If two match, or the match is
     unclear, ask once. Never overwrite on a guess.
  2. `action: "read"` with that `url` and `path: "notes.md"` **first**. Then read the current
     `index.html`. Save both locally. Don't read old page files unless fixing one of them.
  3. Publish with **`url` set to that artifact**, `file_path` = your local `index.html`, and
     `files` = only what changed. Without `url`, you'd create a duplicate topic.
- **Old v1 topic** (no `notes.md` in the artifact): build `notes.md` from the existing pages'
  titles and sources footers (best effort; mark facts you can't trace as `general knowledge`),
  write `napkin.css`, and replace the shell with `references/shell-template.md` (keep its `PAGES` lines).
  Publish all three with the new page. Old page files stay untouched and keep their old look.
  If one of them gets a "fix one part", switch that page to `../napkin.css` at the same time.

**Without the Artifact tool:** write the same tree to `./learn/<topic-slug>/` and tell the user to
open `./learn/<topic-slug>/index.html`. If that folder already exists, read its `notes.md` first
and add a page, but only when it's clearly the same topic (check its `<title>`). If unsure, ask once.

## Every page (each file in `pages/`)

- Is a full document: `<!doctype html>`, `<meta charset="utf-8">`, the viewport meta,
  `<link rel="stylesheet" href="../napkin.css">`, and a small `<style>` for page-only CSS.
  Don't repeat tokens or base styles from `napkin.css`.
- Works at phone width (390px): 16px side gutter, no horizontal scroll, tap targets ≥ 40px.
  In page-only CSS, never use `repeat(<number>, …)`, fixed `width:` over 340px, or
  `white-space: nowrap`. Each one is a sideways-scroll bug on a phone.
- Is self-contained apart from `napkin.css`. Scripts only from cdnjs.cloudflare.com /
  cdn.jsdelivr.net/npm / unpkg.com with exact versions. Draw with inline SVG; no external images.
- Wraps every `localStorage` read and write in `try/catch`, so the page still renders without storage.
  Ticks and guesses are saved per browser only, under a key starting with `"napkin:" + <title>`.

## Shell

The shell template is in `references/shell-template.md`. Load it only for a new topic or a v1
upgrade. On later pages, only append one line to `PAGES` in the existing `index.html`.
