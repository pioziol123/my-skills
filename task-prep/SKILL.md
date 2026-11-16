---
name: task-prep
description: Prepare work for unattended implementation. Turns an epic, ticket, document or request into a PRD, requirements and solution design plus a bd task that meets the project's readiness checklist, ending at the hand-off. Use when the user wants work prepared, specified for agents, or handed off for implementation.
---

# Prepare a task for hand-off

You take whatever input the user brings and finish with bd tasks an unattended agent can implement without asking anyone. Everything after the hand-off happens without the user, so every question that matters is asked here.

The project's workflow file is the contract: read `docs/agents/implementation-workflow.md` before anything else, together with the domain and tracker files under `docs/agents/`. It defines the documents and their levels, the task size, the task fields, the labels and the readiness checklist. If the file is missing, tell the user and stop. Write every document with the `spec-docs` skill.

## Steps

1. **Collect the input.** Read every source the user points at: bd issues (`bd show`), files, links, the conversation. List what each source establishes and what it leaves open. Done when every consequential claim you will use has a source or is marked open.

2. **Find the epic and its PRD.** Look for an existing bd epic and PRD the work belongs to under `docs/specs/`. Create or extend the PRD when none covers the work, in the directory the workflow file prescribes. Done when the work sits under one epic whose `spec_id` points at a PRD that states its problem, outcome, scope and exclusions.

3. **Split the work into tasks.** Propose tasks following the task-size rule in the workflow file, each a vertical, demoable increment, with blocking order. Mark small-lane candidates. Show the breakdown to the user and iterate until they approve it.

4. **Specify each task.** Write or extend its requirements and solution design. Put decisions to the user in rounds: number each question and give your recommended answer. Look up facts yourself in code and documents. An unknown that needs investigation becomes a bd `spike` blocking the task rather than a guess written as a requirement. Done when each acceptance criterion names how it is checked and every contract the task touches is stated exactly.

5. **Cross-check.** Every requirement of the task has an acceptance criterion; every criterion is covered by the design's verification; no design decision weakens a criterion; terms match the glossary. Fix the documents until the check is clean.

6. **Write the bd tasks.** One bd task per increment, child of the epic, with the fields the workflow file names: document links in metadata, `spec_id`, acceptance criteria as `AC-ID: observable result`, native blocking edges. Leave them without `ready-for-agent`.

7. **Hand off.** Run the readiness checklist on each task and show the user, per task: the documents, the acceptance criteria, the assumptions you recorded and anything marked `ready-for-human`. Apply `ready-for-agent` only to tasks the user approves. When every open task of the epic carries `ready-for-agent` or `ready-for-human`, ask the user which requirements are load-bearing (the decisions most of the epic builds on), record their IDs in the epic's `metadata.load_bearing`, then ask the user to hand off the epic and apply `ready-for-agent` to it on their approval; the runner starts none of the epic's tasks before that. Done when every approved task carries `ready-for-agent`, every other task carries the label that says why it is waiting, and the epic carries `ready-for-agent` once all its tasks are prepared.

A follow-up the runner filed (`metadata.type=follow-up`) is prepared like any task: its description states the conflict and the decision needed; once the user decides, update the documents, give it document links and acceptance criteria that include removing its `FOLLOW-UP` markers, and apply `ready-for-agent`. An epic carrying `follow_ups=true` was taken back by the runner: once every open follow-up carries `ready-for-agent`, ask the user to hand the epic off again and, on their approval, replace its `needs-info` with `ready-for-agent`. The runner never does this itself.

Preparing tasks authorises document edits and bd writes. Implementation belongs to the runner after the hand-off.
