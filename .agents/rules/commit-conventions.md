# Commit conventions

Load this when you're about to commit staged or unstaged changes.

## Format

```
type(scope): short imperative description

Optional body explaining the why, not the what.

Assisted-by: <harness>:<model>
```

## Commit types

`feat`, `fix`, `refactor`, `docs`, `chore`, `style`, `test`, `perf`, `ci`, `build`

## Rules

- First line under 72 characters.
- Imperative mood ("add" not "added").
- Scope in parentheses is optional but preferred when the change is
  localized (e.g., `docs`, `skills`, `deployment`).
- Stage files by name — never `git add -A` or `git add .`.
- Never commit likely-secret files (`.env`, credentials, `.pem` keys) or
  `.DS_Store`.
- Never skip hooks (`--no-verify`); never amend a commit unless explicitly
  asked.
- On an AI-assisted commit, add an `Assisted-by: <harness>:<model>` trailer
  — see [AI_POLICY.md](../../AI_POLICY.md) for the full disclosure policy.
  Never `Co-authored-by:` for a tool, never `Signed-off-by:` from an agent.
- No "Generated with..." or similar marketing lines — this is attribution,
  not promotion.
