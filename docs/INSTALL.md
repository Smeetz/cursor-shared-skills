# Installing Smeetz Cursor Shared Skills

## Prerequisites

- [Cursor](https://cursor.com/) installed.
- This repo cloned (e.g. `git clone <repo-url> cursor-shared-skills`).

## Choose Scope

- **Per project:** Skills available only in that project (use `.cursor/skills/`).
- **Globally:** Skills available in all projects (use `~/.cursor/skills/`).

## Install via Symlinks (recommended)

1. **Clone the repo** (if not already):
   ```bash
   git clone <repo-url> /path/to/cursor-shared-skills
   cd /path/to/cursor-shared-skills
   ```

2. **Create the target skills directory:**
   - Per project: from your project root, run `mkdir -p .cursor/skills`
   - Globally: run `mkdir -p ~/.cursor/skills`

3. **Symlink each skill** you want:
   - Per project (from project root):
     ```bash
     ln -s /path/to/cursor-shared-skills/skills/code-review .cursor/skills/code-review
     ```
   - Globally:
     ```bash
     ln -s /path/to/cursor-shared-skills/skills/code-review ~/.cursor/skills/code-review
     ```
   Replace `code-review` with the actual skill folder name; repeat for each skill.

4. **Verify:** Restart Cursor or open a new Agent chat. Skills appear under Rules / Agent Decides (or Cursor Settings → Rules, depending on version).

## Install via Copy (no symlinks)

1. Clone the repo.
2. Copy desired folders from `skills/` into `.cursor/skills/` (project) or `~/.cursor/skills/` (global):
   ```bash
   cp -r /path/to/cursor-shared-skills/skills/code-review .cursor/skills/
   ```
3. To update later, re-copy the skill folders after `git pull` in the shared-skills repo.

## Install via Cursor Remote Rule (GitHub)

1. Open **Cursor Settings** (e.g. Cmd+Shift+J / Ctrl+Shift+J).
2. Go to **Rules** (or **Project Rules**).
3. **Add Rule** → **Remote (Github)**.
4. Enter this repo’s URL. If your Cursor version supports paths, you can point to a specific skill folder.
5. Save; Cursor will load the rule(s) from the repo.

## Troubleshooting

- **Skills not showing:** Ensure the skill folder contains a `SKILL.md` file and that Cursor has been restarted or a new Agent chat opened.
- **Symlink path:** Use an absolute path for the symlink source so it works from any working directory.
