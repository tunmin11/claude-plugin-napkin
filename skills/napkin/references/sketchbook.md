# Sketchbook: the napkin look

Every napkin page looks like a page torn from a sketchbook: graph paper, handwriting, sticky
notes, tape, wobbly hand-drawn lines. The drawing does the explaining; text only labels it.

## napkin.css

Write this block, unchanged, to `napkin.css` at the artifact root **once**, when a topic is first
created (or when an old topic gets its first v2 page). Never regenerate it for later pages.
Pages link it with `<link rel="stylesheet" href="../napkin.css">` and add only page-specific CSS.

```css
@import url("https://fonts.googleapis.com/css2?family=Caveat:wght@500;700&family=Atkinson+Hyperlegible:ital,wght@0,400;0,700;1,400&family=JetBrains+Mono:wght@400;600&display=swap");
:root {
  --paper:#f7f5ee; --grid:#e6e2d6; --ink:#22262c; --muted:#5f6670; --accent:#d4572f;
  --note:#ffe27a; --note-ink:#3a3320; --card:#ffffff; --good:#2f8452;
  --hand:"Caveat","Bradley Hand","Comic Sans MS",cursive;
  --body:"Atkinson Hyperlegible","Segoe UI",system-ui,sans-serif;
  --mono:"JetBrains Mono",ui-monospace,Menlo,monospace;
  color-scheme: light;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --paper:#171a1f; --grid:#232831; --ink:#e8e6e0; --muted:#a2a7ae; --accent:#f07a52;
    --note:#d9b94a; --note-ink:#211c0c; --card:#1f242b; --good:#6cd197; color-scheme: dark;
  }
}
:root[data-theme="dark"] {
  --paper:#171a1f; --grid:#232831; --ink:#e8e6e0; --muted:#a2a7ae; --accent:#f07a52;
  --note:#d9b94a; --note-ink:#211c0c; --card:#1f242b; --good:#6cd197; color-scheme: dark;
}

/* phone guardrails */
*, *::before, *::after { box-sizing: border-box; }
svg, img, canvas, table { max-width: 100%; }
html, body { margin: 0; }
body {
  background-color: var(--paper);
  background-image: linear-gradient(var(--grid) 1px, transparent 1px), linear-gradient(90deg, var(--grid) 1px, transparent 1px);
  background-size: 24px 24px;
  color: var(--ink); font: 16.5px/1.6 var(--body); overflow-wrap: anywhere;
}
.wrap { max-width: 920px; margin: 0 auto; padding: 36px 16px 64px; display: grid; gap: 48px; }
.grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(140px, 1fr)); gap: 12px; }
.row { display: flex; flex-wrap: wrap; gap: 8px; } .row > * { min-width: 0; }
a { color: var(--accent); }
code { font-family: var(--mono); font-size: .9em; background: var(--card); padding: 1px 5px; border-radius: 4px; }

/* headings and the one-line idea */
.kicker { font-family: var(--hand); font-size: 22px; color: var(--accent); line-height: 1; transform: rotate(-1.5deg); transform-origin: left; display: inline-block; }
h1, h2, h3 { font-family: var(--hand); font-weight: 700; line-height: 1; margin: 0; }
h1 { font-size: clamp(42px, 8vw, 68px); }
h2 { font-size: clamp(30px, 5vw, 40px); }
.idea { font-size: 19px; max-width: 34em; margin: 8px 0 0; }
.idea b { background: linear-gradient(transparent 60%, var(--note) 60%); color: inherit; }

/* the sketch */
.sketch { position: relative; }
.sketch svg { width: 100%; height: auto; display: block; overflow: visible; }
.sketch svg text, .label { font-family: var(--hand); font-size: 20px; fill: var(--ink); color: var(--ink); }
.sketch .ink { stroke: var(--ink); fill: none; stroke-width: 2.2; stroke-linecap: round; stroke-linejoin: round; }
.sketch .fill { fill: var(--card); }
.sketch .hot { stroke: var(--accent); fill: var(--accent); }
.hand-arrow { stroke: var(--accent); fill: none; stroke-width: 2.2; stroke-linecap: round; marker-end: url(#arrowhead); }

/* sticky note + tape */
.note { position: relative; background: var(--note); color: var(--note-ink); font-family: var(--hand); font-size: 21px; line-height: 1.2;
        padding: 16px 14px 12px; max-width: 280px; transform: rotate(1.5deg); box-shadow: 2px 4px 0 rgba(0,0,0,.12); }
.note:nth-of-type(even) { transform: rotate(-1.8deg); }
.tape { position: absolute; top: -9px; left: 30%; width: 64px; height: 18px; background: color-mix(in srgb, var(--accent) 35%, transparent); transform: rotate(-4deg); }

/* source pin: <details class="pin"> works on tap and click, no script */
.pin { display: inline-block; position: relative; vertical-align: super; font-size: 12px; }
.pin > summary { list-style: none; cursor: pointer; min-width: 22px; min-height: 22px; padding: 0 6px; border-radius: 999px;
                 background: var(--accent); color: var(--paper); font: 700 12px/22px var(--body); text-align: center; }
.pin > summary::-webkit-details-marker { display: none; }
.pin[data-kind="general"] > summary { background: var(--muted); }
.pin > div { position: absolute; z-index: 5; left: 0; top: 28px; width: min(280px, 80vw); background: var(--card); color: var(--ink);
             border: 1.5px solid var(--ink); border-radius: 6px; padding: 10px 12px; font: 14px/1.4 var(--body); box-shadow: 3px 3px 0 var(--grid); }
.pin > div q { font-style: italic; display: block; margin-bottom: 4px; }
.pin > div small { color: var(--muted); }
@media (max-width: 560px) { .pin > div { position: fixed; left: 16px; right: 16px; top: auto; bottom: 16px; width: auto; } }

/* guess first, then reveal */
.guess { background: var(--card); border: 1.5px dashed var(--ink); border-radius: 8px; padding: 14px 16px; display: grid; gap: 10px; }
.guess p { margin: 0; font-weight: 700; }
.guess button { min-height: 40px; padding: 6px 14px; border: 1.5px solid var(--ink); border-radius: 999px; background: var(--paper);
                color: var(--ink); font: 600 15px var(--body); cursor: pointer; }
.guess button[aria-pressed="true"] { border-color: var(--accent); color: var(--accent); }
.reveal { display: none; font-family: var(--hand); font-size: 21px; line-height: 1.25; }
.guess.answered .reveal { display: block; }

/* tick list */
.ticks { list-style: none; padding: 0; margin: 0; display: grid; gap: 10px; }
.ticks label { display: flex; gap: 10px; align-items: flex-start; min-height: 40px; cursor: pointer; }
.ticks input { width: 22px; height: 22px; accent-color: var(--good); flex: none; margin-top: 3px; }
.ticks input:checked + span { text-decoration: line-through; text-decoration-color: var(--accent); color: var(--muted); }

/* sources footer */
footer.sources { border-top: 1.5px dashed var(--grid); padding-top: 16px; font-size: 14px; color: var(--muted); }
footer.sources p { font-family: var(--hand); font-size: 20px; color: var(--ink); margin: 0 0 6px; }
footer.sources ol { margin: 0; padding-left: 20px; }

@media (prefers-reduced-motion: no-preference) { .note, .kicker { transition: transform .2s; } .note:hover { transform: rotate(0); } }
```

