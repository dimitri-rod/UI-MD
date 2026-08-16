# Why UI-MD is shaped this way

Four references. Each would change a decision if it had found the opposite.

---

Viscosity and diffuseness. Prose resists small changes, and costs a sentence per element. That's the whole brief. `[[Get Started]]` is three tokens; "add a button that says Get Started" is nine.

> Green, T.R.G. & Petre, M. (1996). Usability Analysis of Visual Programming Environments: A 'Cognitive Dimensions' Framework. *JVLC* 7(2), 131–174.

`*` local, `**` global. Bold is louder, louder reaches further. One character between "this button" and "the whole file" is textbook error-proneness, so the model reports every global rule it applied. Where a notation can't make an error visible, the tool around it should.

No third scope. Cross-file scope would let one file rewrite values other screens depend on — a hidden dependency, worse than a typo because it's invisible by design. `{Token}` reads upstream; nothing writes back. The ladder stops at the file, which is why `***rule***` reaches no further than `**rule**` rather than being an error: every Markdown entity gets a meaning, and the honest meaning of a third asterisk is that there was nowhere left to go.

Group syntax, borrowed — after borrowing the wrong thing first. The rule was never *don't group*; it was don't invent a shape for grouping. The first borrowing was Markdown's blank line: a rule bound to the run of lines above it, and the run ended at a blank. That failed in the field. Blank lines are cosmetic to every other tool, and a round-trip through a builder stripped one and silently changed what a rule bound to — the render survived, the file no longer meant what was written. A list is the shape Markdown already uses for *these belong together*, and it survives the trip because it is visible. So `- item` groups, a rule attaches to the single element above it, and no rule spans a run. The objection to inventing a shape stands; runs were the wrong borrowing. Same reason globals behave like a stylesheet, and `on hover` is a word rather than `:hover`.

> Blackwell, A.F. et al. (2001). [Cognitive Dimensions of Notations](https://www.cl.cam.ac.uk/~afb21/publications/CT2001.pdf). *Cognitive Technology 2001*, LNCS 2117, 325–341.

Parens, not angle brackets. `<Label>` was HTML. Markdown passes inline HTML straight through, so one builder rendered the literal characters and another rendered an empty unknown element; `<>` is JSX fragment shorthand and renders nothing by design. Two tools, two different wrong answers, one collision — a primitive that renders differently per parser isn't one. Parentheses are inert in HTML, JSX and Markdown, and pill-shaped besides. This is the only decision here that was found by testing rather than argued. The lesson was about inventing shapes out of angle brackets, not about angle brackets: `<https://acme.com>` is Markdown's own autolink, every renderer knows it, and it means what it has always meant.

Names are the product. EDIT-Bench: 540 real edit instructions, only 1 of 40 models above 60%, and context alone swings success 11 points. Assistants never parse "the second button" — the editor hands them the cursor. A designer in a chat box has no cursor. A name is the cheapest substitute.

> [EDIT-Bench: Evaluating LLM Abilities to Perform Real-World Instructed Code Edits](https://arxiv.org/abs/2511.04486) (2025). arXiv:2511.04486.

One page, handed over whole. Models infer a grammar badly from examples and well from the grammar itself — minimally sufficient, not complete. Hence the dictionary is one page, handed over entire. The README argues and the dictionary defines; the syntax appears in exactly one of them, because the first time it appeared in two they drifted apart within a week.

> Wang, B. et al. (2023). [Grammar Prompting for Domain-Specific Language Generation with LLMs](https://arxiv.org/abs/2305.19234). *NeurIPS 2023*. arXiv:2305.19234.

---

The references above show the pain is real; they aren't what justifies the format. That came from use — dozens of runs with Claude across the project, 97% accurate.

The risk: if the hierarchy can be exported from a design file, nobody needs to write one by hand.
