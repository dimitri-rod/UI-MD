# UI-MD

Designing with LLMs can be annoying.

Every message written in prose starts from zero. If a screen comes back 70%
right, fixing it costs a paragraph saying *which* before a few words saying
*what*.

UI-MD is a handful of characters you already know from Markdown.

It provides a structure for prompting. Set a unique name for each component and
start building. Titles, buttons, labels, links and rules. Later, just say the
component name and edit without touching anything else.

```
> Pricing
>> Pro Card
*bordered, slightly larger than the others*
>>> ### Pro
>>> $29/month, unlimited projects.
>>> [[Get Started]][signup]
```

Then, later:

```
Pricing >> Pro Card: thicker border, glow on hover
```

Shapes are structure. Rules are prose. Every entity in Markdown has exactly one
meaning here, plus six shapes Markdown didn't have — button, input, tag, note,
token, icon. Models have read more Markdown than anything else, it previews on
GitHub as a legible wireframe, and it's typeable anywhere.

## The dictionary

| IF | THEN |
|:--|:--|
| `> Name` | container. Each extra `>` goes one level deeper. No depth limit. |
| any bare line | body copy — paragraph, subtitle or caption, by position |
| `# H1` … `###### H6` | heading, six levels |
| text under `===` | H1 |
| text under `---` | H2 |
| `---` `***` `___` after a blank line | divider |
| `---` block at the very top | screen settings: route, theme, breakpoints |
| `*rule*` | rule for the element above |
| `**rule**` `***rule***` | rule for the whole screen |
| `_rule_` | breakpoint or state, element above |
| `__rule__` | breakpoint or state, whole screen |
| `*text*` in prose | italic |
| `**text**` in prose | bold |
| `***text***` in prose | bold italic |
| `~~text~~` in prose | struck out — an old price, a dropped feature |
| `` `text` `` | literal. Keep exactly, don't reword. |
| `\` | the next character is literal |
| `&entity;` | the character it names |
| two trailing spaces | line break inside one element |
| `[^1]` + `[^1]: text` | footnote — fine print, legal line |
| `- item` | item in a set — nav links, features, anything that repeats |
| `- item` indented | item in a subset — a dropdown |
| `1. item` | item in an ordered sequence — steps, a wizard |
| set with blank lines between items | the same set, spaced out |
| `[x] Item` / `[ ] Item` | checked / unchecked. As a set, multi-select unless `*single-select*`. |
| `[Link](url)` | text link. `#name` is a container in this file; no `https://` is a page in the same product. |
| `[Link][name]` | link to a defined destination |
| `[name]: /route` at the bottom | define a destination once, use `[name]` anywhere |
| `<https://acme.com>` | external link, URL shown as its own text |
| `![alt](image.jpg)` | image |
| pipe table | grid or comparison — a pricing matrix |
| `:--` `:-:` `--:` | column alignment, left / centre / right |
| ` ``` ` fenced, or 4-space indent | data behind a repeat, or any block that isn't UI-MD |
| `<tag>` | raw markup, passed through untouched |
| `[[Button]]` | button |
| `[[Button]](url)` `[[Button]][name]` | button that navigates |
| `() Placeholder` | text input |
| `(Label)` | tag. `*clickable, toggles active*` makes filters. |
| `// note` | note for whoever builds this. Never becomes UI. |
| `{Name,Variant}` | value from your design system |
| `:icon-name:` | icon |

## Rules

A line that is entirely one shape is that shape. Inside a line of prose,
everything is text. So `*ghost, 14px*` alone on a line is a rule, `*really*`
inside a sentence is italic, `(Draft)` alone is a tag, and
`Free forever (for one project)` is a sentence.

A `>` line is a container if deeper lines follow it, content if they don't.
Container names are yours to pick, and must be unique in the file.

A rule attaches to the element above it, never below — a line, a list, a table
or a container. Containers pass rules down. Rules stack. To rule several things
at once, make them a set.

```
>> - [Pricing][pricing]
   - [FAQ][faq]
*ghost, 14px, gap 24px*
```

Local beats global, later beats earlier, children inherit. A `{Token}` is a
binding, not a value — if an edit replaces one with a literal, say so.

## Pointing

Walk the same path you wrote. `#2` picks the second match when siblings are
identical.

