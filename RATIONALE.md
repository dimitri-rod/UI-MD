# Why UI-MD is shaped this way

Four references. Each would change a decision if it had found the opposite.

---

**Viscosity and diffuseness.** Prose resists small changes, and costs a sentence per element. That's the whole brief. `[[Get Started]]` is three tokens; "add a button that says Get Started" is nine.

> Green, T.R.G. & Petre, M. (1996). Usability Analysis of Visual Programming Environments: A 'Cognitive Dimensions' Framework. *JVLC* 7(2), 131–174.

**`*` local, `**` global.** Bold is louder, louder reaches further. One character between "this button" and "the whole file" is textbook error-proneness, so the model reports every global rule it applied. Where a notation can't make an error visible, the tool around it should.

**No `***`.** Cross-file scope would let one file rewrite values other screens depend on — a hidden dependency, worse than a typo because it's invisible by design. `$Token$` reads upstream; nothing writes back. The ladder stops at the file.

**No group syntax.** A blank line already separates blocks in Markdown. Borrowing that costs nothing; inventing a parallel shape costs a rule and a new way to be wrong. Same reason `Global` behaves like a stylesheet, and `on hover` is a word rather than `:hover`.

> Blackwell, A.F. et al. (2001). [Cognitive Dimensions of Notations](https://www.cl.cam.ac.uk/~afb21/publications/CT2001.pdf). *Cognitive Technology 2001*, LNCS 2117, 325–341.

**Names are the product.** EDIT-Bench: 540 real edit instructions, only 1 of 40 models above 60%, and context alone swings success 11 points. Assistants never parse "the second button" — the editor hands them the cursor. A designer in a chat box has no cursor. A name is the cheapest substitute.

> [EDIT-Bench: Evaluating LLM Abilities to Perform Real-World Instructed Code Edits](https://arxiv.org/abs/2511.04486) (2025). arXiv:2511.04486.

**One page, handed over whole.** Models infer a grammar badly from examples and well from the grammar itself — minimally sufficient, not complete. Hence the README *is* the spec, and the separate model-facing file was deleted.

> Wang, B. et al. (2023). [Grammar Prompting for Domain-Specific Language Generation with LLMs](https://arxiv.org/abs/2305.19234). *NeurIPS 2023*. arXiv:2305.19234.

---

**None of this tested UI-MD.** It shows the pain is real. The test would be one screen three ways — prose, UI-MD, and an outline the model writes itself — ten edits each, counting first-try hits. Until then the case is argued, not measured.

**The risk:** if the hierarchy can be exported from a design file, nobody needs to write one by hand.
