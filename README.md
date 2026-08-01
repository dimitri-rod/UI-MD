# UI-MD

Prose has no structure and nothing persists. Every message starts from zero.

So a screen comes back 70% right, and fixing it costs a paragraph saying *which* before four words saying *what*.

UI-MD is a handful of characters you already know from Markdown. Structure on turn one, a name to point at on every turn after.

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

Inside the asterisks is the only place prose lives. `*make it bigger*` and `*padding 24px, text 20px*` both work.

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

## Files

| | |
|---|---|
| [`assets/UI-MD_skill.md`](assets/UI-MD_skill.md) | The full rules. Give this to the model. |
| [`RATIONALE.md`](RATIONALE.md) | Why it's shaped this way. |
| [`assets/UI-MD_landingpage-example.md`](assets/UI-MD_landingpage-example.md) | A landing page, written precisely. |
| [`assets/UI-MD_landingpage-example-casual.md`](assets/UI-MD_landingpage-example-casual.md) | The same page, written as feelings. |

---

## Limits

- Rename something and the old name stops resolving.
- Hand-edit the code and this file becomes fiction. A round-trip extractor would fix that. Not built.
- Untested against its null hypothesis: the same screen in prose, in UI-MD, and as a numbered outline the model emits itself. Ten edits each. Count first-try hits.

No IDs, no schema, no parser, no validator. If a shape doesn't make something shorter or clearer, it isn't here.
