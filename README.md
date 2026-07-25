# UI-MD

Designing with LLMs is annoying.

Saying which layer a component belongs in, or that this one specific button needs a different font, takes a paragraph — and the model still guesses wrong.

UI-MD mixes Markdown and basic CSS into a stupidly simple dictionary, so designers and machines can point at the same thing and mean the same thing.

## The idea, in one example

You write this:

```
> Card
>> [Click Here](signup)
>> [Follow us](https://twitter.com/acme)
```

That's a container with two links in it. `>>` just means "one level deeper." `signup` with no `https://` is an internal page — a screen elsewhere in the same product. A full URL is external. That's most of the language.

Hand this to a model along with the rules file below, and it builds the actual screen (React, HTML, Figma — whatever you ask for).

## Later, when you want to change one thing

Once a screen is written, you can point at any single piece of it by walking down the same path:

```
Card >> [Click Here](signup)
```

"The link, inside the card." No need to describe it — just read the path off the file you already have.

## What's in this repo

| File | What it's for |
|---|---|
| [`assets/UI-MD_manifest.md`](assets/UI-MD_manifest.md) | Why this exists — the short pitch. Read this first. |
| [`assets/UI-MD_skill.md`](assets/UI-MD_skill.md) | The rules for writing a screen. Give this to the model as its instructions. |
| [`assets/UI-MD_pointer.md`](assets/UI-MD_pointer.md) | The rules for pointing at one exact thing inside a screen you already wrote. |
| [`assets/UI-MD_landingpage-example.md`](assets/UI-MD_landingpage-example.md) | A full example — a real landing page written in UI-MD, so you can see the rules in use. |
| [`assets/UI-MD_landingpage-example-casual.md`](assets/UI-MD_landingpage-example-casual.md) | The same page, written casually instead of in CSS-speak — proof the tidy version is optional. |

## Using it

1. Give a model [`UI-MD_skill.md`](assets/UI-MD_skill.md) as its system instructions.
2. Write your screen in UI-MD.
3. To edit one thing later, give the model [`UI-MD_pointer.md`](assets/UI-MD_pointer.md) plus a path to what you want changed, e.g. `Card >> [Click Here](signup)`, and say what should change.

## The shapes, quickly

- `>` `>>` `>>>` — how deep something is nested (max 3 levels)
- `# H1` / `## H2` / `### H3` — headings
- `[x] Label` / `[ ] Label` — checkbox, checked / unchecked
- `<x> Label` / `<> Label` — radio, selected / unselected
- `[Label]` — button
- `[Label](url)` — link
- `![alt text](image.jpg)` — image
- `:icon-name:` — icon
- `// note` — context for the model, never shown on screen
- `$Token$` — pull an exact value from your design system, e.g. `$Border Width,200$`
- `*local instructions*` — a note attached to the thing above or below it
- `**global instructions**` — a note that applies to the whole screen

## A full example

A real landing page, written entirely in UI-MD:

```
> Navbar
*spread out, logo left, links and button right, sticky top*
>> UI-MD
*bold wordmark*
>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
>> [Get Started](signup)
*background $Color,Accent 1$, stands out from the rest*

> Hero
*centered, lots of padding*
>> # Design at the speed of thought.
*huge, gradient $Color,Accent 1$ to $Color,Accent 2$*
>> ### A markdown-native language for AI-driven interfaces. Stop writing boilerplate.
*softer, faded*
>> [Start Free Trial](signup)
*background $Color,Accent 2$, glows on hover*
>> ![Preview of a screen built in UI-MD](preview.png)
*rounded corners, shadow*

> Pricing Section
*centered, stacked, generous padding*
>> ## Simple, transparent pricing.
*bold, centered*
>> <x> Monthly
>> <> Annual, save 20%
*pill-shaped toggle*
// switching to Annual should update all three card prices to reflect the 20% discount

>> Developer Card
*plain card*
>>> ### Developer
>>> Free forever, for one project.
>>> [Get Started](signup)

>> Pro Card
*stands out — border $Color,Accent 1$, scaled up a little*
>>> ### Pro
>>> $29/month, unlimited projects.
>>> [Get Started](signup)
*solid button, background $Color,Accent 1$*

>> Enterprise Card
*understated*
>>> ### Enterprise
>>> Custom pricing, talk to sales.
>>> [Contact Sales](contact)
*outline button*

> Footer
*spread out, quiet, faded*
>> Acme Corp © 2026. All rights reserved.
>> :twitter: :github: :discord:
*spaced out*
```

Same page, written casually instead — see [UI-MD_landingpage-example-casual.md](assets/UI-MD_landingpage-example-casual.md).

## One thing to know

The shapes above are the only part that's really "UI-MD." What goes *inside* a `*rule*` is just plain CSS-ish description — things like `padding 32px`, `background $Color,Accent 1$`, `align center`, `on hover: translate Y -4px`. You don't need to write real CSS syntax, but knowing the basic vocabulary helps you say what you mean instead of hoping the model guesses right.

The ones that come up constantly:

- **Spacing:** padding, margin, gap
- **Layout:** align, center, stack, flex-row / flex-col, width, overflow
- **Look:** background, color, border, rounded, shadow, opacity
- **Text:** font, weight, uppercase, text size
- **Motion:** on hover / on click / on load, transform, translate, rotate, animate, duration, infinite

If a term isn't in that list, plain English usually works fine. The shapes are the strict part of the language; the rules are closer to talking, not coding.

## Or just say it however you'd normally say it

If you don't know the "real" word, don't stop to look it up — say it like you would out loud. Both sides below work the same:

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

Same result either way — the model translates it, not you. The tidier version is just faster to type once it's second nature. Start on the left side of the table and move right whenever it feels natural, not before.
