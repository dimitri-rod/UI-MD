# UI-MD_pointer.md

**Title:** UI-MD Pointer Syntax
**Version:** 1.1
**Date:** 2026-07-25

**Purpose:** A way to point at one specific element inside a UI-MD document, so a designer can say "change this" instead of describing it in prose. The layout file itself is the map — a pointer is just directions through it.

**Syntax:** Chain element names or symbols with `>>`, from outermost to innermost, ending at the target.

```
Navbar >> [Get Started](signup)
```

This reads: inside "Navbar," the link labeled "Get Started."

**Rules**

1. **Named containers** (plain-text container names, e.g. `Navbar`, `Hero`, `Pricing Section`) are referenced by that name.
2. **Elements** (buttons, links, checkboxes, filter chips, headings) are referenced by their symbol + label, e.g. `[Get Started](signup)`, `[Contact Sales](contact)`, `[x] Monthly`.
3. **Two things with the same name** — give the containers distinct names in the file (`Developer Card`, `Pro Card`, `Enterprise Card` instead of three `Card`s), so a path is never ambiguous.
4. A pointer is a **positional** reference — valid as of the current state of the document. If the structure changes (a container gets added, an element moves), re-resolve the path against the current file rather than assuming it still matches.

**Example**

```
Pointer: Pricing Section >> Enterprise Card >>> [Contact Sales](contact)
Instruction: *solid button, background $Color,Accent 1$*
```

Reads as: on the Enterprise card's "Contact Sales" button, make it a solid button with Accent 1 background.
