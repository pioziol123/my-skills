---
name: implement-task
description: Implement one prepared bd task unattended in a runner worktree and finish with a result file. Use when a runner prompt hands you a task to implement.
---

# Implement a prepared task

You run without a human, inside a sandbox. The runner gave you one task, a worktree on the task's own branch, and a result file path. Your workspace is that worktree and its branch: the runner owns bd, `master`, remotes, merging and closing the task, and it judges your work with its own gates and a separate reviewer. Anything you cannot settle from the documents and the code goes into the result file, because nobody can answer a question mid-run.

## Steps

1. **Read the contract.** Read the task in the prompt, then every document it links (PRD, requirements, solution design) in full, `docs/agents/implementation-workflow.md`, and the project's agent instructions. If the prompt includes a failure report from an earlier attempt, read it as the first thing to fix. Done when you can name, for each acceptance criterion, the check that proves it.

2. **Implement.** Work test-first with the `tdd` skill where the solution design names a seam. Follow the design's contracts exactly; reuse the patterns the code already has. Keep the change inside the task. Commit on the current branch as you reach green steps, each message starting with the task id.

3. **Classify discoveries** as they appear, using the workflow file's rules:
   - a defect inside the task: fix it;
   - a gap or contradiction in the documents that changes behaviour or a contract: stop, commit what is sound, and finish as `blocked` with the question;
   - new scope outside the task: record it as a follow-up and carry on.

4. **Verify.** Run the gate and every check the acceptance criteria name, using the commands section of the workflow file, and fix what fails before going on. Done when the gate exits 0 on committed work and each criterion has evidence: the command or test, and its observed result.

5. **Write the result file** at the path from the prompt, as JSON:

   ```json
   {
     "status": "done",
     "summary": "what changed, in two or three sentences",
     "evidence": [{ "ac": "AC-01", "check": "pnpm vitest run test/x.test.ts", "result": "passed" }],
     "followups": [{ "title": "...", "description": "..." }],
     "question": null
   }
   ```

   Use `"status": "blocked"` with `question` set when step 3 stopped you or a criterion cannot be met. Every acceptance criterion appears in `evidence` when the status is `done`.

Finish with the worktree clean: all work committed, nothing left uncommitted.

The runner checks your work after you finish. When it finds a problem it sends the report back into this same session: treat it like a failing check from step 4, fix it, rerun the gate, commit and rewrite the result file.
