# Openclaw-PR Workflow

**Safe phase-based workflow for OpenClaw pull request agents**

This is a compact Codex skill for agents working on OpenClaw pull requests. It keeps PR work split into explicit phases so an agent can scout, inspect, patch, prove, and publish without jumping ahead.

Use it when you want careful OpenClaw PR work with read-only discovery first, operator approval between phases, and reusable templates for proof notes and PR bodies.

<p align="center">
  <a href="SKILL.md"><strong>Skill file</strong></a>
  &nbsp;|&nbsp;
  <a href="docs/INSTALL.md"><strong>Install</strong></a>
  &nbsp;|&nbsp;
  <a href="docs/WORKFLOW.md"><strong>Workflow guide</strong></a>
  &nbsp;|&nbsp;
  <a href="references/04-output-templates.md"><strong>Output templates</strong></a>
  &nbsp;|&nbsp;
  <a href="references/05-pr-body-template.md"><strong>PR body template</strong></a>
  &nbsp;|&nbsp;
  <a href="references/07-maintainer-test.md"><strong>Maintainer test</strong></a>
</p>

## What It Covers

| Area | Purpose |
| --- | --- |
| Scout and gate | Find candidates and check ownership before touching code. |
| Inspect and patch | Read narrowly, plan the smallest safe change, then patch only after GO. |
| Proof and publish | Run proof, prepare PR notes, and publish only the exact approved action. |

## Quick Start

Ask Codex to use the skill by name:

```text
Use openclaw-pr-workflow. Phase 0.
Use openclaw-pr-workflow. Phase 2 OpenClaw.
Use openclaw-pr-workflow. Phase 3 openclaw/openclaw#12345.
```

The detailed phase guide lives in [docs/WORKFLOW.md](docs/WORKFLOW.md).

## Repository Map

| Path | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Main skill entry file. |
| [docs/WORKFLOW.md](docs/WORKFLOW.md) | Full README-style guide with phases, stop conditions, and usage patterns. |
| [references/](references/) | Safety rules, phase details, templates, and failure-pattern notes. |
| [agents/openai.yaml](agents/openai.yaml) | Agent metadata/config included with the skill package. |

## License

MIT. See [LICENSE](LICENSE).
