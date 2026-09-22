# Agent instructions for this repo

Guidance for AI coding agents working with this repository. This file is
the entry point and is deliberately short — detailed rules live under
[.agents/rules/](.agents/rules/) and are loaded on demand: read the one
whose trigger matches your current task, not all of them.

## Non-negotiables

- No first-class hooks system exists in OpenJarvis; use `confirm_callback`,
  `CapabilityPolicy`, or a skills-based verifier instead.
- Energy-aware evals must run on local hardware with real power monitoring —
  not on a cloud VM.

## Rule index

| File | Load when... |
| --- | --- |
| [.agents/rules/repository-map.md](.agents/rules/repository-map.md) | You need to know what this repo is, where a file lives, or what the environment looks like. |
| [.agents/rules/commit-conventions.md](.agents/rules/commit-conventions.md) | About to commit staged or unstaged changes. |
| [.agents/rules/troubleshooting.md](.agents/rules/troubleshooting.md) | A documented setup/build command fails or behaves unexpectedly. |
