# My Skills

Personal agent skills maintained in one Git repository. On this Mac, Codex loads these skills through symbolic links in `~/.codex/skills`, so editing a file here updates the installed copy directly.

## Skills

| Directory | Purpose |
| --- | --- |
| `write-documents/` | Write documents matched to their purpose and audience, using Diátaxis to choose an appropriate form. |
| `spec-docs/` | Create and revise product requirements, feature requirements, and solution designs. |
| `implement-with-tester/` | Coordinate implementation with a separate agent responsible for testing. |

Each skill starts with `SKILL.md`. Its `references/` and `agents/` directories contain supporting instructions or interface metadata where needed.

## Make changes

Edit the files in this repository, review the diff, and commit the changes. The global links point here; no copy or synchronization step is required. Keep this repository at its current location unless you also update the links.

System skills, plugin caches, and third-party skills are managed separately and are not included here.

## Connect this checkout to Codex

The current checkout is `/Users/piotrziolkowski/Documents/my-skills`. The following commands connect that location to the default Codex skill directory. Before using them on another machine, change the checkout path and inspect any existing destinations. If a destination already exists, preserve and reconcile it first; these commands do not replace it.

```sh
skills_repo="/Users/piotrziolkowski/Documents/my-skills"
mkdir -p "$HOME/.codex/skills"
for skill in write-documents spec-docs implement-with-tester; do
  destination="$HOME/.codex/skills/$skill"
  if [ -e "$destination" ] || [ -L "$destination" ]; then
    printf 'Already exists: %s\n' "$destination"
    continue
  fi
  ln -s "$skills_repo/$skill" "$destination"
done
```

Verify a connection with `readlink "$HOME/.codex/skills/write-documents"` and check that its `SKILL.md` is readable. Start a new Codex chat if the skill list has not refreshed.

On this Mac, `~/.codex/AGENTS.md` also instructs agents to apply `write-documents` before creating non-code documents or substantially revising them. That global instruction remains outside this repository; cloning the skills alone does not install it. Its existing skill path continues to work through the symbolic link.

## Conclusion

This repository is the source of truth for these three personal skills. Maintain their content here and keep the global links pointing to the checkout.
