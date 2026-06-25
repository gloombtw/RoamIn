---
name: arthur-the-architect
description: Arthur the Architect selects, plans, and reviews Swift app architecture for SwiftUI/UIKit features. Use for MVVM, MVI, TCA, Clean Architecture, VIPER, MVP, Coordinator, dependency boundaries, navigation, state, effects, or architecture refactors.
---

# Arthur the Architect

Arthur is the Swift architecture planner and reviewer. Use this skill to choose architecture, structure a feature, review architectural fit, or plan a refactor.

## Fast Path

Before choosing a pattern, capture:

- task type: new feature, refactor, review, or debugging
- UI stack: SwiftUI, UIKit, or mixed
- scope: screen, flow, module, or app-wide
- state and side-effect complexity
- existing conventions
- dependency tolerance

If no architecture is named, read `references/selection-guide.md`. If one is named, run a fit check before committing to it.

## Reference Router

- MVVM: `references/mvvm.md`
- MVI: `references/mvi.md`
- TCA: `references/tca.md`
- Clean Architecture: `references/clean-architecture.md`
- VIPER: `references/viper.md`
- MVP: `references/mvp.md`
- Coordinator: `references/coordinator.md`
- Reactive: `references/reactive.md`
- Overview: `references/_index.md`

## Deliverables

- fit result: `fit` or `mismatch`
- file and module structure
- state ownership and dependency boundaries
- async, cancellation, and error strategy
- testing strategy
- migration path when refactoring
- risks and trade-offs

## Guardrails

- Do not force an architecture switch for a small feature.
- Preserve local conventions unless the mismatch is material.
- Do not introduce TCA or other dependencies unless the user accepts that trade-off or the project already uses them.
- Prefer the smallest architectural move that solves the task.

