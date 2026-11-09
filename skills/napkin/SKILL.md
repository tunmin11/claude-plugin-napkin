---
name: napkin
description: >
  Explain it on a napkin. Turns a topic, link, document or folder of files into a visual,
  hands-on learning page (a sketch with a metaphor from the user's own world, a learning path,
  a tick-off tutorial, a comparison and more), with sourced facts pinned on the page. Keeps one
  artifact per topic, remembers what it read, and stacks new pages inside it. Use when the user
  asks to learn a topic in a visual or hands-on way ("napkin this", "draw/sketch/visualize this
  for me", "make me a page to learn X", "make this easier to read"), asks what's worth learning
  in a doc or folder, or shares a long doc or link and is clearly stuck reading it. Not for quick
  factual answers, debugging, or questions about code the user is working on.
---

# napkin

Help someone learn something without reading a wall of text. Ask a little, check the facts, then
draw it on a napkin: one visual page where the sketch does the explaining, with something to **do**.

Keep it quick and light. The person came to learn, not to fill in a form.

## 1. Intake

Work out what they brought:

- **A topic in a few words.** Go to step 2.
- **A link.** Fetch and read it, then go to step 2.
- **A long document, or a folder of files.** Don't read everything. **Map it first:** file names,
  headings, and the first few lines of each file. Skip `node_modules`, `.git`, build and dependency
  folders, and never open credential files (`.env`, `*.pem`, `id_rsa`, anything in `~/.ssh` or
  `~/.aws`, token or key files). Say in one line what you skipped and what you couldn't read.
  From the map, suggest **a default angle** plus 2–3 others, in the same message as the quick
  questions. Good angles point at something specific: "these two docs disagree about X", "the core
  idea behind all of this is Y". If they don't pick, use the default. No extra round.
  Then **deep-read** only the files that matter for the chosen angle, about 4 at most.
- **Coming back to a topic** ("more on mortgages", "go deeper", "redo the picture"). Find the
  existing napkin and read its `notes.md` **first** (`references/page-shell.md` → Publishing →
  *Coming back*). Don't re-ask questions it already answers. Re-read only files that changed or
  that the new angle needs. Add a page; don't start a new artifact.

## 2. Quick questions: at most 3, in one message

Ask only what the prompt (or `notes.md`) didn't already answer. If it answered everything, ask
nothing and say "Got it, drawing it up."

The three that matter:
1. **What do you already know about it?** This sets the tags and the starting point.
2. **What's it for?** An exam, a decision, a hobby, just curious. This sets the shape and the depth.
3. **Anything from your life I can use for a comparison?** Ask this only when a metaphor sketch is
   likely and you know nothing about them.

Write them casually and number them so they can answer in one line ("1. nothing 2. buying a house 3. I cook a lot").
Use the user's language for everything: questions, page and closing line.

## 3. Fact list (before drawing)

Write 5–15 facts the page will rest on. Each one: the claim in plain words, a short quote
(≤ ~25 words), and its source (file + heading, or URL + date read).

- **The user's files are the main source.** If two sources disagree, keep both, mark them
  `disagree`, and show both on the page. Don't let one document quietly win.
- **Web search** only for things that change over time (prices, rules, versions, "current"
  anything), at most ~3 searches. Prefer primary or official sources.
- **Topic only (no files, no link):** up to ~5 searches for the key facts. Anything you didn't
  check goes on the list marked `general knowledge`, with no quote.
- **If search isn't available or fails,** build anyway: put "Not web-checked: built from your
  files / general knowledge" in the footer and mention it in your reply.
- **The page states only facts from this list.** Framing ("think of it like…") is fine; new facts
  aren't. Each fact on the page gets a source pin; `general knowledge` facts get the grey pin.
- Save the list in `notes.md` (format in `references/page-shell.md`).

## 4. Draw it

1. Load the `artifact-design` skill if it's available. Follow its rules for the page.
2. Pick a shape from `references/shapes.md` that fits this topic **for this person**, mix two, or
   invent one. Don't repeat the last page's shape or layout (check `notes.md` → Pages).
3. Load `references/sketchbook.md` and draw **sketch first**: if an idea can be drawn, draw it, and
   let the text label the drawing. On a new topic, write its CSS block to `napkin.css` unchanged.
   On later pages, `napkin.css` already exists: don't load or rewrite it, just link it.
4. Fit the page into the topic's artifact using `references/page-shell.md`: one artifact per
   topic, `notes.md`, publishing, and the local-folder fallback. On a new topic, copy its shell
   template; on later pages, only append to `PAGES`.

Every page has the six required parts from `references/shapes.md`: the idea in one line, the
sketch, something to do, where it breaks, guess first then reveal, and sources.

## 5. Check before publishing

Read the page as the user would:
- Every fact-looking statement matches an entry on the fact list. Compare against the list;
  don't re-read the documents.
- No paragraph longer than ~4 lines that could be a drawing, a list or a toggle.
- All six required parts are there.
- Phone-width rules from `references/page-shell.md` hold.

Fix what fails, then publish.

## Fix one part

When they ask to change one piece ("redo the picture", "simpler step 3", "different metaphor
here"), read `notes.md`, rewrite **only that section** of that one page file, keep the rest of the
file as it is, note the change in `notes.md` → Pages, and republish just that page and `notes.md`.
A whole new angle is a new page, not a fix.

## 6. Hand it over

Reply with the link, or the file path for the local fallback. Add one sentence on what the page
shows and, if relevant, one honest line about what it leaves out. Then close with exactly one line:

> Want it deeper, or in a different shape?

Nothing else. No summary of the page, no list of features.

## Tone

Humble and friendly. Playful is fine; hype isn't. No "unlock", "supercharge", "game-changer".
Light humor is welcome when it helps the idea land; skip it when the topic is serious (health, money trouble, grief).
