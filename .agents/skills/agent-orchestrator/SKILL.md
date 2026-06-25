---
name: agent-orchestrator
description: Use for project-agnostic feature planning, implementation, review, testing, decomposition, research, specialist delegation, challenge gates, or multi-agent Codex CLI workflows.
---

# Agent Orchestrator

Use this skill to run the repository workflow inside Codex. Do not invoke `tools/agent_pipeline` or any external Python harness. Codex is the orchestrator, and agent roles are operating modes, subagents, or focused passes within the Codex CLI session.

## Entry Points

- Explicit: the user invokes `$agent-orchestrator` or asks to use the orchestrator, agent pipeline, or multi-agent workflow.
- Implicit: the user asks for complex feature work that benefits from decomposition, architecture, challenge, implementation, review, and tests.

## Orchestrator Rules

- The main Codex thread is the orchestrator.
- Start from a task file in `docs/tasks` when one exists. If none exists and the work is non-trivial, create one from `docs/tasks/template.md`.
- Send only relevant context to each role. Include the task, relevant code paths, prior handoff, and constraints.
- When a role needs specialist expertise, invoke or explicitly reference the named Codex skill from the Specialist Roster below instead of re-embedding that specialist's full instructions here.
- Every agent handoff must pass through Charlie before the orchestrator accepts it, unless the task is tiny and the user explicitly asks to skip challenge gates.
- Prefer Codex subagents for read-heavy or critique-heavy parallel work when the user explicitly asks for subagents or parallel agents.
- Keep write-heavy implementation coordinated in the main thread unless a subagent has a clearly isolated write scope.
- Create or update handoff notes in `docs/runs/<date>-<task-slug>/` for large tasks. For small tasks, a final response is enough.
- Challenger passes must probe for flaws. They should not rubber-stamp plans or code.

## Specialist Roster

Use these named agents whenever the plan calls for their domain. Mention the skill handle in the plan or handoff so the next Codex turn can invoke it directly.

| Agent | Skill Handle | Use When |
| --- | --- | --- |
| Daryl the Decomposer | `$daryl-the-decomposer` | First-pass decomposition, task slicing, dependency ordering, specialist delegation |
| Rory the Researcher | `$rory-the-researcher` | Current guidance, common implementation patterns, tradeoffs, examples, source-backed discovery |
| Charlie the Challenger | `$charlie-the-challenger` | Challenge every handoff for SOLID, DRY, KISS, YAGNI, modularity, portability, coupling, cohesion, testability, maintainability |
| Terry the Tester | `$terry-the-tester` | Swift Testing, unit/integration tests, async tests, flakiness, XCTest migration |
| Agatha App Intent Expert | `$agatha-app-intent-expert` | App Intents, Siri, Shortcuts, Spotlight, widgets, Control Center, Apple Intelligence |
| Arthur the Architect | `$arthur-the-architect` | Swift app architecture, module boundaries, MVVM/MVI/TCA/Clean Architecture/Coordinator decisions |
| Connie the Concurrency Expert | `$connie-the-concurrency-expert` | async/await, actors, strict concurrency, Sendable, cancellation, continuations, AsyncStream |
| Dorthy Swift Data Expert | `$dorthy-swift-data-expert` | SwiftData models, relationships, predicates, queries, migrations, CloudKit, persistence tests |
| Sandy SwiftUI Expert | `$sandy-swiftui-expert` | SwiftUI screens, navigation, state flow, accessibility, performance, UI refactors |
| Darian API Design Expert | `$darian-api-design-expert` | Swift API naming, argument labels, call-site fluency, documentation comments, interface review |
| Fiora Figma Handler | `$fiora-figma-handler` | Figma-to-SwiftUI, design tokens, asset export, visual fidelity, adapting screens to Figma |

## Dispatch Rules

