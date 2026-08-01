# UI-MD

Designing with LLMs is annoying. Prose has no structure and nothing persists, so every message starts from zero — a screen comes back 70% right, and fixing it costs a paragraph saying *which* before four words saying *what*.

UI-MD is a handful of characters you already know from Markdown. Structure on turn one, a name to point at on every turn after. This page is the whole language. If you're inventing a symbol that isn't here, don't — write plain text and a `*rule*`.

```
> Pricing Section
>> Pro Card
>>> ## Pro
>>> $29/month, unlimited projects.
>>> [[Get Started]](signup)
*bordered, slightly larger than the others*
```

Then, later:

```
Pro Card: thicker border, glow on hover
```

**Nouns are syntax. Adjectives are prose. Verbs are chat.** Primitives are what exists, modifiers are how it looks, and verbs are never written down — you say them once, in chat.

---

## Primitives

| | |
|---|---|
| `> Name` | Container. Each extra `>` goes one level deeper. No depth limit. |
| `# H1` `## H2` `### H3` | Heading |
| any bare line | Body copy — paragraph, subtitle or caption, by position |
| `[Link](url)` | Text link. No `https://` means a page in the same product. |
| `[[Button]]` | Button |
| `[[Button]](url)` | Button that navigates |
| `<> Placeholder` | Text input |
| `<Label>` | Tag. `*clickable, toggles active*` on a group makes filters. |
| `[x] Item` / `[ ] Item` | Checked / unchecked. Multi-select unless `*single-select*`. |
| `![alt](image.jpg)` | Image |
| `:icon-name:` | Icon |
| `---` | Divider |
| `// text` | Note for whoever builds this. Never rendered. |
| `$Name,Variant$` | Value from your design system |

Container names are yours to pick — section, card, banner, drawer. A two-column layout is two named containers at the same depth.

**Names must be unique in the file.** Not `Card` three times — `Developer Card`, `Pro Card`, `Enterprise Card`. The name is the address, and it carries into the emitted code so it's findable later.

## Modifiers

`*...*` attaches to the run of lines above it. Never below.

```
>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
*ghost, 14px*

>> [[Get Started]](signup)
*background $Color,Accent 1$, rounded 8px, glow on hover*
```

The run ends at a blank line, another modifier, or a shallower container. Containers pass it down. That's why there's no group syntax.

`**Double asterisks**` are global — the whole file, wherever they appear.

```
**$Color,Accent 1$ #6366F1, $Color,Accent 2$ #EC4899**
**base font Inter, spacing unit 8px, rounded 12px**
```

Local beats global, later beats earlier, children inherit.

One character separates the two, and both render as emphasis — so the model lists every global rule it applied. `***Three***` is undefined: treated as global, reported as a probable typo.

A `$Token$` is a binding, not a value. It stays one even when nothing defines it yet. If an edit replaces one with a literal, the model says so.

## Building

Globals first, then the tree in order. Fill in unspecified detail; don't invent content or sections that weren't written.

**One written item is a pattern.** Where content repeats — FAQ entries, table rows, cards in a feed — write one and the model fills the rest:

```
>> Can I switch between monthly and annual billing?
*accordion, one open at a time*
// six or so, spanning billing, setup and API
```

That's the only case where it adds content you didn't write.

## Changing

```
Pro Card: thicker border, make it feel premium
FAQ Search: move it above the chips
Enterprise Card: remove it

Pro Card on hover: soft glow
Pricing Section on mobile: stack the cards
```

The name comes off the file. You're reading its label, not describing it.

- Only that node changes.
- `on hover`, `on mobile`, `when empty` leave the base case alone.
- A name that isn't in the file has no address — the model says so instead of creating it.
- The file is updated after, in the modifier that owns the node. Never in a `// note`; notes don't render, so a rule left in one won't survive the next build.

---

## What goes inside a rule

Plain description. You don't need CSS syntax, but the vocabulary helps you say what you mean.

- **Spacing:** padding, margin, gap
- **Layout:** align, center, stack, flex-row / flex-col, width, overflow
- **Look:** background, color, border, rounded, shadow, opacity
- **Text:** font, weight, uppercase, text size
- **Motion:** on hover / on click / on load, transform, translate, animate, duration

And if you don't know the real word, say it out loud instead. Both sides work:

| | |
|---|---|
| `*make it bigger*` | `*padding 24px, text 20px*` |
| `*push it over to the right*` | `*align right*` |
| `*keep it in the middle*` | `*align center*` |
| `*give them some breathing room*` | `*gap 16px*` |
| `*round the corners a bit*` | `*rounded 12px*` |
| `*make the text lighter, kind of faded*` | `*opacity 70%*` |
| `*when someone clicks it, save the form*` | `*on click: save*` |
| `*make it lift a little on hover*` | `*on hover: translate Y -4px*` |
| `*fade it in when the page loads*` | `*on load: animate opacity, 1s*` |

Start on the left, move right when it feels natural. The model translates, not you.

## The same page, two ways

[Precisely](assets/UI-MD_landingpage-example.md):

```
>> Pro Card
*background: $Color,Surface$, border: 2px solid $Color,Accent 1$, padding: 40px*
>>> ### Pro
>>> [[Get Started]](signup)
*width: 100%, background: $Color,Accent 1$*
```

[Casually](assets/UI-MD_landingpage-example-casual.md):

```
>> Pro Card
*the golden child — make everyone want to be here*
>>> ### Pro
>>> [[Get Started]](signup)
*loud and proud, this is the one*
```

Same shapes, same result.

---

## Limits

- Rename something and the old name stops resolving.
- Hand-edit the code and this file becomes fiction. A round-trip extractor would fix that. Not built.
- Untested against its null hypothesis: the same screen in prose, in UI-MD, and as an outline the model writes itself. Ten edits each. Count first-try hits.

Why it's shaped this way: [RATIONALE.md](RATIONALE.md).

No IDs, no schema, no parser, no validator. If a shape doesn't make something shorter or clearer, it isn't here.