```
Hero >> [[Start Free Trial]]
Pricing >> [[Get Started]] #2
Hero >> [[Start Free Trial]] _on mobile_
```

Only that element changes. Update the file after, in the rule that owns the
element — never in a `// note`, which never becomes UI.

## Building

Globals first, then the tree in order. Fill in unspecified detail; don't invent
content or sections that weren't written.

One written item is a pattern. Where content repeats, write one and fill the
rest. The note controls how far: `// six or so` invites invention,
`// exactly these four: Nike, Google, Oura, Patagonia` forbids it.

## Example

```
---
route: /
theme: dark
---

**{Color,Background} #0A0A0F, {Color,Surface} #14141C, {Color,Text} #E8E6F0**
**{Color,Accent 1} #7C3AED, {Color,Accent 2} #22D3EE**
**{Font,Heading} "Playfair Display" serif, {Font,Body} "Inter" sans-serif**
__on mobile: stack everything, padding 24px__

> Navbar
*sticky top, space-between, padding 20px 5%, background {Color,Background}*
>> UI-MD
*confident, like it knows what it's doing*
>> - [Pricing][pricing]
   - [FAQ][faq]
*ghost, 14px, gap 24px*
>> [[Get Started]][signup]
*background {Color,Accent 1}, padding 8px 20px, radius 8px*

> Hero
*deep breath energy — calm, centered, room to exist. max-width 800px, padding 120px 5%*
>> # Design at the speed of thought.
*massive, gradient {Color,Accent 1} to {Color,Accent 2}, 'thought' in italic*
>> A markdown-native language for AI-driven interfaces. Stop writing boilerplate.
*soft, like a whisper right after the shout. opacity 70%, margin-top 16px*
>> [[Start Free Trial]][signup]
*irresistible, warm, radius 8px, padding 14px 28px*
_on mobile: full width_
// fires trial_start, focus ring required
>> ![Preview of a screen built in UI-MD](preview.png)
*floaty, like it's hovering just above the page. radius 16px*

---

> Pricing
*align center, padding 100px 5%, gap 32px*
>> ## Simple, transparent pricing.
*font-size 40px, weight 700, centered*
>> - [x] Monthly
   - [ ] Annual, save 20%
*single-select, pill, satisfying to toggle*
// flipping to Annual drops all three prices 20%

| Plan | Price | Projects | |
|:--|--:|--:|--|
| Developer | Free | 1 | [[Get Started]][signup] |
| Pro | ~~$39~~ $29 | Unlimited | [[Get Started]][signup] |
| Enterprise | Custom | Unlimited | [[Contact Sales]][contact] |
*lift the Pro row — border 2px {Color,Accent 1}*

> FAQ
*calm, centered, breathing room. padding 80px 5%*
>> ## Frequently asked questions.
*font-size 32px, weight 700, centered*
>> () Search questions...
*width 400px, radius 8px, inviting, not demanding*
>> - (All)
   - (Billing)
   - (Setup)
   - (API)
*clickable, toggles active, pill-shaped, the picked one lights up with {Color,Accent 1}*
>> Can I switch between monthly and annual billing?
*accordion, one open at a time, border-bottom 1px {Color,Surface}*
// six or so, spanning billing, setup and API

> Footer
*space-between, padding 60px 5%, border-top 1px {Color,Surface}, fading out gently*
>> Acme Corp © 2026. All rights reserved.[^terms]
*opacity 50%, 14px*
>> :twitter: :github: :discord:
*gap 16px, color {Color,Accent 1}, tucked away, not asking for attention*

[^terms]: Prices exclude VAT. Annual billing renews automatically.

[pricing]: #pricing
[faq]: #faq
[signup]: /auth/signup
[contact]: /sales/contact
```

## Limits

- Structure is reproducible. Styling is interpreted — two runs will differ.
- No round-trip. Once a model emits React, the code and the file diverge.
- Paths are names, not IDs. Rename a container and every pointer stops matching.
- No component reuse. Defining a card once and calling it elsewhere needs a new
  sigil and a resolution order. Left open on purpose.

Why it's shaped this way: [RATIONALE.md](RATIONALE.md).

No IDs, no schema, no parser, no validator. If a shape doesn't make something
shorter or clearer, it isn't here.