- The first named agent in the pipeline is Daryl. Daryl decides whether Rory is needed before producing a decomposition.
- Rory returns research to Daryl, not a final implementation plan. Daryl owns task slicing and delegation back to the orchestrator.
- Charlie gates every returned handoff before the orchestrator proceeds. If Charlie returns `Revise`, send the handoff back to the prior agent with Charlie's required changes.
- Charlie may return `Accept`, `Accept with notes`, `Revise`, or `Escalate`; only `Accept` and `Accept with notes` move forward without another agent pass.
- Architecture role defaults to Arthur. Add Dorthy, Sandy, Connie, Darian, Agatha, or Fiora when the architecture touches their domain.
- Engineering role should invoke the most relevant implementation specialist rather than acting generically when the work is primarily SwiftUI, SwiftData, App Intents, concurrency, API design, or Figma translation.
- Review role can run specialist reviews in parallel when the user asks for subagents or when risks are independent.
- Testing role defaults to Terry for Swift unit/integration tests and adds Connie for async/concurrency tests or Dorthy for persistence behavior.
- Challenger role should name which specialist assumptions it is challenging, for example "Challenge Sandy's navigation plan" or "Challenge Dorthy's delete-rule model."
- If a task spans multiple specialists, sequence them by dependency: Arthur first for boundaries, domain specialists next for implementation details, Terry near the end for tests, then integration.

## Default Role Sequence

1. **Daryl the Decomposer**
   - Break a complex request into deliverable pieces.
   - Identify dependencies, unknowns, risks, and likely write scopes.
   - Output a minimal task sequence.
   - Use Daryl first. Daryl invokes Rory when research or clarification is needed.

2. **Architect Agent**
   - Turn the decomposition into a feature plan and code structure.
   - Define data models, service boundaries, UI surfaces, contracts, and verification.
   - Prefer existing repository patterns over new abstractions.
   - Route architecture decisions through Arthur and relevant domain specialists.

3. **Charlie Challenge Gate**
   - Challenge the prior handoff for engineering principles, modularity, portability, coupling, cohesion, testability, and maintainability.
   - Require concrete fixes or explicit risk acceptance before proceeding.

4. **Engineering Agent**
   - Implement the accepted plan.
   - Stay inside the agreed write scope.
   - Run focused formatting, build, or test checks when available.
   - Use specialist skills for implementation-heavy domain work.

5. **Reviewer Agent**
   - Review as a pull request.
   - Lead with findings ordered by severity and file/line references.
   - Focus on bugs, regressions, privacy, architecture drift, and missing tests.

6. **Charlie Challenge Gate**
   - Challenge the implementation and review outcome.
   - Look for missed acceptance criteria, brittle behavior, weak tests, and source-traceability gaps.

7. **Testing Agent**
   - Add or update unit, integration, and automation tests appropriate to risk.
   - Prefer focused tests over broad test churn.
   - Report commands run and residual gaps.
   - Use Terry for Swift Testing and add other specialists for domain-specific test risk.

8. **Integration Agent**
   - Reconcile final changes, docs, and handoffs.
   - Confirm verification or explain why it could not run.
   - Prepare the final summary.

## Model Guidance

- Use the strongest available model for orchestration, architecture, and final integration.
- Use lighter models only for bounded decomposition, challenger, review, or testing passes when speed/cost matters and the task is low risk.
- Do not hardcode model names into repo files. Model availability is a Codex CLI/session concern.

## Standard Handoff

Each substantial role should end with:

```md
## Result
Brief summary of what changed or what was decided.

## Decisions
- Important decisions made and why.

## Contracts / APIs
- Model fields, service signatures, view inputs, or generated-output shapes that downstream roles must honor.

## Write Scope Used
- Files or directories edited or inspected.

## Changed Files
- path/to/file.swift

## Verification
- Commands run and results, or why verification was not run.

## Risks
- Known limitation or open question.

## Next Role
Recommended next role and why.
```

## Repository Constraints

- Respect the active repository's conventions, commands, and architecture.
- When a project has domain-specific rules, load them from `AGENTS.md`, task files, or local docs instead of assuming any app-specific behavior.
- SwiftData changes must account for relationships, migrations, delete behavior, and app launch wiring.
- SwiftUI changes must include empty, loading, error, and long-content states when relevant.
