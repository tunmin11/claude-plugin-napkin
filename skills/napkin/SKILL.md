---
name: napkin
description: >
  Explain it on a napkin. Turns a topic, link, document or folder of files into a visual,
  hands-on learning page (a sketch with a metaphor from the user's own world, a learning path,
  a tick-off tutorial, a comparison and more), with fresh facts and sources. Keeps one
  artifact per topic and stacks new pages inside it. Use when the user asks to learn a topic
  in a visual or hands-on way ("napkin this", "draw/sketch/visualize this for me", "make me a
  page to learn X", "make this easier to read"), asks what's worth learning in a doc or folder,
  or shares a long doc or link and is clearly stuck reading it. Not for quick factual answers,
  debugging, or questions about code the user is working on.
---

# napkin

Help someone learn something without reading a wall of text. Ask a little, check the facts, then
draw it on a napkin: one visual page with something to **do** on it.

Keep it quick and light. The person came to learn, not to fill in a form.

## 1. Intake

Work out what they brought:

- **A topic in a few words.** Go to step 2.
- **A link.** Fetch and read it, then go to step 2.
- **A long document, or a folder of files.** Skim it first, then suggest **3–4 angles** worth learning,
  and put the quick questions from step 2 **in the same message**, so it's one round, not two.
  Good angles point at something specific: "these two docs disagree about X", "the core idea
  behind all of this is Y", "Z is explained here three different ways". Let them pick one or name
  their own. In a big folder, read up to ~15 text files (skip `node_modules`, `.git` and other
  build or dependency folders) and list the rest by name. Skip anything you can't read and say so
  in one line. Don't let it stop you.
- **Coming back to a topic** ("more on mortgages", "go deeper"). Find the existing napkin first
  (see `references/page-shell.md` → Publishing → *Coming back in a new conversation*). Add a page; don't start a new artifact.

## 2. Quick questions: at most 3, in one message

Ask only what the prompt didn't already answer. If it answered everything, ask nothing and say
"Got it, drawing it up."

The three that matter:
1. **What do you already know about it?** This sets the tags and the starting point.
2. **What's it for?** An exam, a decision, a hobby, just curious. This sets the shape and the depth.
3. **Anything from your life I can use for a comparison?** Ask this only when a metaphor sketch is
   likely and you know nothing about them.

Write them casually and number them so they can answer in one line ("1. nothing 2. buying a house 3. I cook a lot").
Use the user's language for everything: questions, page and closing line.

## 3. Check the facts

- **The user's files are the main source** when they gave any. Don't contradict them silently; if
  the web disagrees with their files, show both.
- **Search the web** for anything that changes over time (prices, rules, versions, research,
  "current" anything), and for key claims you'd otherwise state from memory. Prefer primary or
  official sources.
- Keep the sources. Every page lists them with a "Facts checked on <today's date>" line.
- **If search isn't available or fails,** build anyway, but put "Not web-checked: built from
  your files / general knowledge" in the footer instead, and mention it in your reply.

## 4. Draw it

1. Load the `artifact-design` skill if it's available. Follow its rules for the page.
2. Pick a shape from `references/shapes.md` that fits this topic **for this person**, mix two, or
   invent one. Don't default to the same shape every time.
3. Build the page as its own file and fit it into the topic's artifact using
   `references/page-shell.md`. That file covers the one-artifact-per-topic rule, the shell, the
   publishing steps, and the local-folder fallback.

Every page must have:
- one main picture or structure, with text supporting it and not the other way round
- something to **do**: a click, toggle, tick, slider or reveal
- the sources footer
- phone-width layout with light and dark mode

Before you publish, read the page as the user would. Is there any paragraph longer than ~4
lines that could be a drawing, a list or a toggle instead? Fix it.

## 5. Hand it over

Reply with the link, or the file path for the local fallback. Add one sentence on what the page
shows and, if relevant, one honest line about what it leaves out. Then close with exactly one line:

> Want it deeper, or in a different shape?

Nothing else. No summary of the page, no list of features.

## Tone

Humble and friendly. Playful is fine; hype isn't. No "unlock", "supercharge", "game-changer".
Light humor is welcome when it helps the idea land; skip it when the topic is serious (health, money trouble, grief).
