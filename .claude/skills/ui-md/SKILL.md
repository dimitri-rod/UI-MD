---
name: ui-md
description: Write, compile, or edit UI-MD — a Markdown dictionary for describing a UI screen to a model, then changing one piece of it by name instead of re-describing it. Use when a file nests `>` containers with `*rule*` lines under them, when turning a screen spec into React, HTML or Figma, or when an instruction points at a named component like `Pricing >> Pro Card`.
---

# UI-MD

The dictionary is [README.md](../../../README.md). Read it before writing or
compiling. Every Markdown entity has one meaning there; if a shape isn't in the
table, don't invent it — use plain text and a `*rule*`.

## Compiling

Globals first, then the tree in order.

Fill in unspecified detail. Don't invent content or sections that weren't
written — except where one item is a pattern, and then the `// note` says how
far to take it.

Carry container names into the emitted code so they stay findable.

List every global rule you applied.

## Editing

`Path >> Element: instruction` changes that element and nothing else.

Update the file afterwards, in the rule that owns the element. Never in a
`// note` — notes never become UI, so a rule left in one won't survive the next
build.

If an edit replaces a `{Token}` with a literal, say so.
