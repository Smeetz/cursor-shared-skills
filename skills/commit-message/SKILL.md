---
name: commit-message
description: Generate commit messages in the strict semicolon-separated 5-field schema (type, scope, summary, body, footer) aligned with Change log Process and n8n → Intercom. Use when the user or agent makes commits via Chat or when asked to suggest a commit message.
---

# Commit message

This skill defines the commit message format for Smeetz repos, aligned with **Change log Process** (AI-Driven Changelog, n8n → Intercom). Use it when making commits via the agent or when asked to suggest a commit message.

**Limitation:** The built-in “Generate commit message” (✨) button does not use this skill; it applies only when the agent is asked to commit or suggest a message in Chat.

---

## When to Use

- Use this skill when the user or agent is about to make a commit via Cursor Chat.
- Use when the user asks to “write a commit message”, “suggest a commit message”, “commit this”, or similar.
- Do **not** rely on this skill for the in-editor “Generate commit message” button; that path does not load skills.

---

## Instructions

When generating a commit message, follow these steps:

1. **Read [references/scopes.md](references/scopes.md)** for the list of allowed scopes. Use **only** scopes from that list. If the change does not match any scope in the list, use **Other**.

2. **From the diff or context**, determine:
   - **Type:** exactly one of `feat`, `fix`, `perf`, `refactor`, `test`.
   - **Scope:** pick from [references/scopes.md](references/scopes.md) (or **Other** if none fits).

3. **Draft summary:** imperative mood, max 70 characters, no semicolon inside. Be specific about what was affected; add platform/device when relevant (e.g. iOS, mobile). Do not end with a period. Generate from the staged changes or user description.

4. **Draft body:** what and why (user-facing), not how in code. Max 200 characters. Full sentence. Generate from context (diff or user input).

5. **Resolve footer:** Jira issue key in format `<project>-<id>` (e.g. L3-1234, FIS-456). Order: (1) if the user specified a task — use it; (2) else try to extract from branch name (e.g. `feature/L3-1234` → L3-1234); (3) else, in interactive Chat, ask the user for the Jira key and **wait for their answer instead of outputting a commit message**; (4) if, after asking, the user does not specify a key, does not know it, or says there is no ticket — use **NOJIRA**. Validate format (letters, digits, hyphen only) so the Bitbucket→Jira link works.

6. **Output the commit message as plain text only (after Step 5 is fully resolved):** If you still need to ask the user for the Jira key, do **not** output a commit message yet. Once the footer is resolved, output with no markdown, no code block, no commentary. **Each line must start with the field name** (`type:`, `scope:`, `summary:`, `body:`, `footer:`) followed by a space, the value, and a semicolon. Exactly 5 lines in this order, **with no blank lines between them** (one newline between each line). Ready to paste into `git commit`.

---

## Commit Message Format

Format is **not** Conventional Commits. Use this **strict semicolon-separated** order (all fields required):

```
type: <type>;
scope: <scope>;
summary: <summary>;
body: <body>;
footer: <jira_key>;
```

**Footer:** `jira_key` is the Jira issue key in the form **`<project>-<id>`** (e.g. `L3-1234`, `FIS-456`). Use **NOJIRA** when no ticket applies.

### Type

Exactly one of: **feat**, **fix**, **perf**, **refactor**, **test**. Baked into this skill; update the skill in the repo if the list changes.

### Scope

Use **only** scopes from [references/scopes.md](references/scopes.md). If the change does not match any listed scope (e.g. new feature), use **Other**.

### Summary

- Imperative mood (“Resolve”, not “Resolved”).
- Be specific about what was affected; add platform/device when relevant (e.g. iOS, mobile).
- No period at the end. Max 70 characters.
- Avoid “bug”, “issue”, “update”, “improvement” without context.
- **Generate from context:** use staged changes (git diff) or the user’s description to write a short, accurate one-liner.

### Body

- What and why (user-facing), not “how” in code. Max 200 characters. Full sentence.
- **Generate from context:** use the diff or user input to describe what changed and why.

### Footer

- **jira_key:** Jira issue key in the form **`<project>-<id>`** (e.g. `L3-1234`, `FIS-456`). Required for Bitbucket→Jira link.
- **Order:** (1) user specified a task → use it; (2) else extract from branch name; (3) else ask the user; (4) user does not specify or does not know → **NOJIRA**.
- **Validate** format (letters, digits, hyphen); otherwise the Bitbucket link will not work.

### Constraints

- Do **not** use semicolons inside field values — use commas or periods only.
- No markdown, no commentary, no line breaks inside a field. All five fields are required.

---

## Valid Examples

**Full example (feat, with Jira key):**

```
type: feat;
scope: Online checkout;
summary: Add guest checkout option for single-ticket purchases;
body: Allow visitors to complete purchase without creating an account to reduce friction and increase conversion.;
footer: L3-1234;
```

**Full example (fix, footer NOJIRA):**

```
type: fix;
scope: Order management;
summary: Resolve Pay Now button unresponsive on iOS in checkout;
body: Button tap was not firing due to overlay z-index blocking touch events on Safari iOS.;
footer: NOJIRA;
```

**Example (refactor, Tickets scope):**

```
type: refactor;
scope: Tickets;
summary: Extract ticket validation into shared service;
body: Centralise validation logic for reuse across POS and kiosk to avoid drift.;
footer: FIS-456;
```

---

## Invalid Examples

- **Semicolon inside a field:** `summary: Fix bug; in checkout;` — do not use `;` inside summary, body, or scope.
- **Wrong type:** `type: chore;` — only feat, fix, perf, refactor, test are allowed.
- **Vague summary:** `summary: Fixed the button bug;` — be specific (which button, what behaviour, which context).
- **Missing fields:** omitting body or footer — all five fields are required.
- **Made-up scope:** `scope: auth;` when “auth” is not in [references/scopes.md](references/scopes.md) — use only scopes from the list or **Other**.

---

## Output

Output the commit message **explicitly as plain text**:

- No markdown (no headers, no bold, no backticks).
- No code block wrapper.
- No extra commentary before or after the message.
- **Every line must include the field label:** `type: `, `scope: `, `summary: `, `body: `, `footer: ` — do not output only values or a single line with semicolons. Example: `footer: NOJIRA;` not just `NOJIRA`.
- Exactly 5 lines, in order: `type: …;`, `scope: …;`, `summary: …;`, `body: …;`, `footer: …;`. **No blank lines between the five lines** — each line immediately followed by a single newline (product did not require blank lines; this keeps the format compact and unambiguous for parsing).
- Ready to paste into `git commit` (multiline message).

---

## Validation

Repos may enforce this format via:

- **Local:** `npx @smeetz/dev-standards commit` (Husky + Commitlint) — run from repo root.
- **Server:** Bitbucket Push Checkers by regex as a second line of defence.

This skill defines the format; validation enforces it. When validation is set up, commit messages that do not match the schema will be rejected.
