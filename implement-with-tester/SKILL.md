---
name: implement-with-tester
description: Orchestrate implementation work with an automatic tester subagent. Use when Codex is asked to implement, modify, refactor, or fix code and the change should be followed by new or updated automated tests. Especially appropriate for feature work, bug fixes, parser changes, API behavior changes, persistence changes, and regression fixes where one agent should own production code while a second agent writes tests, fixtures, and targeted verification.
---

# Implement With Tester

## Overview

Run coding work as a paired workflow: the main agent owns production changes and integration, then hands testing to a dedicated tester subagent before final verification. Treat test authoring as a required phase of implementation, not optional cleanup.

## Workflow

1. Inspect the codebase and identify the production files that need changes.
2. Implement the production change locally.
3. After the implementation exists, spawn a `worker` subagent dedicated to tests.
4. Review and integrate the tester's changes.
5. Run the narrowest meaningful verification, then report outcomes and gaps.

## Main Agent Responsibilities

- Own all production-code edits.
- Decide which behaviors changed and therefore require tests.
- Choose the test target before spawning the tester.
- Keep moving on integration and verification while the tester works when parallelism is useful.
- Review test changes before finalizing.

## Tester Subagent Responsibilities

- Own test files, fixtures, and test helpers.
- Add or update automated tests for the implemented behavior.
- Prefer the closest existing test suite over creating a new testing pattern.
- Run targeted verification when practical.
- Report blockers instead of silently skipping coverage.

## Tester Spawn Rules

- Use `spawn_agent` with `agent_type: "worker"` once the production change is concrete enough to hand off.
- Give the tester explicit ownership of test files, fixtures, and helpers only.
- Tell the tester it is not alone in the codebase and must not revert edits made by others.
- If the tester needs a production-code seam that does not exist, instruct it to report the blocker instead of rewriting the implementation wholesale.
- If the task is docs-only, comment-only, or has no behavioral change worth testing, skip the tester and explain why in the final response.

## Required Tester Handoff

Include all of the following in the tester prompt:

- the original user request
- a short implementation summary
- the production files changed
- the behavior that must now be true
- the main regression risks
- the most likely test file or fixture path
- the verification command to run

If the workspace contains `.agents/testing-preferences.md`, tell the tester to read it first. Then read `.agents/testing-playbook.md` if it exists. Use [tester-handoff-template.md](./references/tester-handoff-template.md) as the default prompt skeleton.

## Project Technical Preferences

Support a repo-local preferences file at `.agents/testing-preferences.md`.

Use it for details such as:

- preferred assertion style
- mocking and fixture rules
- snapshot policy
- naming conventions for test files
- boundaries between unit, integration, and parser tests
- commands that should be preferred or avoided
- any technology-specific constraints

Treat this file as the highest-priority source for test-writing preferences inside a workspace.

## Test Selection Heuristics

- Extend an existing nearby test file when one already covers the same module.
- Add a focused regression test for bug fixes.
- Add or refresh fixtures for parsers and scrapers when the behavior depends on real payload shape.
- Assert externally visible behavior rather than internal implementation details.
- Prefer one high-signal test over many weak duplicates.

## Verification Expectations

- Run the narrowest meaningful test command first.
- Run broader validation when the change touches shared behavior or the suite is fast enough.
- Mention exactly what was run and what was not run.

## Final Response Checklist

- confirm whether the tester subagent ran
- list the behavior covered by tests
- summarize verification commands and outcomes
- call out any remaining testing gaps

## Example Trigger Phrases

- "Implement this scraper change and add tests"
- "Fix this bug in the parser"
- "Refactor this service"
- "Add support for a new response shape"
- "Update this feature"

## Resource

- [tester-handoff-template.md](./references/tester-handoff-template.md) contains the default prompt structure for the tester subagent.
