# Progress

Rolling status and next steps for this project. Update this file as work
progresses — read it at the start of a session, write back to it before
finishing one.

## Confirmed working

- OpenJarvis installed and running (see [deployment/ec2-deployment.md](../deployment/ec2-deployment.md)
  for environment setup, [.agents/rules/troubleshooting.md](rules/troubleshooting.md)
  for known setup/build gotchas).
- Bare `native_react` agent launch: `jarvis ask -a native_react "<query>"` or
  `jarvis chat -a native_react`.
- Workspace-local skill discovery confirmed end-to-end via the two toy
  skills under [skills/](../skills/):
  - [skills/toy-greeting/SKILL.md](../skills/toy-greeting/SKILL.md) — confirms basic skill loading.
  - [skills/toy-verify-estimate/SKILL.md](../skills/toy-verify-estimate/SKILL.md) — a toy
    independent verifier, prototyping the generator/evaluator split.
- No first-class "hooks" system exists in OpenJarvis — see
  [.agents/rules/troubleshooting.md](rules/troubleshooting.md).

## Next steps

1. Write a generator-side skill to pair with
   [skills/toy-verify-estimate/SKILL.md](../skills/toy-verify-estimate/SKILL.md),
   completing the generator/evaluator split prototype.
2. Decide which hook analog to build the "turn every mistake into a
   permanent check" idea on: `confirm_callback`, `CapabilityPolicy`
   (`openjarvis/security/capabilities.py`), or a skills-based verifier
   pattern (currently the leading candidate, since skill loading is already
   proven).
3. Wire in an Anthropic API key via the `cloud` engine to validate the
   engine-swap mechanism before touching real cryosphere data.
4. Move to a real toy pilot: one narrow cryosphere task (e.g., a single
   glacier basin mass-balance step) with one real skill and one real
   verifier.
