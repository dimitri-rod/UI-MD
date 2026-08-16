# UI-MD Dictionary

**Shapes are structure. Rules are prose.**

Structure is strict — depth, membership, order, position. Get a `>` wrong and
the tree is wrong. How a thing *looks* is never a shape. It goes in a rule, in
whatever words you have. Miscount a `>` and the screen is wrong; say
`*make it pop*` and you've only been vague.

Meaning is defined here and nowhere else. A UI-MD file stays legible in a
Markdown preview and we don't break that on purpose, but nothing in the
language means what it means because a renderer says so.

## Shapes

Fifteen of them.

| IF | THEN |
|:--|:--|
| `> Name` | container. Each extra `>` goes one level deeper. No depth limit. |
| `#` `##` `###` … `######` | heading. Six levels, six is the ceiling. |
| any bare line | body copy — paragraph, subtitle or caption, by position |
| `[Link](url)` | text link. `#name` is a container in this file; no `https://` is a page in the same product. |
| `[[Button]]` | button |
| `[[Button]](url)` | button that navigates |
| `[[Button]][name]` | button that navigates to a defined destination |
| `() Placeholder` | text input |
| `(Label)` | tag, alone on a line. `*clickable, toggles active*` makes filters. |
| `[x] Item` / `[ ] Item` | checked / unchecked. As a set, multi-select unless `*single-select*`. |
| `![alt](image.jpg)` | image |
| `:icon-name:` | icon |
| `---` | divider. Leave a blank line above it. |
| `// text` | note for whoever builds this. Never becomes UI. |
| `{Name,Variant}` | value from your design system |

**A shape owns its whole line.** Past the `>` markers, a line made only of
shapes is shapes; a line with prose in it is body copy, and any brackets,
parens or colons inside it are just characters. So `(Draft)` alone is a tag,
`Free forever (for one project)` is a sentence, and `$29/month` is a price.

**A `>` line is a container if deeper lines follow it, content if they don't.**
`>> Pro Card` with `>>>` lines under it is a container named Pro Card;
`>>> Free forever, for one project.` is a line of body copy.

Container names are yours to pick — section, card, banner, drawer. A two-column
layout is two named containers at the same depth.

## Sets

Markdown that was sitting unclaimed. Nothing above changes.

| IF | THEN |
|:--|:--|
| `- item` | item in a set — nav links, features, anything that repeats |
| `- item` indented under another | item in a subset — a dropdown |
| `1. item` | item in an ordered sequence — steps, a wizard |
| pipe table | grid or comparison — a pricing matrix |
| `[name]: /route` at the bottom | define a destination once, use `[name]` anywhere |
| `---` block at the very top | screen settings: route, theme, breakpoints |
| ` ```json ` | data behind a repeat, or any block that isn't UI-MD |

A set is one element, not several that happen to be adjacent. Four nav links at
the same depth are four things to place; as a list they are one collection, and
what gets built is a repeat.

## Rules

| IF | THEN |
|:--|:--|
| `*rule*` | the element above |
| `**rule**` | the whole screen |
| `_rule_` | one breakpoint or state |

**A rule attaches to the element above it. Never below.** The element is a
line, a list, a table or a container — whichever ends directly above the rule.
Containers pass their rules down to their children.

Rules stack. Several in a row all attach to the one element above the stack, so
a base rule, a breakpoint and a state can sit together.

To rule several things at once, make them a set. That is what sets are for, and
it is why no rule ever spans a run of lines.

```
>> - [Pricing][pricing]
   - [FAQ][faq]
*ghost, 14px, gap 24px*
```

Local beats global, later beats earlier, children inherit.

One character separates `*` from `**`, and both render as emphasis — so list
every global rule you applied. `***rule***` is undefined: treat it as global,
and report it as a probable typo.

A `{Token}` is a binding, not a value. It stays one even when nothing defines
it yet. If an edit replaces one with a literal, say so.

## Building

Globals first, then the tree in order. Fill in unspecified detail; don't invent
content or sections that weren't written.

**One written item is a pattern.** Where content repeats — FAQ entries, table
rows, cards in a feed — write one and fill the rest:

```
>> Can I switch between monthly and annual billing?
*accordion, one open at a time*
// six or so, spanning billing, setup and API
```

That's the only case where content you didn't write gets added, and the note
controls how far it goes. `// six or so` invites invention.
`// exactly these four: Nike, Google, Oura, Patagonia` forbids it — use that
form for anything named, like clients, logos or people, where a plausible
invention is a false claim.

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
variant over the base case and leave the base alone. Update the file after, in
the rule that owns the element — never in a `// note`, which never becomes UI,
so a rule left in one won't survive the next build.

## Declined

Free, deliberately unused. Each is a look or an instruction, and those live in
rules. Claiming them would create two ways to say one thing.

| Available | Say instead |
|:--|:--|
| `~~x~~` | `*'$29' crossed out, it's the old price*` |
| `` `x` `` | `*keep 'Start Free Trial' exactly*` |
| `[^x]` footnote | `// text` |
| `:--` `--:` in tables | `*right-align the price column*` |
| `\` escape | nothing to escape — a shape owns its whole line |
| `<https://acme.com>` | `[Acme](https://acme.com)` |

## Never

Rules of the language.

| IF | THEN |
|:--|:--|
| a look in a shape | say it in a rule |
| `#######` | not a heading, six is the max |
| `$` | ordinary character. Prices are just prices. |
| a rule below its element | it attaches above, always |

Courtesies. None of these change what a file means — they change what a
reviewer sees in a preview, which is worth keeping.

| IF | THEN |
|:--|:--|
| `---` directly under text, outside frontmatter | turns that line into a heading — leave a blank line |
| `<tag>` | stripped by renderers, content disappears |
| 4-space indent | collides with list continuation, use fences |
| `:x:` `:warning:` as icon names | collide with emoji shortcodes, pick another name |

## Example

```
---
route: /
theme: dark
---

**{Color,Background} #0A0A0F, {Color,Surface} #14141C, {Color,Text} #E8E6F0**
**{Color,Accent 1} #7C3AED, {Color,Accent 2} #22D3EE**
**{Font,Heading} "Playfair Display" serif, {Font,Body} "Inter" sans-serif**

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
|--|--|--|--|
| Developer | Free | 1 | [[Get Started]][signup] |
| Pro | $29 | Unlimited | [[Get Started]][signup] |
| Enterprise | Custom | Unlimited | [[Contact Sales]][contact] |
*right-align price and projects, lift the Pro row — border 2px {Color,Accent 1}*

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
>> Acme Corp © 2026. All rights reserved.
*opacity 50%, 14px*
>> :twitter: :github: :discord:
*gap 16px, color {Color,Accent 1}, tucked away, not asking for attention*

[pricing]: #pricing
[faq]: #faq
[signup]: /auth/signup
[contact]: /sales/contact
```

Why it's shaped this way: [RATIONALE.md](RATIONALE.md).

No IDs, no schema, no parser, no validator. If a shape doesn't make something
shorter or clearer, it isn't here.
