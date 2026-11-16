---
name: implement-task
description: Implement one prepared bd task unattended in a runner worktree and finish with a result file. Use when a runner prompt hands you a task to implement.
---

# Implement a prepared task

You run without a human, inside a sandbox. The runner gave you one task, a worktree on the task's own branch, and a result file path. Your workspace is that worktree and its branch: the runner owns bd, `master`, remotes, merging and closing the task, and it judges your work with its own gates and a separate reviewer. Anything you cannot settle from the documents and the code goes into the result file, because nobody can answer a question mid-run.

## Steps

1. **Read the contract.** Read the task in the prompt, then every document it links (PRD, requirements, solution design) in full, then the project's agent instructions and the process contract and architecture rules they name. If the prompt includes a failure report from an earlier attempt, read it as the first thing to fix. Done when you can name, for each acceptance criterion, the check that proves it.

2. **Implement.** Work test-first with the `tdd` skill where the solution design names a seam. Follow the design's contracts exactly; reuse the patterns the code already has. Keep the change inside the task. Commit on the current branch as you reach green steps, each message starting with the task id.

3. **Classify discoveries** as they appear, using the process contract's rules:
   - a defect inside the task: fix it;
   - a spec conflict, a gap or contradiction in the documents: walk the classification in the process contract's section "Spec conflicts during implementation", with the epic's `load_bearing` list and open follow-ups from the prompt. An **assumption** you decide by precedence, record, and pin with a test of the case it rests on; a **deviation** you implement as interim code with its marker, describe as a follow-up with the `write-documents` skill, and carry on; anything else stops you: commit what is sound and finish as `blocked` with the question;
   - a design cost from the architecture rules that your change would carry and the solution design does not record: take an option without it that the design has not discarded; when every option the design has not discarded carries one, treat it as a spec conflict, so a cost you keep becomes an assumption naming the cost, whose `requirements` lists the requirements the change serves and whose `rule` names the architecture rule instead of a precedence rule;
   - new scope outside the task: record it under `new_scope` and carry on.

   Build nothing new on another follow-up's interim code (its marker is in the prompt). Done when every conflict you met has one of the three outcomes.

4. **Verify.** Run the gate and every check the acceptance criteria name, using the commands section of the process contract, and fix what fails before going on. Done when the gate exits 0 on committed work and each criterion has evidence: the command or test, and its observed result.

5. **Write the result file** at the path from the prompt, as JSON:

   ```json
   {
     "status": "done",
     "summary": "what changed, in two or three sentences",
     "evidence": [{ "ac": "AC-01", "check": "pnpm vitest run test/x.test.ts", "result": "passed" }],
     "assumptions": [{
       "id": "ASM-1",
       "requirements": ["R-05", "T2-R02"],
       "gap": "what the documents leave open",
       "decision": "what the code does",
       "rule": "the precedence rule applied",
       "if_reversed": "what changes if the owner decides otherwise"
     }],
     "deviations": [{
       "id": "DEV-1",
       "kind": "contradiction | underspecified | blocked-by-task",
       "requirements": ["R-01", "T2-AC05"],
       "deferred_acs": ["T2-AC05"],
       "interim": "what the code does until the follow-up",
       "qualification": "how each qualification criterion holds",
       "title": "follow-up title",
       "description": "the full follow-up description"
     }],
     "new_scope": [{ "title": "...", "description": "..." }],
     "question": null
   }
   ```

   Use `"status": "blocked"` with `question` set when step 3 stopped you or a criterion cannot be met. When the status is `done`, every acceptance criterion appears either in `evidence` or in one deviation's `deferred_acs`, and every deviation's marker `FOLLOW-UP(<task id>/<deviation id>)` is in the committed code. Leave the lists empty when there is nothing to report.

Finish with the worktree clean: all work committed, nothing left uncommitted.

The runner checks your work after you finish. When it finds a problem it sends the report back into this same session: treat it like a failing check from step 4, fix it, rerun the gate, commit and rewrite the result file.
