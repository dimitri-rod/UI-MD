# UI-MD

Designing with LLMs is annoying.

Prose has no structure and nothing persists, so every message starts from zero. A screen comes back 70% right, and fixing it costs a paragraph saying *which* before four words saying *what*.

UI-MD is a handful of characters you already know from Markdown. Structure on turn one, a name to point at on every turn after. That's it — the whole dictionary is below, and if you find yourself inventing a symbol that isn't in it, don't. Write plain text and a `*rule*` instead.

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

---

## The principle

**Nouns are syntax. Adjectives are prose. Verbs are chat.**

Nouns are **primitives** — what exists on screen. Adjectives are **modifiers** — how it looks, in plain words. Verbs are never written down; you say them once, in chat.

---

## Primitives

| | |
|---|---|
| `> Name` | Container |
| `# H1` `## H2` `### H3` | Heading |
| any bare line | Body copy |
| `[Link](url)` | Text link |
| `[[Button]]` | Button |
| `[[Button]](url)` | Button that navigates |
| `<> Placeholder` | Text input |
| `<Label>` | Tag or pill |
| `[x]` / `[ ]` | Checked / unchecked |
| `![alt](image.jpg)` | Image |
| `:icon-name:` | Icon |
| `---` | Divider |
| `// note` | Context for the model, never rendered |
| `$Name,Variant$` | Exact value from your design system |

`>` is a container. Each extra `>` goes one level deeper. No depth limit.

Container names are yours to pick — section, card, banner, accordion, drawer, whatever you're describing. A two-column layout is just two named containers at the same depth:

```
> Hero
>> Left Container
>>> # Hero title
>> Right Container
>>> ![Hero illustration](hero_illustration.jpg)
```

**Names must be unique in the file.** Not `Card` three times — `Developer Card`, `Pro Card`, `Enterprise Card`. The name is the address.

## Modifiers

`*...*` attaches to the run of lines directly above it.

```
>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
*ghost, 14px*

>> [[Get Started]](signup)
*background $Color,Accent 1$, rounded 8px, glow on hover*
```

Three links, one rule. The run ends at a blank line, another modifier, or a shallower container — so styling a group needs no group syntax.

On a container, a modifier is inherited by everything nested under it.

`**Double asterisks**` apply to the whole file — every screen in it:

```
**base font Inter, spacing unit 8px, rounded 12px**
**$Color,Accent 1$ #6366F1**
```

Local beats global, later beats earlier, children inherit.

---

## What goes inside a rule

The shapes above are the only part that's really "UI-MD." What goes *inside* a `*rule*` is just plain description. You don't need real CSS syntax, but knowing the vocabulary helps you say what you mean instead of hoping the model guesses right.

The words that come up constantly:

- **Spacing:** padding, margin, gap
- **Layout:** align, center, stack, flex-row / flex-col, width, overflow
- **Look:** background, color, border, rounded, shadow, opacity
- **Text:** font, weight, uppercase, text size
- **Motion:** on hover / on click / on load, transform, translate, rotate, animate, duration, infinite

### Or just say it however you'd normally say it

If you don't know the "real" word, don't stop to look it up — say it like you would out loud. Both sides work the same:

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

Same result either way — the model translates it, not you. The tidier version is just faster to type once it's second nature. Start on the left and move right whenever it feels natural, not before.

The shapes are the strict part of the language. The rules are closer to talking than to coding.

---

## The same page, two ways

Here's the pricing section from the [full landing page example](assets/UI-MD_landingpage-example.md), written precisely — real values, nothing left to guess:

```
> Pricing Section
*align-center, flex-col, padding: 100px 5%*
>> ## Simple, transparent pricing.
*font-size: 40px, font-weight: 700, text-align: center*

>> Pro Card
*background: $Color,Surface$, border: 2px solid $Color,Accent 1$, border-radius: 16px, padding: 40px, transform: scale(1.05)*
>>> ### Pro
>>> $29/month, unlimited projects.
*opacity: 70%, margin: 12px 0*
>>> [[Get Started]](signup)
*width: 100%, background: $Color,Accent 1$, border-radius: 8px*
```

And the [same page written casually](assets/UI-MD_landingpage-example-casual.md) — same shapes, same structure, every rule swapped for a feeling:

```
> Pricing Section
*calm, spacious, no rush*
>> ## Simple, transparent pricing.
*confident and clear, no games*

>> Pro Card
*the golden child — make everyone want to be here*
>>> ### Pro
>>> $29/month, unlimited projects.
>>> [[Get Started]](signup)
*loud and proud, this is the one*
```

Same layout, same result. The tidy version is optional, not required.

---

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

---

## Using it

1. Give a model [`assets/UI-MD_skill.md`](assets/UI-MD_skill.md) as its instructions.
2. Write your screen in UI-MD.
3. To change something later, name it and say what should happen.

| | |
|---|---|
| [`assets/UI-MD_skill.md`](assets/UI-MD_skill.md) | The full rules. Give this to the model. |
| [`assets/UI-MD_landingpage-example.md`](assets/UI-MD_landingpage-example.md) | A full landing page, written precisely. |
| [`assets/UI-MD_landingpage-example-casual.md`](assets/UI-MD_landingpage-example-casual.md) | The same page, written as feelings. |
| [`RATIONALE.md`](RATIONALE.md) | Why it's shaped this way. |

---

## Limits

- Rename something and the old name stops resolving.
- Hand-edit the code and this file becomes fiction. A round-trip extractor would fix that. Not built.
- Untested against its null hypothesis: the same screen in prose, in UI-MD, and as a numbered outline the model emits itself. Ten edits each. Count first-try hits.

No IDs, no schema, no parser, no validator. If a shape doesn't make something shorter or clearer, it isn't here.
