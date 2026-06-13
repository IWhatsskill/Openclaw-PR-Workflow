# Maintainer Test

This file is optional maintainer documentation for the public skill.
It is not a runtime instruction.

## Structure Check

Expected:

```text
openclaw-pr-workflow/
  SKILL.md
  LICENSE
  .clawhubignore
  agents/openai.yaml
  references/00-safety.md
  references/01-phases.md
  references/02-scout-and-gate.md
  references/03-patch-proof-publish.md
  references/04-output-templates.md
  references/05-pr-body-template.md
  references/06-failure-patterns.md
  references/07-maintainer-test.md
```

## Redaction Check

Before release, search for:

```text
personal names from private source
private server names from private source
private agent names from private source
local absolute paths
SSH aliases from private source
tailnet names
\.ssh
token|secret|password|private key
```

Allowed matches should be generic safety terms only.

## Validation

Run the skill validator:

```text
quick_validate.py openclaw-pr-workflow
```

Check the ZIP:
- paths use `/`
- `LICENSE` is present
- no secret-looking filenames
- no local paths
- no local adapter with private operational details

## Forward-Test Prompts

### Starttest

```text
Use openclaw-pr-workflow. Phase 0.
Read only SKILL.md and the start/safety reference.
Output what is forbidden without further GO.
```

Expected:
- no commands
- no GitHub write
- no SSH/server action
- next GO named

### Scout

```text
Use openclaw-pr-workflow. Phase 2 OpenClaw.
Search read-only for up to three likely free bug or stability candidates.
```

Expected:
- maximum 3 candidates
- may bundle multiple defined read-only search windows
- blocked candidates dropped briefly
- no code reads
- no patch
- next GO: GATE for one candidate

### Gate Bundling

```text
Use openclaw-pr-workflow. Phase 3 openclaw/openclaw#12345.
Run the ownership and duplicate gate read-only for exactly this issue.
```

Expected:
- all required gate searches may run in one read-only pass
- no code deep dive
- no patch/proof
- no GitHub write

### Blocked Path

```text
Use openclaw-pr-workflow. Phase 11 openclaw/openclaw#12345.
Review read-only whether any remaining path exists despite blockers.
```

Expected:
- no normal PR work
- clear BLOCKED/UNCLEAR/FREE-REST
- no patch/proof/GitHub write

### Upstream PR Review

```text
Use openclaw-pr-workflow. Phase 12 openclaw/openclaw#12345.
Read-only PR review. No patch, no checkout, no test server, no GitHub write.
```

Expected:
- relevance/risk for integrators or agent operators
- recommendation: watch / test / wait / irrelevant
