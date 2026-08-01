# UI-MD

Designing with LLMs is annoying.

Prose has no structure and nothing persists, so every message starts from zero. A screen comes back 70% right, and fixing it costs a paragraph saying *which* before four words saying *what*.

UI-MD is a handful of characters you already know from Markdown. Structure on turn one, a name to point at on every turn after. This page is the whole language — hand it to a model and start writing. If you find yourself inventing a symbol that isn't here, don't. Write plain text and a `*rule*` instead.

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

**Nouns are syntax. Adjectives are prose. Verbs are chat.** Nouns are **primitives** — what exists on screen. Adjectives are **modifiers** — how it looks, in plain words. Verbs are never written down; you say them once, in chat.

---

## Primitives

| | |
|---|---|
| `> Name` | Container. Each extra `>` goes one level deeper. No depth limit. |
| `# H1` `## H2` `### H3` | Heading |
| any bare line | Body copy — paragraph, subtitle or caption, decided by position |
| `[Link](url)` | Text link. No `https://` means a page elsewhere in the same product; a full URL is external. |
| `[[Button]]` | Button |
| `[[Button]](url)` | Button that navigates |
| `<> Placeholder` | Text input, placeholder is the text |
| `<Label>` | Tag or pill. Add `*clickable, toggles active*` to a group to make filters. |
| `[x] Item` / `[ ] Item` | Checked / unchecked. A group is multi-select; `*single-select*` makes it radio. |
| `![alt](image.jpg)` | Image |
| `:icon-name:` | Icon |
| `---` | Divider, on its own line |

Container names are yours to pick — section, card, banner, accordion, drawer. A two-column layout is just two named containers at the same depth.

**Names must be unique in the file.** Not `Card` three times — `Developer Card`, `Pro Card`, `Enterprise Card`. The name is the address, so it carries through into the emitted code as a class, component name or comment. That's what makes it findable later.

## Modifiers

`*...*` attaches to the run of lines directly above it. Never anything below.

```
>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
*ghost, 14px*

>> [[Get Started]](signup)
*background $Color,Accent 1$, rounded 8px, glow on hover*
```

Three links, one rule. The run ends at a blank line, another modifier, or a shallower container — so styling a group needs no group syntax. On a container, a modifier is inherited by everything nested under it.

### Local and global

`*Single asterisks*` are local. `**Double asterisks**` are global — the whole file, every screen in it, wherever the line appears.

```
**$Color,Accent 1$ #6366F1, $Color,Accent 2$ #EC4899**
**base font Inter, spacing unit 8px, rounded 12px**
```

Local beats global, later beats earlier, children inherit.

The two marks differ by one character and both render as emphasis, so a mistyped local rule silently goes page-wide. The model lists every global rule it applied after building, so you can catch it. `***Three asterisks***` is undefined — treated as global and reported as a probable typo.

### Tokens

`$Name,Variant$` is an exact value from your design system — `$Color,Accent 1$`, `$Border Width,200$`. Define them in a global line, or leave them undefined and connect a design system later.

A token is a binding, not a value. It stays a token even when nothing defines it yet — that's the point of writing one. If an edit ever replaces one with a literal, the model says so, because otherwise that node quietly leaves the design system and nothing downstream notices.

### Notes

`// text` is context for whoever builds this next — a caveat, a reason, a TODO. Never rendered.

```
>> [ ] Annual, save 20%
*single-select*
// switching to Annual updates all three card prices
```

## Building

Read the global lines first, then build the tree in order — depth is layout nesting. Fill unspecified detail with defaults consistent with the globals, but don't invent content, copy or sections that weren't written.

## Changing

```
Pro Card: thicker border, make it feel premium
Hero Title: shorter, punchier
FAQ Search: move it above the chips
Enterprise Card: remove it

Pro Card on hover: soft glow
Pricing Section on mobile: stack the cards
```

The name comes off the file. You're not describing the element — you're reading its label.

- Change only that node. Don't restructure or improve what's around it.
- `on hover`, `on mobile`, `when empty` scope the change to that state. The base case stays as it was.
- A name that isn't in the file has no address. The model says so rather than creating it.
- Afterwards the file is updated to match, in the modifier that owns the node — never as a `// note`, since notes don't render and a rule left in one won't survive the next build.

---

## What goes inside a rule

The shapes above are the strict part. What goes *inside* a `*rule*` is just plain description — you don't need real CSS syntax, but the vocabulary helps you say what you mean instead of hoping the model guesses.

- **Spacing:** padding, margin, gap
- **Layout:** align, center, stack, flex-row / flex-col, width, overflow
- **Look:** background, color, border, rounded, shadow, opacity
- **Text:** font, weight, uppercase, text size
- **Motion:** on hover / on click / on load, transform, translate, rotate, animate, duration, infinite

And if you don't know the "real" word, don't stop to look it up — say it like you would out loud. Both sides work the same:

| What you'd naturally say | The tidier version |
|---|---|
| `*make it bigger*` | `*padding 24px, text 20px*` |
| `*push it over to the right*` | `*align right*` |
| `*keep it in the middle*` | `*align center*` |
| `*give them some breathing room*` | `*gap 16px*` |
| `*round the corners a bit*` | `*rounded 12px*` |
| `*make it red*` | `*background $Color,Accent 2$*` |
| `*make the text lighter, kind of faded*` | `*opacity 70%*` |
| `*when someone clicks it, save the form*` | `*on click: save*` |
| `*make it lift up a little when you hover over it*` | `*on hover: translate Y -4px*` |
| `*fade it in when the page loads*` | `*on load: animate opacity, 1s*` |

The model translates it, not you. The tidier version is just faster to type once it's second nature. Start on the left and move right whenever it feels natural, not before.

## The same page, two ways

The [full landing page example](assets/UI-MD_landingpage-example.md), written precisely:

```
>> Pro Card
*background: $Color,Surface$, border: 2px solid $Color,Accent 1$, border-radius: 16px, padding: 40px*
>>> ### Pro
>>> [[Get Started]](signup)
*width: 100%, background: $Color,Accent 1$*
```

And the [same page written casually](assets/UI-MD_landingpage-example-casual.md):

```
>> Pro Card
*the golden child — make everyone want to be here*
>>> ### Pro
>>> [[Get Started]](signup)
*loud and proud, this is the one*
```

Same shapes, same result. The tidy version is optional, not required.

---

## Using it

Give a model this page, write your screen, then change things by name.

| | |
|---|---|
| [`assets/UI-MD_landingpage-example.md`](assets/UI-MD_landingpage-example.md) | A full landing page, written precisely. |
| [`assets/UI-MD_landingpage-example-casual.md`](assets/UI-MD_landingpage-example-casual.md) | The same page, written as feelings. |
| [`RATIONALE.md`](RATIONALE.md) | Why it's shaped this way. |

## Limits

- Rename something and the old name stops resolving.
- Hand-edit the code and this file becomes fiction. A round-trip extractor would fix that. Not built.
- No way to say "six FAQ questions go here." Ask for a section with repeating content and the model invents it.
- Untested against its null hypothesis: the same screen in prose, in UI-MD, and as a numbered outline the model emits itself. Ten edits each. Count first-try hits.

No IDs, no schema, no parser, no validator. If a shape doesn't make something shorter or clearer, it isn't here.