## Snippets

**Wobble filter + arrowhead.** Paste once per page, inside the first `<svg>` (or a hidden one):
```html
<defs>
  <filter id="wobble"><feTurbulence type="fractalNoise" baseFrequency="0.02" numOctaves="2" seed="3"/>
    <feDisplacementMap in="SourceGraphic" scale="1.5"/></filter>
  <marker id="arrowhead" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse">
    <path d="M0 0 L10 5 L0 10" fill="none" stroke="currentColor" stroke-width="1.5"/></marker>
</defs>
```
Put `filter="url(#wobble)"` on the group of hand-drawn shapes, not on text.

**Source pin.** The number matches the fact (`F3` → `3`). Grey for general knowledge:
```html
<details class="pin"><summary>3</summary><div><q>short quote from the source</q><small>notes/sleep.md · Deep sleep</small></div></details>
<details class="pin" data-kind="general"><summary>?</summary><div>General knowledge, not checked against a source.</div></details>
```
Inside SVG, put the pin in a `<foreignObject>` next to the label it backs, or right after the label in the text.

**Sticky note:**
```html
<aside class="note"><span class="tape"></span>Where it breaks: real snow melts, money usually doesn't.</aside>
```

**Guess first, then reveal:**
```html
<div class="guess"><p>Guess first: after 10 years at 7%, what does $100 become?</p>
  <div class="row"><button>$170</button><button data-right>$197</button><button>$700</button></div>
  <div class="reveal">About $197. The extra $27 is interest earning interest. Look at the biggest snowball in the sketch.</div></div>
<script>
document.querySelectorAll(".guess").forEach(g => g.querySelectorAll("button").forEach(b => b.onclick = () => {
  g.querySelectorAll("button").forEach(x => x.setAttribute("aria-pressed", x === b));
  g.classList.add("answered");
}));
</script>
```
Any guess reveals the answer. The reveal is kind and points back at the sketch. No scores, no timers.

**Sources footer:**
```html
<footer class="sources">
  <p>Facts checked on YYYY-MM-DD</p>   <!-- or: "Not web-checked: built from your files / general knowledge" -->
  <ol><li><a href="…">Source title</a>: what it was used for</li></ol>
</footer>
```

## Sketch first

Before writing a paragraph, ask: can this be drawn? Draw it when the idea is:
- **a flow**: boxes and hand arrows, one verb on each arrow
- **a before/after**: two small sketches side by side, the difference circled in the accent color
- **a part-to-part mapping**: the real thing on one side, the metaphor on the other, dotted lines between, labelled both ways
- **a quantity growing or shrinking**: things that get bigger, stack up, or fill in
- **a place or structure**: a floor plan, a map, a cross-section

Rules:
- Labels go **on** the drawing, in the hand font, never in a legend far away.
- Pins sit next to the label they back.
- `viewBox` + `width:100%`. Check that labels are still readable at 390px wide; if not, use fewer, bigger labels.
- One accent color for "the thing to notice". Everything else is ink.
- Vary the layout between pages: sketch on top, sketch in the middle with notes around it, or two sketches side by side. Don't reuse the last page's layout.
