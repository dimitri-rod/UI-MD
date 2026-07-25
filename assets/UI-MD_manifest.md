# UI-MD_manifest.md

**Title:** UI-MD Core Manifest
**Version:** 2.4
**Date:** 2026-07-25

**Premise:** English is a poor medium for spatial reasoning. Traditional UI code (React, HTML) is too token-dense for rapid conceptual wireframing. Emmet and JSX require structural boilerplates that impede the speed of thought.

**Solution:** UI-MD. A markdown-native Domain Specific Language (DSL) engineered strictly for transformer reasoning. 

**Principles:**
1. **The LLM is the Compiler:** There is no Abstract Syntax Tree (AST), lexical analyzer, or middleware. The system prompt is the engine. UI-MD structures the latent space directly.
2. **Shape is Function:** ASCII boundaries define primitives (e.g., `[ ]` for buttons, `( )` for inputs).
3. **Indentation is Architecture:** Depth is defined visually by carets (`>`). Maximum depth is 3 levels to enforce component modularity and prevent the "Textarea Tab Trap".
4. **Default to System:** Primitives inherit design system tokens automatically. Modifications require explicit local modifiers (`* rule *`).
5. **Zero Boilerplate:** Data binding (`'var'`), state interactions (`* On click: action *`), and loops (`... 'list'`) use minimal syntax to conserve context windows.