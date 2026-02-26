# Smeetz Cursor Shared Skills

Shared [Cursor Agent Skills](https://cursor.com/docs/context/skills) for Smeetz. Use these skills across projects for code review, conventions, deployment, and other reusable workflows. Only **non–project-specific** skills belong here; project-specific skills stay in each repo’s `.cursor/skills/`.

## Skills

| Skill | Description |
|-------|-------------|
| [_template](skills/_template/) | Template for creating new skills. Copy this folder and edit `SKILL.md`. |

*(Add new rows as you add skills; descriptions can be taken from each skill’s `SKILL.md` frontmatter.)*

## Installation

### **Install via Cursor Remote Rule (GitHub)** — recommended

1. Open **Cursor Settings** → **Rules**.
2. **Add Rule** → **Remote (Github)**.
3. Enter this repo’s URL (and path to a specific skill folder if your Cursor version supports it).

Skills load from the repo; updates apply when Cursor refreshes.

### Option 2: Symlinks

1. Clone this repo (e.g. into `~/projects/smeetz/cursor-shared-skills`).
2. Symlink the skills you want:

   **Per project** — from your project root:
   ```bash
   mkdir -p .cursor/skills
   ln -s /path/to/cursor-shared-skills/skills/your-skill .cursor/skills/your-skill
   ```

   **Globally** (all your projects):
   ```bash
   mkdir -p ~/.cursor/skills
   ln -s /path/to/cursor-shared-skills/skills/your-skill ~/.cursor/skills/your-skill
   ```

3. Restart Cursor or open a new Agent chat so skills are picked up.

## Updating

- If you use **symlinks**: run `git pull` in the `cursor-shared-skills` repo; skills update automatically.
- If you use **copies**: re-copy the updated skill folders into `.cursor/skills/` or `~/.cursor/skills/`.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add or change skills.

## License

[MIT](LICENSE) © Smeetz
