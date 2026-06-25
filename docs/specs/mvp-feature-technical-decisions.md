# MVP Feature Technical Decisions

This document captures approved working decisions for turning the budget-first travel MVP scope into implementation-ready features and Linear tickets.

Primary product reference: [budget-travel-mvp-scope.md](budget-travel-mvp-scope.md)

## Status

Draft in progress. Only decisions that have been talked through and approved should be added here.

## Approved Direction

### Local-First, Remote-Ready Later

The MVP should be local-first. Remote storage, backup, account sync, sharing, and partner voting are desired future capabilities, but they should not add backend-specific complexity to the first model pass.

Do not add remote-specific fields yet, such as:

- `remoteRecordID`
- `syncStatus`
- `ownerUserID`
- `storageMode`

Keep the model portable enough that remote storage and cross-platform clients can be added later without a major rewrite.

### SwiftData As MVP Source Of Truth

Use SwiftData models as the MVP source of truth for persisted app data.

Do not introduce a separate DTO, domain, and persistence model split yet. That would create extra mapping and sync complexity before there is a backend or second platform that requires it.

Future schema generation should derive from the SwiftData models when needed. A later tool or script can reverse-generate YAML or JSON Schema from the SwiftData model declarations.

### Portable Model Design

Even though SwiftData is the MVP source of truth, models should use portable primitives where practical.

Guidelines:

- Use stable `String` IDs, likely UUID strings.
- Store money as minor units plus currency code, not floating-point dollars.
- Store enum-like fields in a way that can cleanly export to string values.
- Use neutral lifecycle fields from day one.
- Avoid Apple-only concepts in core data fields unless they are isolated behind iOS-specific implementation details.

Neutral lifecycle fields:

- `id: String`
- `createdAt: Date`
- `updatedAt: Date`
- `deletedAt: Date?`
- `schemaVersion: Int`

## Core Model Shape

The board is not a single trip search and should not impose one shared set of constraints across all trips.

The approved hierarchy is:

```text
TravelBoard
  contains many Trips

Trip
  contains one trip idea/search and owns its own constraints

TripCandidate
  contains one destination or option being evaluated for a Trip
```

### TravelBoard

A lightweight planning workspace that groups multiple trip ideas.

Examples:

- `2026 trip ideas`
- `Anniversary travel`
- `Warm winter options`

The board should contain broad organization fields, not budget/date/origin constraints.

Early fields:

- `id`
- `title`
- `notes`
- `createdAt`
- `updatedAt`
- `deletedAt`
- `schemaVersion`
- relationship: trips

### Trip

A specific trip idea or feasibility search inside a board.

Examples:

- `Warm 5-day trip under $900`
- `October food city trip`
- `Weekend from ATL`

Each trip owns its own planning constraints.

Likely fields:

- identity and lifecycle fields
- `boardID`
- `title`
- total budget
- currency code
- traveler count
- buffer percentage
- budget limit type
- trip length mode
- minimum nights
- maximum nights
- time flexibility mode
- exact or flexible date fields
- origin flexibility mode
- origin airport fields
- destination scope
- region preferences
- passport requirement preference
- travel style
- lodging style
- weather preference
- notes
- relationship: candidates

### TripCandidate

A destination or option being evaluated for a trip.

Examples:

- `Mexico City`
- `Chicago`
- `San Juan`

Each candidate owns destination-specific estimates and feasibility details.

Likely fields:

- identity and lifecycle fields
- `tripID`
- destination name
- destination region or country
- status, such as active, pinned, hidden, rejected, or verified
- flight cost estimate
- lodging cost estimate
- food cost estimate
- ground mobility cost estimate
- activity cost estimate
- fees and buffer estimate
- best time window label
- best departure airport
- budget fit
- transit feasibility
- car need verdict
- weather fit
- confidence level
- what makes this work
- what could break the budget
- notes

## Current Decision Summary

The working data model is:

```text
TravelBoard
- Organizes many trip ideas.
- Does not own shared trip constraints.

Trip
- Owns the budget, dates, length, origins, preferences, and other constraints for one trip idea.

TripCandidate
- Owns destination-specific costs, feasibility labels, verification state, and notes for one option inside a trip.
```

## Next Topics To Discuss

1. Exact `TravelBoard` fields.
2. Exact `Trip` constraint fields and enum values.
3. Exact `TripCandidate` cost model shape.
4. Whether `VerificationLink` should be a separate model in the first pass.
5. Whether `TripNote` should be a separate model or a simple text field in MVP.
6. How to represent cost ranges consistently.
7. What the first Linear tickets should be once the model is approved.
