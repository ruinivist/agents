---
name: distill-architecture
description: Create a visual-first, source-grounded architecture explanation at a suitable zoom, using focused UML SVGs and concise teaching prose.
---

# Distill architecture

Help a reader understand and reconstruct an application's design through focused visuals and short explanations. Recommend a useful scope from the user's intent, or honor an explicit one. A scope may be a whole application, subsystem, component, or one mechanism; these are examples, not fixed levels.

## Dispatch and ownership

The lead extracts the user's intent and constraints, then delegates reconnaissance and reference reading to `worker(author)`. The lead leaves repository and reference reading and source research to the author. It does not reread the complete artifacts or rerun the author's rendered-diagram checks. The author reads applicable repository instructions and relevant references, gathers enough source evidence to propose a scope, and sends a preview before writing artifacts. The author pauses while the lead presents the preview and obtains approval unless the user explicitly waived approval or already approved the exact scope.

After approval, continue with the same author only when applicable warm-session rules allow; otherwise send a fresh author a compact handoff. Do not promise worker reuse. The author owns the complete Markdown and SVG slice, its source checks, and diagram rendering and inspection. Do not split prose and diagram ownership across parallel workers.

Use a separate `worker(editor)` session to edit all finished prose, captions, and diagram labels with the embedded guidance in [writing guidance](references/writing.md). Then use a fresh `reviewer` for one read-only pass over the finished prose and rendered SVGs. The lead triages concrete findings and, if needed, directs one bounded correction batch. The lead checks the integration diff, repository status, and worker reports, then communicates the result; the lead does not independently reread the complete artifacts.

## References and boundaries

Follow the staged roles, approval gate, correction limit, and escalation rules in [distillation workflow](references/distillation.md). Use [UML and visual style](references/uml-and-visual-style.md) for notation and validation, [writing guidance](references/writing.md) for the author and editor, and [examples](references/examples.md) when useful. These references are self-contained; no external writing or humanizer skill is required.

Write all outputs in `docs/arch/` relative to the target repository root unless the user or applicable repository instructions explicitly require another location. Preserve observed, intended, and proposed distinctions and source-supported failure, order, and concurrency details. Do not redesign the system, edit unrelated source, or continue into another zoom after the selected question is answered. A material scope change or unresolved factual conflict goes to the lead for an evidence-backed decision; do not guess.
