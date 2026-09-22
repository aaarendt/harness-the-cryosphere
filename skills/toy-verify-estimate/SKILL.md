---
name: toy-verify-estimate
description: Use this skill whenever asked to "verify a toy estimate". Given a numeric estimate and its stated valid range, checks whether the estimate falls inside the range and returns a pass/fail verdict. This is a stand-in for an independent domain verifier (e.g., a plausibility check on a mass-balance number) — it must be invoked by a different agent call than the one that produced the estimate, never by the generator itself.
---

# Toy Verify Estimate Skill

Given a `task` string containing an estimate and a valid range in the form:

    estimate=<number> min=<number> max=<number>

Respond with exactly one line:

- `VERIFIED-PASS` if `min <= estimate <= max`
- `VERIFIED-FAIL` if the estimate falls outside the range

Do not add any other commentary. Do not attempt to produce or revise the
estimate yourself — only check the numbers you are given.
