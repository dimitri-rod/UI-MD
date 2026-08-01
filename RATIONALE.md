# Why UI-MD is shaped this way

Four references. Each is here because a design decision would change if the paper had found the opposite.

---

## The problem has a name

Green & Petre call it **viscosity** — a notation's resistance to small local changes — and **diffuseness** — how many symbols a meaning costs. Prose scores badly on both for UI work: every change means a full re-description, and every element costs a sentence. Those two dimensions are the entire design brief.

Diffuseness is also the answer to "why not just write it out?" `[[Get Started]]` is three tokens. "Add a button that says Get Started" is nine, for the same meaning. Over sixty nodes that decides whether the file is scannable.

> Green, T.R.G. & Petre, M. (1996). Usability Analysis of Visual Programming Environments: A 'Cognitive Dimensions' Framework. *Journal of Visual Languages and Computing*, 7(2), 131–174.

## What follows from it

**Scope marks.** One asterisk local, two global — bold is louder, louder reaches further. The framework also names **error-proneness**, and a one-character gap between "this button" and "the entire file" is a textbook case: both render as emphasis, so the typo is invisible on the page and invisible in the source. Spelling out a `Global` keyword was rejected — scope markers are typed constantly, and terseness counts too. The risk is handled outside the notation instead: the model lists every global rule it applied. Where a notation can't make an error visible, the tool around it should.

**No third scope.** `***bold italic***` is available and means nothing here. The obvious candidate was cross-file scope, the next rung on a ladder where louder means wider. It points the wrong way: `$Token$` connects a file to the design system by **reading** — design system upstream, screens downstream — and a cross-file rule would **write** back, letting one file change values used by screens you haven't opened. That's a **hidden dependency**, worse than the typo risk because it's invisible by design rather than by accident. So the ladder stops at the file, and everything you can affect is everything you can see by scrolling. When a notation has an obvious empty slot, ask what would fill it and whether that thing should exist. Empty slots are cheaper than wrong ones.

**No group syntax.** A modifier takes the run of lines above it, ending at a blank line, another modifier, or a shallower container — three sibling links share one rule by sitting together. A dedicated grouping shape was rejected on **consistency**: a blank line already separates blocks in Markdown, and every parser and every model treats it that way. Borrowing a convention the reader has costs nothing; inventing a parallel one costs a shape, a rule, and a new way to be wrong. Same reasoning throughout — `Global` is a stylesheet and node modifiers are inline styles because that is CSS's cascade, and `on hover` and `on mobile` are words rather than `:hover` and `@media` because words are what a designer says out loud.

> Blackwell, A.F. et al. (2001). [Cognitive Dimensions of Notations: Design Tools for Cognitive Technology](https://www.cl.cam.ac.uk/~afb21/publications/CT2001.pdf). *Cognitive Technology 2001*, LNCS 2117, 325–341.

## Why naming things is the whole product

The load-bearing evidence. EDIT-Bench collected 540 real edit instructions in the wild and found them brief and often ambiguous — actionable only in combination with code context, the highlighted region, and cursor position. Across 40 models, **only one scored above 60%**; varying how much context the model received moved success rates by **up to 11 percentage points**.

Coding assistants never parse "the second button." The editor hands them the selection, and that hand-off is worth double digits. A designer working in a chat box has no cursor. A name is the cheapest substitute for one.

> [EDIT-Bench: Evaluating LLM Abilities to Perform Real-World Instructed Code Edits](https://arxiv.org/abs/2511.04486) (2025). arXiv:2511.04486.

## Why there is one page, handed over whole

LLMs generalise poorly to a structured language from examples alone, and improve substantially when handed the grammar up front — and a **minimally sufficient** grammar, a subset rather than the full specification, works best.

So: hand the model the rules rather than hoping it infers them, and keep them small enough to state once. This is also why the README *is* the spec. A separate model-facing file was tried and deleted — two documents describing one grammar drift, and the duplicated half is dead weight in both.

> Wang, B. et al. (2023). [Grammar Prompting for Domain-Specific Language Generation with Large Language Models](https://arxiv.org/abs/2305.19234). *NeurIPS 2023*. arXiv:2305.19234.

---

## What none of this shows

No study here examined UI-MD. They establish that the pain is real, named, and unsolved. They say nothing about whether this notation is the right answer. That would take one experiment: the same screen written three ways — prose, UI-MD, and a numbered outline the model emits itself — then ten edits against each, counting how many land on the first try without re-description. Until that runs, the case is argued, not measured.

And the clearest risk is in none of them: **if the hierarchy can be exported from a design file, nobody needs to hand-write one.** The case for UI-MD rests on the human wanting to author and read that structure, not on the model benefiting from it.
