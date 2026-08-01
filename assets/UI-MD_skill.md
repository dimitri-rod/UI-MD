# UI-MD — rules for the model

You are given screens written in UI-MD. Build them. Later you will be asked to change one named part.

Three kinds of thing: **primitives** (what exists), **modifiers** (how it looks), **notes** (context you use but never render).

---

## Structure

`>` opens a container. Each additional `>` is one level deeper. The word after `>` is its name.

```
> Pricing Section
>> Pro Card
>>> ## Pro
```

Container names are arbitrary — section, card, banner, accordion, drawer. No fixed list, no depth limit.

**Names are unique within a file, and they are addresses.** Preserve them. When you emit code, carry each container's name through as a class, component name, or comment so it can be found again.

---

## Primitives

| Shape | Renders as |
|---|---|
| `> Name` | Container |
| `# H1` `## H2` `### H3` | Heading |
| any bare line | Body copy — paragraph, subtitle, caption or label, decided by position |
| `[Link](url)` | Text link, no button styling |
| `[[Button]]` | Button |
| `[[Button]](url)` | Button that navigates |
| `<> Placeholder` | Text input, placeholder is the text |
| `<Label>` | Tag or pill |
| `[x] Item` / `[ ] Item` | Checked / unchecked |
| `![alt](image.jpg)` | Image |
| `:icon-name:` | Icon |
| `---` | Divider, on its own line |

**Links.** A target with no `https://` is an internal page elsewhere in the same product. A full URL is external.

**Checkboxes.** A group defaults to multi-select. `*single-select*` on the group makes it radio-style.

**Tags.** `*clickable, toggles active*` on a group makes them filters.

---

## Modifiers

A line wrapped in `*asterisks*` modifies **the run of lines directly above it**. Never anything below. This is absolute — when in doubt, bind upward.

The run ends at whichever comes first, reading upward: a blank line, another modifier, or a container at a shallower depth.

```
> Navbar
*sticky top, space-between, padding 20px 5%*

>> UI-MD
*font-weight 700, 20px*

>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
*ghost, 14px*

>> [[Get Started]](signup)
*background $Color,Accent 1$, rounded 8px*
```

In order: the whole navbar, the logo alone, all three links, the button alone.

That is how sibling groups are styled — there is no separate group syntax. A modifier on a container is inherited by everything nested under it.

**Contents are free prose.** `padding 24px` and `make it bigger` are equally valid. Interpret intent; do not ask the user to be more precise.

### Local and global

`*single asterisks*` are **local** — the run of lines above.
`**double asterisks**` are **global** — the whole file, wherever they appear. A file may hold one screen or several; global reaches all of them.

```
**base font Inter, spacing unit 8px, rounded 12px, motion 200ms ease-out**
**$Color,Accent 1$ #6366F1, $Color,Accent 2$ #EC4899**
```

A `Global` block at the top is the conventional home for tokens and defaults, but it is a convention — a `**global**` line is valid anywhere.

**Precedence:** `Global` block, then `**global**` lines (later beats earlier), then `*local*` modifiers. Children inherit; the nearest declaration wins.

**Report global rules back.** `*` and `**` differ by one character and both render as emphasis, so a mistyped local rule silently becomes page-wide. After building, list every global rule you applied — one line each. Never fail silently on scope.

**`***three asterisks***` is undefined.** Scope stops at the file. Treat it as `**global**`, and say that you did, so it surfaces as a typo rather than becoming a feature. The level above the file is the design system — a separate upstream file that UI-MD files *read* from via `$Token$`. Nothing in a UI-MD file may change it, and no UI-MD file may reach into another.

### Tokens

`$Name,Variant$` is an exact value from the user's design system — `$Color,Accent 1$`, `$Border Width,200$`.

Never approximate. If a token has no definition in the `Global` block or supplied context, emit it as a named variable (CSS custom property or theme key) rather than guessing a value.

A token is a binding, not a value. It stays a token even when nothing defines it yet — that's the point of writing one.

---

## Notes

`// text` is context for you. Never render it.

A note **binds upward**, like a modifier — to the run of lines directly above it. Same rule, same boundaries, so a reader always knows which node a note is about.

```
>> [x] Monthly
>> [ ] Annual, save 20%
*single-select*
// switching to Annual updates all three card prices with the discount
```

---

## Building

1. Read `Global` first. Establish tokens, type scale, spacing, motion.
2. Build the tree in order. Depth is layout nesting.
3. Apply modifiers upward, inheriting downward.
4. Carry container names into the output so they remain addressable.
5. Fill unspecified detail with sensible defaults consistent with `Global`. Do not invent content, copy, or sections that were not written.

Where a state is implied but not written — hover, focus, disabled, empty, error — implement a reasonable one rather than omitting it.

---

## Changing

An edit arrives as a name, a colon, and an instruction.

```
Pro Card: thicker border, make it feel premium
FAQ Search: move it above the chips
Enterprise Card: remove it
Pro Card on hover: soft glow, lift slightly
Pricing Section on mobile: stack the cards, full width
```

- Resolve the name against the UI-MD file, then locate that node in the code by the name you carried through.
- **Change only that node.** Do not restructure, reformat, or improve surrounding code.
- `on hover`, `on mobile`, `when empty` and similar scope the change to that state or breakpoint. Leave the base case untouched.
- A repeated **primitive** label resolves to all of them — three `[[Get Started]]` buttons are three hits. Apply the change to each, then say how many you changed and where.
- An ambiguous **container** name is an error, not a choice. Names are unique by rule, so a collision means the file is broken. Stop and ask.
- If a name resolves to nothing, say so. Do not create it, and do not fall back to searching the built code — a name that isn't in the file has no address.
- If the edit replaces a `$Token$` with a literal, say so and name the token you dropped. Silently overwriting one decouples that node from the design system, and nothing downstream will notice.

After an edit, update the UI-MD file to match. The file and the screen must not drift.

Write the change into the **modifier** of the node it addresses. Never store a rule in a `// note` — notes don't render, so a rule left there won't survive the next build. A note may sit alongside the modifier to explain the reasoning behind it:

```
> Pricing Section
*align-center, flex-col, padding: 100px 5%, gap: 32px, on mobile: stack vertically*
// equal height, no scale on the featured card — hierarchy comes from the border
```
