# UI-MD Dictionary

**Shapes are structure. Rules are prose.**

Every entity in Markdown has exactly one meaning here. Nothing is reserved,
nothing is forbidden, nothing renders as a surprise. Six shapes are additions —
Markdown had no button, input, tag, note, token or icon.

**A line that is entirely one shape is that shape. Inside a line of prose,
everything is text.** So `*ghost, 14px*` alone on a line is a rule, `*really*`
inside a sentence is italic, `(Draft)` alone is a tag, and
`Free forever (for one project)` is a sentence.

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

## Structure

**A `>` line is a container if deeper lines follow it, content if they don't.**
`>> Pro Card` with `>>>` lines under it is a container named Pro Card;
`>>> Free forever, for one project.` is a line of body copy.

Container names are yours to pick — section, card, banner, drawer. A two-column
layout is two named containers at the same depth.

## Rules

**A rule attaches to the element above it. Never below.** The element is a
line, a list, a table or a container — whichever ends directly above the rule.
Containers pass their rules down. Rules stack: several in a row all attach to
the one element above the stack.

To rule several things at once, make them a set.

```
>> - [Pricing][pricing]
   - [FAQ][faq]
*ghost, 14px, gap 24px*
```

Local beats global, later beats earlier, children inherit. One character
separates `*` from `**`, so list every global rule you applied.

A `{Token}` is a binding, not a value. It stays one even when nothing defines
it yet. If an edit replaces one with a literal, say so.

## Building

Globals first, then the tree in order. Fill in unspecified detail; don't invent
content or sections that weren't written.

**One written item is a pattern.** Where content repeats — FAQ entries, table
rows, cards in a feed — write one and fill the rest. The note controls how far:
`// six or so` invites invention, `// exactly these four: Nike, Google, Oura,
Patagonia` forbids it. Use the forbidding form for anything named, where a
plausible invention is a false claim.

## Pointing

Walk the same path you wrote.

```
Hero >> [[Start Free Trial]]
Navbar >> - [Pricing][pricing]
Pricing >> [[Get Started]] #2
Hero >> [[Start Free Trial]] _on mobile_
```

`#2` picks the second match when several siblings are identical. Paths are
names, not IDs — rename a container or reword a button and the path stops
matching.

Only that element changes. `on hover`, `on mobile`, `when empty` layer a
variant over the base case. Update the file after, in the rule that owns the
element — never in a `// note`, which never becomes UI.

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

Why it's shaped this way: [RATIONALE.md](RATIONALE.md).

No IDs, no schema, no parser, no validator. If a shape doesn't make something
shorter or clearer, it isn't here.
