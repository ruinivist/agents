# Distillation workflow

## Roles and sequence

The lead extracts the user's intent and constraints, delegates reconnaissance and reference reading to the author, and owns scope and architecture decisions, approval, evidence-backed escalations, and final integration checks. The lead does not repeat the author's reconnaissance, reference reading, or research, reread all finished prose, or rerun rendered checks assigned to workers.

```text
lead --intent/constraints--> author
author --preview; pause--> lead --presents--> user
user approval/waiver --> author (reuse only if allowed; otherwise fresh)
author --> editor (separate session) --> fresh reviewer --> lead
lead --one correction batch if needed--> author/editor --> lead
lead --integration checks--> handoff
```

Keep handoffs compact: include paths, scope, evidence anchors, constraints, and checks. Do not pass whole conversations or files when anchors suffice. Limit stages by pass count, not elapsed time. Artifact owners work in sequence; do not assign overlapping prose and diagram work or create overlapping worktrees.

### Author

The author reads applicable repository instructions, the relevant design specification and its Behavior sections when present, implementation and tests, nearby notes, and every package reference. The author opens and inspects the bundled SVG exemplars, then identifies scope boundaries, state ownership, a representative flow, and evidence anchors. This reconnaissance should support a preview, not exhaustive branch research.

Use implementation and tests to verify current behavior. A design note or specification can establish documented intent, but cannot prove that code follows it. If no complete note exists, code-grounded work can continue. If there is no implementation, explain documented design as intended and label genuinely new suggestions as proposed; do not invent implementation behavior or force a new design. If neither implementation nor documented design exists, ask for source material or explicit direction to create a proposal. Resolve material conflicts before presenting claims as facts; escalate conflicts that cannot be resolved from available evidence.

Keep evidence anchors useful if context is shortened: repository-relative paths, class or function names, and line or section references where they help locate a claim. Put anchors in prose or a short source note, not on every diagram label.

Before writing any artifact, send a preview with one root labeled `(make now)` and only its immediate meaningful children labeled `(possible next zoom)`, joined with tree connectors. Name each planned diagram and its teaching purpose, exclusions, and uncertainties or proposed details. This is a preview, not a full hierarchy unless the user specifically asked for one. The author pauses; the lead presents the preview and obtains approval unless the user explicitly waived approval or already approved this exact scope. A broad request is not approval for every possible subtopic.

If investigation changes the preview materially, stop and send a revised preview for approval before expanding. After approval, reuse the author only when applicable warm-session rules allow; otherwise the lead gives a fresh author a compact handoff. Do not promise worker reuse. The author continues investigating the approved scope and writes its complete Markdown and linked SVGs together. No other worker owns prose or diagrams in parallel. Teach in responsibility-led steps where useful; separate structure from behavior when that makes the model clearer. Prefer focused, editable SVGs over Mermaid unless the user asks otherwise.

Preserve what sources show about ownership, state changes, synchronous and asynchronous work, failures, ordering, and important concurrency. Include failure paths, locks, retries, queues, or async handoffs when they change the result or explain ownership. Separate observed behavior from intended or proposed behavior in diagrams and prose. Do not imply that a draft design is implemented, silently choose between contradictory sources, or infer behavior from a diagram or design note alone.

The selected view is the finish line: where useful, explain how it connects to the surrounding system. If the user selected a complete leaf, cover its approved details here without adding next-zoom branches or deferred details; stop once the selected question is answered. Do not add a pattern catalog or unrelated redesign.

The author checks source agreement, relative Markdown links and anchors, SVG XML, unique IDs and local references, and renders and actually inspects each diagram. Follow [UML and visual style](uml-and-visual-style.md) for notation and validation. Report any unavailable rendering or incomplete visual inspection; never claim an unchecked diagram was visually verified.

### Editor

After the author finishes, a separate editor worker session is mandatory. It edits the entire finished prose, captions, and diagram labels using the self-contained rules in [writing guidance](writing.md). The editor changes the artifacts directly, preserving supported facts, qualifiers, event order, technical identifiers, links, and approved scope. The editor does not repeat full research or expand scope. Flag material factual uncertainty for the lead instead of guessing. If labels or layout change, rerun affected link, source, XML/reference, render, and visual checks.

### Reviewer

A fresh reviewer is mandatory for one read-only pass over the completed prose and rendered SVGs. Check source accuracy against the author's evidence anchors, completeness within approved scope, consistency between diagrams and prose, actual visual readability, UML notation, and clear violations of the writing rules. Return one batch of concrete, actionable defects only. Each finding names a path and location, cites evidence or the violated rule, and gives the smallest correction. Do not report preferences, optional improvements, alternative styles, or general rewrite requests.

### Lead triage and finite correction

If the review is clean, the lead checks integration diff, repository status, and worker reports, then communicates the result; ordinary documentation does not require the lead to reread all artifacts. If findings exist, the lead triages evidence, rejects preference-only requests, and directs the author or editor to one bounded correction batch on the same slice. Reuse a worker only when applicable warm-session rules allow; otherwise give a fresh worker a compact handoff. The correcting worker verifies fixes and affected links, facts, and renders.

There is no automatic second review. Re-review only if a correction materially changes a security or data-loss boundary. If a defect remains unresolved after the one correction batch, the lead decides or asks the user for clarification; never loop automatically or silently declare completion.

### Optional scout and escalation

A scout is optional; use one only for a specific unresolved standards or source question. It returns evidence and uncertainties without editing artifacts; the lead does not default to research. Stop and escalate material scope changes, unsupported claims, or factual conflicts that cannot be resolved. The lead reads only the evidence needed to decide, not a duplicate of the full work.

## Output boundary

Write Markdown and linked SVGs in `docs/arch/` relative to the target repository root, creating the folder only after scope approval. Use another location only when the user or applicable repository instructions explicitly require it. Follow local filename conventions and relative links. Leave unrelated files and diagrams untouched; update an existing diagram only when it is within approved scope, preserving unrelated edits. Do not change source code unless requested.
