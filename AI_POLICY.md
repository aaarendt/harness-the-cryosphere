# AI Policy

AI-assisted contributions are welcome in this repo. Contributors (including
the maintainer) should:

- Disclose that AI was used and name the harness and model in the pull
  request or commit description.
- Review and understand every line submitted — the human contributor is
  responsible for it, not the AI.
- Meet the same quality and correctness standards as any other change,
  especially for domain rules and verification criteria (see
  [README.md](README.md)) — an AI-assisted change is not exempt from the
  generator/evaluator split this project itself is built around.
- Not use fully autonomous agents to open issues or pull requests unattended.
- Respond to reviewers directly, in your own words.
- Clearly mark AI-generated text in descriptions, issues, and comments.

This applies to issues and comments as well as pull requests. Using AI for
translation or grammar help is fine and doesn't need disclosure.

## Crediting AI assistance in commits

Only humans can be named as co-authors, and AI can never sign off on a
commit. Credit AI assistance with a trailer naming the coding agent (a
lowercase, hyphenated slug) and the model identifier it reports, joined by a
colon:

```
Assisted-by: <harness>:<model>
```

For example:

```
Assisted-by: github-copilot:claude-sonnet-5
```

Use the same harness/model string in the commit trailer and in any pull
request disclosure so they agree.
