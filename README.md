# Openclaw-PR Workflow

Safe phase-based workflow for OpenClaw pull request agents.

[Quick start](#quick-start) | [Phases](#phases) | [Safety](#safety) | [Files](#files) | [Install](#install)

## Overview

`openclaw-pr-workflow` helps an agent work on OpenClaw pull requests without jumping ahead. It separates discovery, ownership checks, inspection, patching, proof, PR body work, and publishing into explicit phases.

Use it when you want a conservative OpenClaw PR agent that asks before it reads wider, patches, tests, comments, commits, pushes, or publishes.

## Quick Start

```text
Use openclaw-pr-workflow. Phase 0.
Use openclaw-pr-workflow. Phase 2 OpenClaw.
Use openclaw-pr-workflow. Phase 3 openclaw/openclaw#12345.
Use openclaw-pr-workflow. Phase 12 openclaw/openclaw#12345.
```

The skill invocation name is:

```text
openclaw-pr-workflow
```

## Phases

```text
STARTTEST -> ORIENT -> SCOUT -> GATE -> INSPECT -> HYGIENE -> PATCH -> PROOF -> PR-BODY -> PUBLISH
```

The important rule is simple:

```text
One phase does not authorize the next phase.
```

Examples:

- `SCOUT-GO` allows read-only issue and PR metadata only.
- `GATE-GO` allows ownership and duplicate checks only.
- `PATCH-GO` allows only the approved minimal change.
- `PROOF-GO` allows only the named proof.
- `PUBLISH-GO` allows only the exact named write action.

## Safety

- No server, SSH, terminal, file, test, build, service, config, firewall, install, update, cleanup, GitHub, patch, commit, push, or PR action without the matching GO.
- Read-only phases may inspect only the approved scope.
- Write phases require exact operator approval.
- If the operator says stop, wait, inactive, or no commands, the agent does nothing.
- Secrets and private data must not be printed.

## Files

```text
SKILL.md
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

## Install

Clone or copy this folder into your skills directory, then invoke the skill by name:

```text
openclaw-pr-workflow
```

## License

MIT
