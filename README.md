# UI-MD

Designing with an LLM is a conversation with someone who can't see what
you're looking at.

You describe a screen. It builds something. It's close. You want the button in
the middle pricing card to be quieter — not the other two, that one. So you
write a paragraph locating it. *The call-to-action in the highlighted plan, the
one in the middle, not the header button.* The model reads your paragraph,
guesses, and changes the wrong button.

The model isn't bad at design. You have no way to point.

## What it is

UI-MD is a dictionary. Fifteen shapes, all of them ordinary Markdown, each
assigned exactly one meaning in an interface.

You describe a screen in plain text. A model builds it — React, HTML, Figma,
whatever you ask for. Later, when you want to change one thing, you point at it
by reading its path off the same file.

The file is the brief and the map. That's the whole idea.

The syntax is [DICTIONARY.md](DICTIONARY.md), and it is the only place the
syntax lives.

## Two halves, deliberately unequal

**Shapes are structure.** A `>` opens a container, and each extra `>` goes one
level deeper. `[[Button]]` is a button. `[ ]` is an unchecked box. These are
strict. Miscount a `>` and the tree is wrong, the same way a misplaced brace
breaks code.

**Rules are prose.** Everything about how a thing looks lives between
asterisks, in whatever words you have.

```
*padding 14px 28px, radius 8px, background {Color,Accent 1}*
```

```
*irresistible, warm, makes you want to click without thinking*
```

Both are valid. Both work. The model translates, not you. If you know the CSS
word, use it — it's faster once it's second nature. If you don't, say it the
way you'd say it out loud and keep moving.

This split is the design. It means the strict part is small enough to learn in
a minute, and the loose part is as expressive as your vocabulary. It also tells
you which mistakes matter: get a `>` wrong and the screen is wrong; write *make
it pop* and you've only been vague.

## What it looks like

```
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
```

A container. A heading. A line of body copy. A button that navigates to a
destination defined once at the bottom of the file. A rule for one breakpoint.
A note for whoever builds it, which never becomes UI.

Nothing here needs explaining to a designer, and nothing here needs parsing
help from a model. Both sides already read Markdown.

## Pointing

Once a screen exists, you address any piece of it by walking the same path you
wrote.

```
Hero >> [[Start Free Trial]]
```

The button, inside the hero. No paragraph. No hedging about which one.

When several siblings look identical — a `[[Get Started]]` on every row of a
pricing table — you index.

```
Pricing >> [[Get Started]] #2
```

This is the part that changes how it feels to work. Editing stops being
re-describing. You read the coordinate off the file and say what should change.

## Why Markdown, specifically

Three reasons, none of them aesthetic.

**Models have read more Markdown than any other format.** Structure comes for
free. You aren't teaching a parser; you're using notation the model already
understands deeply, then narrowing what a few characters mean.

**It renders, and that's a bonus rather than a rule.** A UI-MD file previewed
on GitHub is a legible low-fi wireframe — headings, lists, tables, images and
checkboxes all appear as themselves, so anyone can review a screen in a pull
request with no tooling installed. But meaning is defined in the dictionary and
nowhere else. No shape means what it means because a renderer says so. Where
keeping the preview honest is free, the dictionary says how; where it would
cost a rule, the preview loses.

**It's typeable.** No canvas, no plugin, no editor, no account. A text file in
whatever you already have open. Version-controlled, diffable, greppable,
pasteable into any chat window.

## What it doesn't do

It isn't a design tool, and it isn't trying to replace one. It produces a first
draft of a screen that doesn't exist yet, fast, in a form both a person and a
model can hold in their head.

It isn't precise about looks. Structure is reproducible — depth, order, and
membership survive every generation. Styling is interpreted, and two runs will
differ. The file looks like a spec, which makes it tempting to trust like one.
It's exact in layout and approximate in appearance.

It doesn't round-trip. The moment a model turns UI-MD into React, the two
diverge. Developers edit the code, designers edit the `.md`, and within a week
neither describes the product. UI-MD relocates that problem rather than solving
it. It's most valuable at the beginning of a screen's life and progressively
less so as the screen ages.

Paths are names, not identifiers. Rename a container or reword a button and
every pointer to it silently stops matching.

There's no component reuse. Defining a card once and calling it elsewhere needs
a new sigil and a resolution order — real power, at the cost of the thing that
makes this typeable. Left open on purpose.

None of these are secret. Knowing them is the difference between using the
format well and being disappointed by it.

## Who it's for

Anyone who describes interfaces to a machine and is tired of describing the
same interface twice.

Designers who think in screens and want a first build without opening a design
tool. Product people who can specify a page but not draw one. Engineers who
want the brief in the repo instead of in a comment thread. Anyone iterating
with a model who has noticed that the second request is always harder than the
first, because the first had no context to point at and the second has too
much.

## The shortest version

Write the screen. Get it built. Point at one piece. Change it.

Fifteen shapes. The rules are just talking. The file renders as a wireframe,
versions like code, and stays readable by both parties for as long as anyone
bothers to keep it true.

That last part is on you. Everything else the format handles.

***

[DICTIONARY.md](DICTIONARY.md) — the syntax, and the only copy of it.
[RATIONALE.md](RATIONALE.md) — why it's shaped this way.
