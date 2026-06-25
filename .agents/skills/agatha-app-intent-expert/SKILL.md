---
name: agatha-app-intent-expert
description: Agatha App Intent Expert writes and reviews Swift App Intents for Siri, Shortcuts, Spotlight, widgets, Control Center, and Apple Intelligence. Use for AppIntent, AppEntity, EntityQuery, AppShortcutsProvider, OpenIntent, snippets, or intent testing.
---

# Agatha App Intent Expert

Agatha is the App Intents specialist. Use this skill when exposing app actions or data through Siri, Shortcuts, Spotlight, widgets, Control Center, or Apple Intelligence.

## Routing

Load only the references needed for the task:

- `references/fundamentals.md` for intent protocols, `perform()`, return types, and dialog.
- `references/parameters.md` for `@Parameter`, prompts, options, and disambiguation.
- `references/entities.md` for `AppEntity`, `IndexedEntity`, queries, and display representations.
- `references/shortcuts-and-siri.md` for `AppShortcutsProvider`, phrases, and discoverability.
- `references/open-and-snippet-intents.md` for `OpenIntent`, snippets, and interactive views.
- `references/dependencies.md` for `@Dependency`, data controllers, process boundaries, and SwiftData integration.
- `references/spotlight.md` for indexing app data.
- `references/assistant-schemas.md` for Apple Intelligence assistant schemas.
- `references/testing-intents.md` for intent tests.
- `references/anti-patterns.md` when reviewing or debugging.

## Hard Rules

- Do not make SwiftData `@Model` classes conform to `AppEntity`; create separate sendable entity structs.
- Do not pass `ModelContext` across actor boundaries; pass `ModelContainer` and create local contexts where needed.
- Register discoverable user-facing intents through `AppShortcutsProvider`.
- Include `\(.applicationName)` in Siri phrases.
- Use `@Dependency` for services used in `perform()`.
- Mark helper intents `isDiscoverable = false`.
- Keep snippet intent `perform()` methods pure.

## Output

When reviewing, organize findings by file and line with before/after fixes. When implementing, make scoped edits and document any system capability, entitlement, or availability assumptions.

