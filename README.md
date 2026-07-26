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
- `---` — divider, on its own line
- `# H1` / `## H2` / `### H3` — headings
- `[x] Label` / `[ ] Label` — checked / unchecked (checkbox or radio — add `*single-select*` on the group for radio-style behavior)
- `[Label]` — button
- `<Label>` — filter chip (toggles active on click)
- `<> Placeholder` — text input
- `[Label](url)` — link
- `![alt text](image.jpg)` — image
- `:icon-name:` — icon
- `// note` — context for the model, never shown on screen
- `$Token$` — pull an exact value from your design system, e.g. `$Border Width,200$`
- `*local instructions*` — a note attached to the thing above or below it
- `**global instructions**` — a note that applies to the whole screen

## A full example

The same landing page, two ways. First, precise — real CSS-ish values, nothing left to guess:

```
> Navbar
*align-center, justify-space-between, padding: 20px 5%, position: sticky-top, background: $Color,Background$*
>> UI-MD
*font-weight: 700, font-size: 20px*
>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
*variant: ghost, font-size: 14px*
>> [Get Started](signup)
*background: $Color,Accent 1$, padding: 8px 20px, border-radius: 8px*

> Hero
*align-center, justify-center, text-align: center, padding: 120px 5%, max-width: 800px, margin: 0 auto*
>> # Design at the speed of thought.
*font-size: 80px, background: linear-gradient(90deg, $Color,Accent 1$, $Color,Accent 2$), background-clip: text*
>> ### A markdown-native language for AI-driven interfaces. Stop writing boilerplate.
*font-size: 20px, opacity: 70%, margin-top: 16px*
>> [Start Free Trial](signup)
*background: $Color,Accent 2$, padding: 14px 28px, border-radius: 8px, on-hover: box-shadow 0 0 24px $Color,Accent 2$*
>> ![Preview of a screen built in UI-MD](preview.png)
*border-radius: 16px, box-shadow: 0 20px 40px rgba(0,0,0,0.4)*

> Pricing Section
*align-center, flex-col, padding: 100px 5%*
>> ## Simple, transparent pricing.
*font-size: 40px, font-weight: 700, text-align: center*
>> [x] Monthly
>> [ ] Annual, save 20%
*single-select, border-radius: 999px, padding: 8px*
// switching to Annual should update all three card prices to reflect the 20% discount

>> Developer Card
*background: $Color,Surface$, border-radius: 16px, padding: 40px*
>>> ### Developer
*font-size: 24px*
>>> Free forever, for one project.
*opacity: 70%, margin: 12px 0*
>>> [Get Started](signup)
*width: 100%*

>> Pro Card
*background: $Color,Surface$, border: 2px solid $Color,Accent 1$, border-radius: 16px, padding: 40px, transform: scale(1.05)*
>>> ### Pro
*font-size: 24px*
>>> $29/month, unlimited projects.
*opacity: 70%, margin: 12px 0*
>>> [Get Started](signup)
*width: 100%, background: $Color,Accent 1$, border-radius: 8px*

>> Enterprise Card
*background: $Color,Surface$, border-radius: 16px, padding: 40px, opacity: 90%*
>>> ### Enterprise
*font-size: 24px*
>>> Custom pricing, talk to sales.
*opacity: 70%, margin: 12px 0*
>>> [Contact Sales](contact)
*width: 100%, variant: outline, border: 1px solid $Color,Accent 1$*

> FAQ Section
*align-center, flex-col, padding: 80px 5%*
>> ## Frequently asked questions.
*font-size: 32px, font-weight: 700, text-align: center*
>> <> Search questions...
*width: 400px, margin: 24px 0, padding: 12px 16px, border-radius: 8px, background: $Color,Surface$*
>> <All>
>> <Billing>
>> <Setup>
>> <API>
*pill-shaped, gap: 12px, active one gets background $Color,Accent 1$*

> Footer
*align-center, justify-space-between, padding: 60px 5%, border-top: 1px solid $Color,Surface$*
>> Acme Corp © 2026. All rights reserved.
*opacity: 50%, font-size: 14px*
>> :twitter: :github: :discord:
*gap: 16px, color: $Color,Accent 1$*
```

Now the dumb version — same structure, every rule swapped for a feeling instead of a property:

```
> Navbar
*keep it breezy — logo chilling on the left, stuff floating on the right, stays put when you scroll*
>> UI-MD
*confident, like it knows what it's doing*
>> [Features](#features)
>> [Pricing](#pricing)
>> [FAQ](#faq)
*whisper quiet, just kinda there*
>> [Get Started](signup)
*this is the star of the show, make it glow*

> Hero
*deep breath energy — calm, centered, room to exist*
>> # Design at the speed of thought.
*massive, a mic-drop moment, feels alive*
>> ### A markdown-native language for AI-driven interfaces. Stop writing boilerplate.
*soft, like a whisper right after the shout*
>> [Start Free Trial](signup)
*irresistible, warm, makes you want to click without thinking about it*
>> ![Preview of a screen built in UI-MD](preview.png)
*floaty, like it's hovering just above the page*

> Pricing Section
*calm, spacious, no rush*
>> ## Simple, transparent pricing.
*confident and clear, no games*
>> [x] Monthly
>> [ ] Annual, save 20%
*pick one — cute little switch, satisfying to toggle*
// heads up: flipping to Annual needs to update all three prices with the discount

>> Developer Card
*chill, no pressure, just here if you need it*
>>> ### Developer
>>> Free forever, for one project.
>>> [Get Started](signup)

>> Pro Card
*the golden child — make everyone want to be here*
>>> ### Pro
>>> $29/month, unlimited projects.
>>> [Get Started](signup)
*loud and proud, this is the one*

>> Enterprise Card
*quietly confident, doesn't need to try hard*
>>> ### Enterprise
>>> Custom pricing, talk to sales.
>>> [Contact Sales](contact)
*understated, almost whispering*

> FAQ Section
*calm, centered, breathing room*
>> ## Frequently asked questions.
*clear, confident, no fluff*
>> <> Search questions...
*simple, inviting, not demanding*
>> <All>
>> <Billing>
>> <Setup>
>> <API>
*little chips, satisfying to tap, the picked one lights up*

> Footer
*fading out gently, like the credits rolling*
>> Acme Corp © 2026. All rights reserved.
>> :twitter: :github: :discord:
*tucked away, not asking for attention*
```

Same layout, same result either way — the model translates it, not you.

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
