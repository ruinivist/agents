# UML and visual style

Use standard UML to make the architecture teachable and easy to redraw. SVG is the default editable format. Use the diagram that answers the question: class for types and relationships, sequence for calls and events in order, component for software boundaries and interfaces, deployment for runtime placement. These forms are not interchangeable. Do not substitute Mermaid unless requested.

Open and inspect the bundled [structure example](visuals/structure.svg) and [behavior example](visuals/behavior.svg) before planning diagrams. Use the class and sequence examples as visual-style references for those diagram types. No component or deployment SVG is bundled; adapt the notation and visual rules below for those views without implying or inventing another exemplar.

## Choose and scope the view

- A class view can show selected attributes, operations, visibility, types, and relationships. Omit irrelevant members. Repeat a type across diagrams when a responsibility grows.
- Use an association when a reference or structural relationship matters. A dashed dependency arrow points from user to supplier. An operation's parameter or return type may already express a dependency; avoid duplicating every type edge when it adds no teaching value.
- Use a filled composition diamond only when the whole owns the part's lifecycle. A reference by itself does not establish composition. Shared aggregation has model-dependent meaning; prefer a plain association unless the stronger meaning is supported.
- An inheritance or interface-realization hollow triangle points to the parent or interface. A composition diamond touches the owner. Keep both shapes visibly distinct from an open message arrow.
- Show multiplicities when they clarify cardinality. Use `1`, `0..1`, `0..*`, and `1..*` accurately. Mark visibility and `{readOnly}` when they matter to the design.
- A sequence diagram runs downward in time. Use participant lifelines and show only the calls needed to explain the chosen path. A solid line with a filled head is a synchronous call; a solid line with an open head is asynchronous. A dashed line is a reply, with an open or filled head. Dashed does not mean asynchronous.
- Show meaningful alternatives, failure exits, lock boundaries, and ordering where they change behavior. Use a compact `alt` fragment or a second focused view when needed. Do not turn one diagram into a dump of every branch.
- A component diagram uses component rectangles, circles for provided interfaces, sockets for required interfaces, and small boundary squares for ports. A dashed dependency indicates use, not sync or async timing.
- A deployment diagram shows runtime placement: nodes represent devices or execution environments, and artifacts show deployed software. Components describe logical software boundaries, not runtime nodes. Placement and communication paths do not establish call order or sync/async timing.

## Visual treatment

Use a white canvas, white boxes, black text and connectors, square corners, and `DejaVu Sans, sans-serif`. Avoid gradients, shadows, decorative icons, and broad color fills. At about 1500 units wide, use roughly 31-unit bold titles, 25-unit bold type names, 20-unit members and labels, and 18–19-unit multiplicities. Scale type sizes consistently for other canvases.

Center the title and a compact color key when color helps. Center type names; left-align members with generous padding and row spacing. Use roughly 2-unit outlines and connectors. Route connectors through whitespace, keep labels clear of lines and arrowheads, and size boxes for their text instead of shrinking type. Use visible dashes, such as `9 7`, for dashed relationships. Folded-corner notes can carry a short fact that cannot be encoded clearly in the diagram; attach them with a dashed line.

Use color only as a reading aid, never as UML meaning. Color names or a small accent, while keeping arrows and symbols black:

| Color | Use | Example |
| --- | --- | --- |
| Blue | Logic and concrete services | `#1856a6` |
| Green | Data and state | `#18713a` |
| Purple | Contracts and abstract types | `#7435a0` |
| Orange | Messaging and queued work | `#b36313` |
| Red | Failures or unresolved questions | `#a12d2d` |

Make the diagram readable in grayscale and do not rely on color alone to communicate status or type.

## SVG and validation

Make the SVG editable, self-contained, and accessible. Include the SVG namespace, a fitting `viewBox`, a `<title>` with a unique `id`, `role="img"`, and `aria-labelledby` referencing that title. A short `<desc>` can add context when the title is not enough. Escape XML text. Give every ID a unique value within the file and resolve every marker, fragment, and local reference to an element in that SVG. Avoid external fonts, images, stylesheets, or script dependencies.

Before delivery:

1. Parse each SVG as XML. Check unique IDs and every local `marker`, `href`, and `aria-labelledby` reference.
2. Check Markdown links and image paths relative to their files.
3. Compare labels, relationships, direction, call order, and outcomes with the approved scope and source evidence.
4. Render the actual SVG and inspect it at useful size for clipping, overlaps, unreadable text, accidental crossings, and connector endpoints.

If no renderer is available, report that rendering and visual inspection remain incomplete. Do not call a diagram visually verified based only on its XML or source text.
