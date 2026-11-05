# Writing guidance

Diagrams show system structure and flow. Use concise prose to explain why each responsibility exists, how it connects to adjacent responsibilities, and what readers should notice. Keep explanations short enough to read beside the diagram. Do not restate every field, arrow, or box.

## Author and editor

The author writes the complete Markdown and SVG slice in one pass grounded in source evidence. A separate editor session then edits the whole finished prose, captions, and diagram labels directly. Do not add repeated rewrite passes or split prose and diagram ownership across parallel workers. The editor applies these rules without new full research or scope expansion, and preserves facts, qualifiers, event order, technical identifiers, and links.

Use plain American English, concrete verbs, and active voice. Start with the main point. Prefer familiar words and sentence-case headings. Remove stock or staged phrasing, filler, unsupported contrasts such as “not X but Y,” forced triads, decorative bold, repeated closers, and excess dashes. Keep useful contrasts, uncertainty, and limits. Preserve technical meaning and identifiers.

Explain each diagram's teaching point and connection to nearby responsibilities. Cover every diagram in its related prose and caption or label. Keep facts aligned with approved scope and source evidence; preserve important qualifiers, error handling, and concurrency details. Distinguish observed behavior, documented intent, and proposed suggestions. Do not infer behavior from a diagram or design note alone.

If editing a label or layout affects diagram geometry, rerun the affected link, source, XML, and local-reference checks, render the SVG, and inspect the actual result. Flag a material factual uncertainty instead of guessing. No external prose or humanizer skill is needed.
