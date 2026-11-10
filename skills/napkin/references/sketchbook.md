# Sketchbook: the napkin look

Every napkin page looks like a page torn from a sketchbook: graph paper, handwriting, sticky
notes, tape, wobbly hand-drawn lines. The drawing does the explaining; text only labels it.

## napkin.css

The shared stylesheet lives in `references/napkin-css.md`. Pages link it with
`<link rel="stylesheet" href="../napkin.css">` and add only page-specific CSS. Class names you can
use: `.wrap .kicker .idea .sketch .ink .fill .hot .hand-arrow .note .tape .pin .guess .reveal
.ticks .grid .row footer.sources`; tokens: `--paper --grid --ink --muted --accent --note --card
--good --hand --body --mono`.

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
