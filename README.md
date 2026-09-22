# harness-the-cryosphere

A domain-specific **agent harness** for cryospheric science — a system that wraps
an AI agent loop with domain-specific verification, rules, and memory, so that
AI-assisted scientific workflows are trustworthy and reproducible rather than
ad hoc.

Built on [OpenJarvis](https://github.com/open-jarvis/OpenJarvis), a local-first
agent framework that supports open-weight models alongside proprietary APIs.

## The concept

Building an AI agent has two parts. First, the generic plumbing: the loop that
lets the agent think, act, and observe results; how it calls tools; how it
manages what it remembers during a task. That part is largely a solved
problem — existing frameworks handle it, and there's little value in
rebuilding it from scratch. Second, the part that's specific to a field of
science: what counts as a correct answer, what mistakes are known to happen,
and what rules and checks catch those mistakes. That second part is where
this project's real effort goes — building that layer for cryospheric
science specifically.

Key ideas underpinning the design:

- **Three layers: model + generic plumbing + domain layer.** The generic
  architecture (the agent's think/act loop, tool calling, memory management) is
  off-the-shelf and increasingly handled well by existing frameworks. The
  domain layer (rules for what's correct, checks for known mistakes) is built
  on top of that architecture, using its extension points like skills and
  hooks, but the content itself has to be written by people who understand
  the science.
- **Turn every mistake into a permanent check.** When something goes wrong
  once, don't just fix it and move on. Instead, turn it into a rule, a hook, or a
  test that runs automatically every time from then on. This is how the
  hard-won judgment of experienced scientists becomes something the system
  itself remembers, instead of a lesson that's forgotten once someone leaves
  or moves on.
- **The agent that produces an answer shouldn't be the one that grades it.**
  Letting a system check its own work is inherently biased toward saying
  "looks good." Checking needs to happen independently, via a second agent, or a
  second person, comparing the result against clear, predefined criteria.
- **Hooks.** Small checks wired into specific moments in the agent's workflow, for example, after it does a calculation, before it accepts an input, when it thinks it's done, that run automatically every time, regardless of who's
  operating the agent. This is how the "turn every mistake into a permanent
  check" idea actually gets enforced in practice.
- **Reproducibility matters.** Unlike most software, a published scientific
  result needs to be traceable back to the exact version of the tooling,
  rules, and checks that produced it, even as all of that keeps changing and
  improving over time.
- **Better models don't replace domain rules.** As underlying AI models
  improve, some of the generic plumbing becomes unnecessary (forcing the
  model to reason step-by-step, rigid tool templates). But the field-specific
  rules and checks don't go away. They're not a workaround for a weaker
  model, they're just facts about what counts as correct in that field.
- **Ralph loop** (a pattern for tasks too long for one sitting): rather than
  trying to keep everything in the agent's working memory across a long
  task, progress is written to a file on disk. A check re-reads that file and
  restarts the agent with a fresh, focused view of what's left to do, pass
  after pass, until the task is finished.
- **ReAct loop:** the basic think → act → observe cycle that most AI agents
  use to complete a task, including this project's default agent type. It's
  intentionally simple, and the real engineering is everything built around it
  (the hooks, the checks, which tools it's given).

## Why OpenJarvis

We selected [OpenJarvis](https://github.com/open-jarvis/OpenJarvis) because it fits the requirement to support **open-weight models**,
not just proprietary APIs:

- Local-first agent framework (Stanford Hazy Research / Scaling Intelligence
  Lab, Intelligence Per Watt initiative).
- Unified `Engine` interface behind four local backends (Ollama, vLLM, SGLang,
  llama.cpp) and five cloud backends (Anthropic, OpenAI, Gemini, OpenRouter,
  MiniMax) — lets us prototype against a strong hosted model, then swap to an
  open model as a config change, without rewriting skills/MCP servers/hooks.
- Eight built-in agent types across three execution modes (on-demand,
  scheduled, continuous), including a plain `native_react` loop, an
  orchestrator with automatic tool selection, a continuous long-horizon
  "operative," and a CodeAct-style coder.
- Skills follow the open [agentskills.io](https://agentskills.io) standard (a
  `SKILL.md` plus optional reference files/scripts) — low barrier for domain
  scientists to author directly.
- Ships its own evaluation framework treating accuracy, cost, latency, and
  energy as joint first-class metrics.

## Status

Early prototype stage. See [.agents/progress.md](.agents/progress.md) for
current status and next steps.


