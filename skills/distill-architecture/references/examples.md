# Examples

These examples show the workflow, not templates. Replace the names and claims with evidence from the target repository. The SVGs in this package are illustrative designs, not evidence about any real application.

## Whole-application preview

Imagine a small commerce application with web entry points, catalog and account features, an `OrderService`, inventory and payment adapters, an order store, and queued email notifications. The user asks, “Explain the app.” After the author checks the relevant sources, a useful whole-application preview could be:

```text
Small commerce application, from web entry points through catalog, accounts, checkout, and order notifications (make now)
├── Checkout and order state (possible next zoom)
├── Catalog browsing (possible next zoom)
├── Account management (possible next zoom)
└── Notification delivery (possible next zoom)

Diagrams: component view for the application's top-level boundaries and dependencies; sequence view for a checkout confirmation or rejection
Exclude: adapter internals and every route-specific variant
Uncertainty: whether payment completion is synchronous must be checked in the implementation
```

The component view covers the whole app's top-level parts. The sequence view teaches one representative checkout path without turning the overview into a tour of every route. If the code shows an asynchronous payment callback, use that observed timing in the sequence instead of assuming a synchronous reply.

## Lower-scope preview

Suppose the user chooses notification delivery as the next zoom in the same app. The author confirms that `NotificationDispatcher` queues accepted notices and a worker later calls `EmailHandler`. A preview for that narrower request could be:

```text
One notification from `NotificationDispatcher` through queue handoff to `EmailHandler` (make now)
├── Dispatcher admission policy (possible next zoom)
└── Email delivery and retries (possible next zoom)

Diagrams: sequence view for the asynchronous handoff and ordering; small structure view only if ownership is unclear
Exclude: handler internals and shutdown unless they affect this handoff
Uncertainty: queue admission behavior under concurrent producers
```

The lower view connects back to the whole-app component view at `NotificationDispatcher`. It does not pull every downstream branch into the same explanation.

## Focused structure and behavior

The [structure SVG](visuals/structure.svg) separates a service's reference to a payment contract from the concrete adapter that realizes it. `Cart` and `Order` appear as types used by the operation. The note makes clear that those type references do not prove lifecycle ownership. The view omits implementations and unrelated data fields.

The [behavior SVG](visuals/behavior.svg) traces one synchronous request, authorization, and two outcomes. Both outcomes appear because the failure branch changes whether the order is saved. Dashed arrows are replies; the diagram uses them for returned outcomes, not as a shorthand for asynchronous work.

## Outputs that miss the goal

- A recursive tree of every package, class, method, and sub-branch before the user selects a zoom. It spends effort on unapproved scope and gives no teaching sequence.
- One giant class diagram that mixes deployment, ownership, and call order. Split views by question so every arrow has one clear meaning.
- A polished sequence diagram based only on a design note when the code's actual order differs. Verify behavior in implementation and tests, or label the diagram as intended.
- A dashed message labeled “async,” a hollow triangle used for a call, or composition inferred from a stored reference. These alter UML meaning.
- A full GoF pattern inventory or prose that restates every box. Explain a pattern only where it solves a visible problem, and use prose for the reason or consequence the diagram cannot show.
- A diagram that hides a failure, lock boundary, queue handoff, or state commit that changes the result. Include the relevant edge or say what remains outside scope.
