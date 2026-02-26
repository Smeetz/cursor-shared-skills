# Contributing to Smeetz Cursor Shared Skills

## Adding a New Skill

1. Copy `skills/_template/` to a new folder: `skills/<skill-name>/`.
   - Use lowercase letters, numbers, and hyphens only (e.g. `code-review`, `commit-msg`).
2. Edit `SKILL.md`:
   - Set `name` in the YAML frontmatter to match the folder name.
   - Write a clear `description` (what the skill does and when the agent should use it).
   - Fill in the body: when to use, step-by-step instructions; link to `references/` or `scripts/` if needed.
3. Optionally add:
   - `scripts/` — executable helpers the agent can run.
   - `references/` — extra docs loaded on demand.
   - `assets/` — static files (templates, configs).
4. Update the [README](README.md) skills table with the new skill and its description.
5. Open a pull request.

## Changing an Existing Skill

- Edit the skill’s files under `skills/<skill-name>/`.
- Keep `SKILL.md` under ~500 lines; use progressive disclosure (link to `references/` for long content).
- Update README if the description or purpose changed.
- Open a pull request.

## Skill Conventions

- **English only** — all skill content (frontmatter, body, comments in scripts) in English.
- **Non–project-specific** — only skills that apply across Smeetz projects belong here. Project-specific skills stay in each repo’s `.cursor/skills/`.
- **Concise** — the agent shares context with the rest of the chat; avoid unnecessary verbosity.

## Questions

Open an issue or ask in your team channel.
