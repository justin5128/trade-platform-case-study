# From a product problem to a verifiable change

[Flagship overview](../README.md) · [Project index](project-index.md)

My product contribution spans requirements, workflow design, architecture choices, AI-assisted implementation, failure diagnosis and iteration. This document turns that approach into a reviewable example. The scenario is synthetic; the underlying concerns are grounded in recorded portal and workflow work.

## Start with the user consequence

A reviewer requests an update for Cedar Labs, then switches to Harbor Works. The earlier request completes. If its result appears in the newly selected workspace, the interface may look healthy while showing the wrong context.

The product problem is loss of trust in the relationship between a user's selection and the information displayed. A faster request alone would not resolve that problem.

## Translate the problem into a decision

| Choice | Benefit | Cost or limitation | Product direction |
| --- | --- | --- | --- |
| Freeze navigation until work finishes | Simple interaction sequence | Interrupts review and makes dependency delays the user's burden | Reserve blocking for actions that truly require it |
| Allow navigation and accept every response | Responsive appearance | An old result can replace current context | Insufficient correctness |
| Allow navigation with item-specific reconciliation | Preserves review flow and result ownership | Requires explicit state and delayed-response checks | Preferred public design |

The requirement becomes observable: completion for one item can update that item's activity, but cannot replace another item's active view. Pending feedback is provisional; backend-owned results remain authoritative.

## Prioritize by consequence and dependency

This is an illustrative prioritization brief, not a historical roadmap or a numerically scored exercise.

| Sequence | Investment | Why it earns its place | Exit evidence |
| --- | --- | --- | --- |
| First | Correct selection and workflow state | Other features depend on users trusting what they see | Delayed and out-of-order scenarios preserve identity |
| Next | Clear freshness and recovery feedback | Makes external dependency failures understandable | A user can explain which data is current and what is pending |
| Then | Mobile task continuity | Extends a coherent workflow to constrained screens | Narrow-screen review preserves context and required controls |
| Explore | Continuous data delivery and service separation | Adds operating complexity and should address an observed need | Measured demand, ownership and recovery plan justify the change |

**Scope cut:** a live-data migration is outside a selected-item correctness fix. Combining them would make it harder to determine which change repaired or broke the workflow.

## Work with engineering and AI

I define the expected user-visible sequence and the owner of each responsibility before asking for implementation. AI can assist with tracing behavior, drafting a bounded change and proposing checks. I remain responsible for scope, evidence interpretation and whether the change meets the product intent.

The development record includes repeated reconciliation work, chart interaction fixes, comment synchronization and reversions. Those are evidence of an iterative process, not a claim that every runtime path is resolved. A reverted change is useful evidence when it exposes an incomplete understanding of ownership.

## Validate the behavior that matters

| Synthetic scenario | Required observation | Why a superficial check misses it |
| --- | --- | --- |
| Switch items during an update | Current selection stays stable when the earlier result arrives | A single-item happy path never changes context |
| Receive responses out of order | Older work cannot replace newer state | Fast local responses hide ordering problems |
| Update fails while a valid view exists | Previous view remains labeled; failure is visible | A blank replacement can erase useful context |
| Open and close an expanded chart | Selection and focus return predictably | Seeing the chart once says little about return behavior |
| Revisit a completed item | Completion remains consistent across relevant views | A toast can disappear while the underlying view stays stale |

These are a proposed public validation set. They do not represent a completed production test report.

## Define success before inventing targets

For a future evaluation, record the number of attempted synthetic scenarios, failures by scenario, unresolved work at the end of each run, and user interpretations of pending versus complete. Capture observed completion times with their starting and ending events so comparisons have consistent meaning.

Set targets after collecting a baseline. Pair speed with correctness: shorter waiting time is not a product win if the wrong item updates. Pair task completion with comprehension: a completed action is not enough if the user cannot tell what happened.

## Release and revisit

For a bounded change, identify affected views, confirm the authoritative owner, exercise failure scenarios and preserve a recovery path. Expand scope when new evidence justifies it. A future infrastructure migration should prove equivalence at one responsibility boundary before taking on another.

**What this demonstrates:** product judgment becomes concrete through scope, trade-offs, acceptance behavior and evidence. The technical detail serves the user's ability to trust and operate the product.

---

© Justin Joseph. Portfolio documentation. Production implementation and proprietary methods are not included.
