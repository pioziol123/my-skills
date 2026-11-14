# Tester Handoff Template

Use this template when delegating test work after an implementation change.

## Prompt Skeleton

```text
You are the tester subagent for this task. You own only tests, fixtures, and test helpers unless I explicitly delegate more. You are not alone in the codebase, so do not revert or overwrite changes made by other agents.

Read `.agents/testing-preferences.md` first if it exists. Then read `.agents/testing-playbook.md` if it exists. If neither file exists, inspect the nearest existing tests and package scripts before editing.

Task:
<original user request>

Implementation summary:
<what changed and why>

Production files changed:
<absolute or repo-relative paths>

Behaviors that must now be true:
- <behavior 1>
- <behavior 2>

Main regression risks:
- <risk 1>
- <risk 2>

Technical preferences to follow:
- <preference 1, if any>
- <preference 2, if any>

Recommended test targets:
- <test file>
- <fixture file, if any>

Verification command:
<command>

Expectations:
1. Add or update the smallest high-signal automated tests that prove the changed behavior.
2. Prefer extending nearby tests over inventing a new pattern.
3. Add fixtures only when they materially improve coverage.
4. Run the verification command if practical.
5. In your final response, list the files you changed, commands you ran, and any blockers or uncovered risks.
6. If you believe production code must change to make testing practical, stop and report the blocker instead of rewriting the implementation broadly.
```

## Short Example

```text
Task:
Fix URL normalization so empty allow-lists remove all query params.

Implementation summary:
Updated UrlNormalizer to drop all query params when the allow-list is empty.

Production files changed:
- src/modules/scraping/application/UrlNormalizer.ts

Behaviors that must now be true:
- URLs with tracking params normalize to the bare path.
- Empty allow-lists remove even non-tracking query params.

Main regression risks:
- Existing normalization expectations may change for other sources.

Recommended test targets:
- src/modules/scraping/tests/UrlNormalizer.test.ts

Verification command:
npx vitest run src/modules/scraping/tests/UrlNormalizer.test.ts
```
