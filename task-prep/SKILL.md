---
name: task-prep
description: Prepare work for unattended implementation. Turns an epic, ticket, document or request into a PRD, requirements and solution design plus a bd task that meets the project's readiness checklist, ending at the hand-off. Use when the user wants work prepared, specified for agents, or handed off for implementation.
---

# Prepare a task for hand-off

You take whatever input the user brings and finish with bd tasks an unattended agent can implement without asking anyone. Everything after the hand-off happens without the user, so every question that matters is asked here.

The project's agent instructions index its documentation and name where each family starts. Read the process contract before anything else, together with the domain docs and the tracker guide they name. The process contract defines the documents and their levels, the task size, the task fields, the labels and the readiness checklist. If the agent instructions name no process contract, tell the user and stop. Write every document with the `spec-docs` skill.

## Steps

1. **Collect the input.** Read every source the user points at: bd issues (`bd show`), files, links, the conversation. List what each source establishes and what it leaves open. Done when every consequential claim you will use has a source or is marked open.

2. **Find the epic and its PRD.** Look for an existing bd epic and PRD the work belongs to among the project's specifications. Create or extend the PRD when none covers the work, in the directory the process contract prescribes. Done when the work sits under one epic whose `spec_id` points at a PRD that states its problem, outcome, scope and exclusions.

3. **Split the work into tasks.** Propose tasks following the task-size rule in the process contract, each a vertical, demoable increment, with blocking order. Mark small-lane candidates. Show the breakdown to the user and iterate until they approve it.

4. **Specify each task.** Write or extend its requirements and solution design, looking up facts yourself in code and documents. Settle the requirements first, in rounds of numbered questions, each with your recommended answer. When the task moves or rebuilds existing code, first list from the code the observable behaviour of the area it touches, per variant where variants differ (for example per source): what the user or the system sees, what is stored after a failure, timings, retries, limits. Show the list to the user as numbered questions: keep, change or irrelevant. Each kept item becomes a requirement with its criterion. Do not write a criterion that nothing else changes: it names no behaviour, and an implementer cannot tell what it protects.

   Then walk the design in levels, top down, one level per round, and start the next level after the user answers:

   1. **Responsibilities:** which part of the system owns what data and rules, decides what, and owns each fixed list.
   2. **Communication:** what crosses between those parts, in which direction, triggered by what.
   3. **Inside each part:** what is stored and in what shape, what a contract carries, what the flow does on the normal path and on refusal. For each operation the task adds or alters, walk the project's architecture rules and the code and list the situations the operation can actually meet beyond the normal path. Each gets an outcome from the user, is marked Open, or becomes a spike; an outcome the user sees is a product rule and goes back to the requirements.
   4. **Outside systems and rollout:** external services touched, migrations, deployment order.

   Open the design by asking how the user would build it, naming these levels; the user may add, drop or reorder them. For a small-lane task, one round covers the levels that hold a choice. Check every option at its level against the project's architecture rules, your recommended one included, and name the design costs from the architecture rules' list that it carries. Each round holds, in order:

   - **Proposal:** the user's proposal for this level, taken from their opening answer or asked for now, in a line or two.
   - **Agreement:** where you agree, in one line. A proposal you agree with is recorded as a plain statement.
   - **Challenge:** your option set beside the user's, each with its consequences and design costs, and your recommendation. Raise it when you hold a checkable argument against the proposal: a fact verified in code or documents, an architecture rule or a design cost, a requirement the proposal misses, or a concrete failure scenario.
   - **Questions:** the questions of this level only. Their answers are plain statements, and the options a question named stay out of the record.

   Each choice gets one challenge. The user's answer, a revised proposal included, closes it; a fact found later that breaks it goes to the user as that fact. A challenged choice is recorded as a decision with both options: the one not chosen is discarded with the user's reason, or, when the user withdrew their own proposal, with the fact that changed it. A cost the user accepts goes into the design as part of that decision.

   When the user has no proposal for a level, lay out the options with their consequences and design costs and recommend one, still one level at a time.

   An unknown that needs investigation becomes a bd `spike` blocking the task, and the requirements state only what is known.

   Before writing a design's decisions, walk them with the user one at a time as they will be recorded: the chosen option, the discarded options, and the reason for each, asking for the user's reason where they gave none ("none" is an answer). The user says whether each entry stays a decision, becomes a plain fact, loses an option or leaves the record; this pass shapes only the record, and every choice stays as the user made it. A product rule a design round surfaces reopens the requirements: ask it as a numbered question, record it as a requirement, and cite its ID in the design. Done when every level is walked or dropped by the user, the user has confirmed the decision record, each acceptance criterion names how it is checked, and every contract the task touches is stated exactly.

5. **Cross-check.** Every requirement of the task has an acceptance criterion; every criterion is covered by the design's verification; no design decision weakens a criterion; every product rule the design relies on cites a requirement; every kept behaviour from the step 4 list has a criterion; every situation listed at level 3 has an outcome or is Open; no statement refers to behaviour it does not name; terms match the glossary. Fix the documents until the check is clean; a decision that weakens a criterion goes back to the user as that fact.

6. **Write the bd tasks.** One bd task per increment, child of the epic, with the fields the process contract names: document links in metadata, `spec_id`, acceptance criteria as `AC-ID: observable result`, native blocking edges. Leave them without `ready-for-agent`.

7. **Hand off.** Run the readiness checklist on each task and show the user, per task: the documents, the acceptance criteria, the assumptions you recorded, the design decisions whose reason, or a discarded option's reason, is none, and anything marked `ready-for-human`. Apply `ready-for-agent` only to tasks the user approves. The runner sees only what is in `main` on the remote, so right before applying `ready-for-agent` to a task or the epic, push `main` with the documents (the user's approval of the hand-off covers this push) and run the check the readiness checklist names for documents at the exchange point; when it fails, apply no label and show the user its output. When every open task of the epic carries `ready-for-agent` or `ready-for-human`, ask the user which requirements are load-bearing (the decisions most of the epic builds on), record their IDs in the epic's `metadata.load_bearing`, then ask the user to hand off the epic and apply `ready-for-agent` to it on their approval; the runner starts none of the epic's tasks before that. Done when every approved task carries `ready-for-agent`, every other task carries the label that says why it is waiting, and the epic carries `ready-for-agent` once all its tasks are prepared.

A follow-up the runner filed (`metadata.type=follow-up`) is prepared like any task: its description states the conflict and the decision needed; once the user decides, update the documents, give it document links and acceptance criteria that include removing its `FOLLOW-UP` markers, and apply `ready-for-agent`. An epic carrying `follow_ups=true` was taken back by the runner: once every open follow-up carries `ready-for-agent`, ask the user to hand the epic off again and, on their approval, replace its `needs-info` with `ready-for-agent`. The runner never does this itself.

Preparing tasks authorises document edits and bd writes. Implementation belongs to the runner after the hand-off.
