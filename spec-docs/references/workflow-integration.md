# Integration with planning and execution

Use when handing specifications to a tracker, combining this skill with other planning skills, or coordinating multiple repositories. These are integration rules, not a requirement to install any particular tool.

## Progressive detail

For a large project: vision and outcomes → stages and key unknowns → first useful slice → requirements and SD for that slice → execution tasks → verification and feedback. Keep future stages coarse. A discovery question may become a research or prototype task before implementation is ready.

After delivery, compare the result with the intended outcome and update remaining scope. A rejected assumption can change the PRD; propagate the accepted change through dependent documents and tasks.

## With Matt Pocock skills

- Use `grill-me` / `grilling`, `research`, `prototype`, and `wayfinder` when their capabilities fit the current uncertainty.
- This document family replaces the combined output of `to-spec` when the project uses separate PRD, requirements, and SD. Avoid a second competing specification.
- Feed `to-tickets` the selected requirements and SD. Derive acceptance from them and partition work into independently verifiable slices with real blocking dependencies. Scope splitting must preserve the complete required behaviour across the slices.
- Use `implement`, `tdd`, and `code-review` for execution where appropriate. Pass canonical document references and the relevant repository instructions. Review against both acceptance criteria and agreed design contracts.
- `implement-spec` assumes an integration branch. Adapt that execution strategy to repository boundaries and the project's merge/release policy before using it across repositories.

Use only skills available in the current environment. Explicit user invocation and tool permissions remain governed by that environment. The specification workflow itself does not start these execution workflows.

## With Beads or another tracker

Choose one authoritative place for execution status. Specifications own scope and decisions; the tracker owns assignments, dependencies, blockers, progress, and completion evidence. Document this mapping in the project's existing workflow configuration. For Pocock workflows, `docs/agents/issue-tracker.md` is a supported convention; creating it is setup work, not necessary for drafting a PRD.

A useful execution task contains:

- A stable task identifier and, where applicable, its parent initiative or external ticket ID.
- The canonical requirements and SD references, with a revision when work needs a fixed baseline.
- The outcome and exact requirement/acceptance IDs covered, plus a concise completion condition.
- The owning repository or component, actual blocking dependencies, unresolved decisions, and later verification/PR evidence.

Keep enough task context for a fresh agent to resume work, while reading the canonical documents for the full rules. If a summary conflicts with its source, reconcile it before execution. Resolve moved spec paths when archiving documents; use stable links or update known references.

With Jira plus Beads, distinguish business work items from agent execution tasks. One Jira item may map to multiple Beads tasks. Finishing one task does not automatically complete its parent; use the project's agreed completion rule. Without Jira, readable initiative IDs suffice.

## Multiple repositories

Use the project's repository map to resolve locations. Define ownership and interface dependencies in the SD and tasks. Follow each repository's local instructions, use its own branches and PRs, and connect them with stable initiative/task references. Include cross-repository compatibility and integration verification in the completion conditions where needed.

## Readiness and completion

Distinguish a drafted document, accepted scope/design, a task with no scheduling blockers, and verified delivery. In Beads, an unblocked task is not by itself evidence that its specification is approved or complete. A task becomes executable when its material decisions are resolved and required dependencies are satisfied under the project workflow. A document or task does not grant authorization for external writes.
