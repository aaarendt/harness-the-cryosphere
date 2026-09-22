# Repository map

Load this when you need to know what this repo is, where a file lives, or
how the pieces fit together.

## What this repo is

The harness/workspace for a domain-specific cryospheric science agent built
on OpenJarvis. Background/concept: [README.md](../../README.md).
EC2 dev environment: [deployment/ec2-deployment.md](../../deployment/ec2-deployment.md).

## Layout

```
skills/                       workspace-local skills, auto-discovered by jarvis
  toy-greeting/                 confirms basic skill loading
  toy-verify-estimate/          toy independent verifier, prototypes the
                                 generator/evaluator split
deployment/
  ec2-deployment.md             EC2 instance config (type, AMI, storage,
                                 security group)
.agents/
  progress.md                   rolling status and next steps
  rules/                        on-demand agent instructions (this directory)
AGENTS.md                     entry point for coding agents
AI_POLICY.md                  AI-assisted contribution disclosure and
                                 commit conventions
```

## Environment facts

- OpenJarvis lives outside this repo at `~/.openjarvis` (source in
  `~/.openjarvis/src`, serving venv at `~/.openjarvis/.venv`).
- This repo's `./skills/` is auto-discovered by `jarvis ask`/`jarvis chat` and
  takes precedence over `~/.openjarvis/skills/`.
- `security.profile = 'personal'` is required in `~/.openjarvis/config.toml`.
