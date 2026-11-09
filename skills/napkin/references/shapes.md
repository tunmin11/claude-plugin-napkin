# Shapes

This is a menu, not a rulebook. Pick the shape that fits **this topic for this person**, mix two, or
invent a new one when none of these fit. Don't reach for the same shape every time.

Every shape needs three things: one main picture or structure, something to **do**, and the sources footer.
Text supports the picture, not the other way round. If a section is more than ~4 short lines, it
probably wants to be a drawing, a list or a toggle.

---

## Metaphor sketch
**Use when:** the idea is abstract or invisible, like how something works inside, or why a rule exists.
**Must have:**
- A metaphor taken **from the user's world**: a hobby, job or daily life they mentioned. If you know
  nothing about them, pick something nearly everyone touches (a kitchen, a bus route, a group chat),
  but never a stock one you'd give anyone.
- A drawing that maps each real part to its metaphor part, labelled both ways ("the yeast = …").
- One line saying **where the metaphor breaks**. Every metaphor does, and saying so builds trust.

**Interaction idea:** a "what if" toggle that removes or changes one part and shows what happens in the picture.

## Learning path
**Use when:** the topic is big and the person needs to know where to start and what's next.
**Must have:**
- 4–8 steps, each tagged by how new it is **to this reader**: `you already know this` / `small step` / `new ground`.
- The tags come from the quick questions, not guesses about "people in general".
- A one-line "why this step matters" for each.

**Interaction idea:** tick a step to mark it done, so the path fills in. Store this in `localStorage` with try/catch.

## Hands-on tutorial
**Use when:** they want to *do* something (bake it, set it up, fill it in), not just understand it.
**Must have:**
- Small, tickable steps with visible progress, like a bar, a filling picture or a level-up.
- An "If it goes wrong" box with the 2–3 most common mistakes and their fixes.
- The end state described so they know when they're done.

**Interaction idea:** each tick lights up part of a drawing (a cake rising, a map filling in).

## Side-by-side
**Use when:** the question is "X vs Y", or the user's documents disagree.
**Must have:**
- The same few rows for both sides, in plain words.
- A "where they actually disagree" row, plus "it depends on…" when there's no clear winner.
- For disagreeing docs: quote each source briefly and link it.

**Interaction idea:** "my situation" chips (e.g. *small budget*, *lots of time*) that highlight which side fits.

## Timeline / map
**Use when:** order matters (history, a process) or the question is "how do the parts connect".
**Must have:**
- One drawing of the whole thing first, then the details.
- 5–10 nodes at most on screen at once. Group the rest.

**Interaction idea:** tap a node to open its short card; a "you are here" marker if the person is mid-process.

## Self-check
**Use when:** almost always, as a small add-on at the end of another shape. Rarely on its own.
**Must have:**
- 3–5 questions that test understanding, not memory ("what happens if…", not "what's the name of…").
- Instant, kind feedback that explains *why*, and points back to the part of the page that answers it.

**Interaction idea:** tap an answer → reveal. No scores, no timers.

---

## Sketch style

- Draw with inline SVG. A hand-drawn feel helps it read as "napkin", not "slide deck":
  - wobbly strokes via an SVG `feTurbulence` + `feDisplacementMap` filter (small scale, ~1.5), or
  - a hand font from Google Fonts for labels (e.g. *Caveat*, *Patrick Hand*), with the body text in a readable sans.
- A warm paper background, one accent color, and soft ink. Use the shell's tokens so pages match.
- Labels go *on* the drawing, not in a legend far away.
- Keep the SVG responsive: use `viewBox` and `width:100%`, and check that it's still readable at phone width.
