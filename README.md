# napkin

**Explain it to me on a napkin.**

A Claude skill for learning things without reading walls of text. You bring a topic, a link, a
document or a folder. napkin asks a couple of quick questions, checks the facts on the web, and
draws it as one visual page you can click around in.

- **It draws, not just writes.** It can be a sketch with a metaphor taken from *your* life, a learning
  path, a tick-off tutorial, a side-by-side comparison, or a map. It picks whatever fits the topic.
- **Every page has something to do:** tick a step, drag a slider, flip a toggle, check yourself.
- **It shows where facts come from.** Each page lists its sources and the date they were checked.
- **One napkin per topic.** Ask to "go deeper" and a new page is added next to the old ones, so you
  can flip back through how you learned it.

## Install

**Claude Code**

```
/plugin marketplace add tunmin11/claude-plugin-napkin
/plugin install napkin@napkin
```

**claude.ai**: download this repo, zip the `skills/napkin` folder, and upload it under
**Settings → Capabilities → Skills**.

## Try it

Call it by name with `/napkin:napkin`, or just ask for something visual:

```
/napkin:napkin how does compound interest work?
```
```
napkin this for me: <paste a link or a long article>
```
```
There's a folder of notes in ./sleep-notes. What's worth learning in there?
```

With a document or folder, napkin skims it first and suggests a few angles, like "these two notes
disagree about how much sleep you need." You pick one.

It asks at most three quick questions (what you already know, what it's for, and something from
your life to compare it to). If your prompt already answers them, it skips straight to drawing.

## Where the page ends up

- **On claude.ai, or in Claude Code with artifacts:** a private web page. Nobody else can see it until you share it.
- **Otherwise:** a folder on your computer at `./learn/<topic>/`. Open `index.html` in a browser.

## Honest limits

- It can still get things wrong. The sources are on the page, so check the ones that matter,
  especially for money, health or legal topics.
- A plain question like "what is X?" usually gets a plain answer. Ask for a napkin (or a page,
  or something visual) when you want one.
- Some metaphors won't click for you. Say "different shape" and it'll try another.

## License

MIT
