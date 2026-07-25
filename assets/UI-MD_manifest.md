# UI-MD_manifest.md

**Title:** UI-MD Core Manifest
**Version:** 3.0
**Date:** 2026-07-25

**Premise:** English is a poor medium for spatial reasoning. Traditional UI code (React, HTML) is too token-dense for rapid conceptual wireframing. Describing which layer a component belongs in, or that one specific button needs a different font, takes a paragraph — and a model still guesses wrong.

**Solution:** UI-MD. A stupidly simple, fixed dictionary of symbols — not a Markdown dialect — that lets a designer describe a screen precisely, and lets a machine read it back the same way every time.

**Principles:**
1. **The LLM is the Compiler:** There is no Abstract Syntax Tree, lexical analyzer, or middleware. The system prompt is the engine.
2. **Shape is Function:** brackets define primitives — `[Label]` a button, `[Label](url)` a link, `[x]`/`[ ]` a checkbox, `<x>`/`<>` a radio.
3. **Depth is Architecture:** nesting is defined visually by `>`, `>>`, `>>>`. Maximum depth is 3 levels, to force composition over sprawl.
4. **Default to System:** `$Token$` pulls an exact value from whatever design system is connected, instead of a guess.
5. **Zero Boilerplate:** a `*rule*` can be plain English or precise CSS-ish terms — both compile the same way. A `// note` carries context without ever rendering.
