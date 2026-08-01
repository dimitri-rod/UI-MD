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
| `() Placeholder` | Text input |
| `(Label)` | Tag. `*clickable, toggles active*` on a group makes filters. |
| `[x] Item` / `[ ] Item` | Checked / unchecked. Multi-select unless `*single-select*`. |
| `![alt](image.jpg)` | Image |
| `:icon-name:` | Icon |
| `---` | Divider |
| `// text` | Note for whoever builds this. Never rendered. |
| `$Name,Variant$` | Value from your design system |

**A primitive owns its whole line.** A line made only of primitives is primitives; a line with prose in it is body copy, and any brackets, parens or colons inside it are just characters. So `(Draft)` alone is a tag, `Free forever (for one project)` is a sentence, and `$29/month` is a price rather than a token.

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

Of those three boundaries only the blank line is fragile — some tools strip blank lines when they hand a file back. When a boundary matters, name a container instead of leaning on one.

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

That's the only case where it adds content you didn't write, and the note controls how far it goes. `// six or so` invites invention. `// exactly these four: Nike, Google, Oura, Patagonia` forbids it — use that form for anything named, like clients, logos or people, where a plausible invention is a false claim.

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
- The file is updated after, in the modifier that owns the node. Never in a `// note`; notes don't render, so a rule left in one won't survive the next build.

---

## What goes inside a rule

Plain description. If you don't know the real word, say it out loud instead — both sides work:

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

Start on the left, move right when it feels natural. Mix them freely — often in the same rule.

## The example

[A full landing page](assets/UI-MD_landingpage-example.md), written both ways at once:

```
>> Pro Card
*background: $Color,Surface$, border: 2px solid $Color,Accent 1$, padding: 40px*
>>> ### Pro
>>> $29/month, unlimited projects.
>>> [[Get Started]](signup)
*width: 100%, background: $Color,Accent 1$, loud and proud — this is the one*
```

---

## Limits

- Rename something and the old name stops resolving.
- Hand-edit the code and this file becomes fiction. A round-trip extractor would fix that. Not built.
- Untested against its null hypothesis: the same screen in prose, in UI-MD, and as an outline the model writes itself. Ten edits each. Count first-try hits.

Why it's shaped this way: [RATIONALE.md](RATIONALE.md).

No IDs, no schema, no parser, no validator. If a shape doesn't make something shorter or clearer, it isn't here.
