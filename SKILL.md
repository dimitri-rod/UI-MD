---
name: ui-md
description: Write, compile, or edit UI-MD — a Markdown dictionary for describing a UI screen to a model, then changing one piece of it by name instead of re-describing it. Use when a file nests `>` containers with `*rule*` lines under them, when turning a screen spec into React, HTML or Figma, or when an instruction points at a named component like `Pricing >> Pro Card`.
---

# UI-MD

Shapes are structure. Rules are prose. Every entity in Markdown has exactly one
meaning below. If a shape isn't in the table, don't invent it — use plain text
and a `*rule*`.

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

## Reading

A line that is entirely one shape is that shape. Inside a line of prose,
everything is text. `*ghost, 14px*` alone on a line is a rule, `*really*` inside
a sentence is italic, `(Draft)` alone is a tag, `Free forever (for one project)`
is a sentence.

A `>` line is a container if deeper lines follow it, content if they don't.
Names are unique in the file.

A rule attaches to the element above it, never below — a line, a list, a table
or a container. Containers pass rules down. Rules stack. Several things ruled at
once are a set.

Local beats global, later beats earlier, children inherit.

```
> Hero
*calm, centered, room to exist. max-width 800px*
>> # Design at the speed of thought.
*massive, gradient {Color,Accent 1} to {Color,Accent 2}*
>> [[Start Free Trial]][signup]
*irresistible, warm, radius 8px*
_on mobile: full width_
// fires trial_start

[signup]: /auth/signup
```

## Compiling

Globals first, then the tree in order.

Fill in unspecified detail. Don't invent content or sections that weren't
written — except where one item is a pattern, and then the `// note` says how far
to take it: `// six or so` invites invention, `// exactly these four: ...`
forbids it.

Carry container names into the emitted code so they stay findable.

List every global rule you applied.

## Editing

`Path >> Element: instruction` changes that element and nothing else.
`#2` picks the second match when siblings are identical.

Update the file afterwards, in the rule that owns the element. Never in a
`// note` — notes never become UI, so a rule left in one won't survive the next
build.

A `{Token}` is a binding, not a value. If an edit replaces one with a literal,
say so.
