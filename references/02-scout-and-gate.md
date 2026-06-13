# Scout And Gate

## SCOUT Purpose

Find current, editable OpenClaw PR candidates for bug or stability work.
Do not patch, do not prove, do not inspect code, and do not write a blocker catalog.

## OpenClaw Starting Point

Preferred OpenClaw scout starting point:

```text
openclaw/openclaw#84599
```

Treat it as a dashboard/filter source, not a fix target.

Verify the starting point as a current working source.
If `openclaw/openclaw#84599` is closed, stale, empty, contradicted, or replaced by the operator or maintainers:
- stop
- report the problem briefly
- ask for the current dashboard/filter source
- do not guess a new source

Search windows:
1. Ready-to-queue fixes: no linked PR.
2. Clear-shape fixes: no linked PR.
3. Small clear-shape fixes: no linked PR.
4. Ready fixes with source repro: no linked PR.
5. Ready fixes by impact: security, data-loss, message-loss, crash-loop, auth/provider, session-state.
6. Then P0/P1/Beta/Regression/Crash.

SCOUT may check multiple defined search windows in one read-only pass until:
- up to 3 candidates are found, or
- the checked window can be reported as empty/blocker-heavy.

This does not authorize GATE, INSPECT, code reads, checkout use, patch, proof, or GitHub write.

## Freshness

Default:
- Prefer activity from the last 7 days.

Fresh activity includes:
- new label
- ClawSweeper comment
- maintainer comment
- new linked PR
- reopen
- new repro
- beta/release relevance
- dashboard mention

Older issues only qualify when:
- dashboard-current
- operator-named
- maintainer/ClawSweeper-current
- beta/release-current
- fresh queue/fix-shape/source-repro signal

Old without exception:
- `DROP-old`
- one line
- no analysis

## Drop Rule

Drop immediately on:
- hard stop label
- open linked/canonical PR
- maintainer or ClawSweeper counter-direction
- obviously blocking ownership
- wrong layer
- too old without freshness exception

Drop output:

```text
#12345: DROP, open canonical PR #99999.
```

No long problem description for drops.

## Stop Labels

Hard stop labels:

```text
clawsweeper:no-new-fix-pr
clawsweeper:needs-maintainer-review
clawsweeper:needs-product-decision
clawsweeper:needs-security-review
clawsweeper:needs-live-repro
clawsweeper:needs-info
```

Continue only when the operator explicitly chooses that blocked issue for Blocked-Path-Review.

## Scout Output

Maximum 3 candidates, maximum 5 drops.

```text
Phase: SCOUT
Search window:
Checked:

Candidate 1:
Issue:
Freshness: activity <= 7 days | dashboard-current | operator-named
Why interesting:
Free signals:
Blocker check:
Status: LIKELY FREE | UNCLEAR

Drops:
- #...: DROP, <one-line reason>.

Next GO:
Recommended:
- <copyable next command>
Why:
- <one sentence>
Alternatives:
- WAIT
```

Do not write:

```text
There are no open issues to work on.
```

Unless the operator requested a true exhaustive search and the full defined search space was verifiably checked.

## Ownership Gate

GATE decides exactly one candidate:

```text
Ownership Gate: FREE | BLOCKED | UNCLEAR
```

Only `FREE` allows the next phase.
`FREE` is not PATCH-GO.

## Required Gate Searches

All searches are live/read-only:
1. Issue directly.
2. Issue comments.
3. Open PRs by issue number.
4. Open PRs by `Fixes #<issue>`.
5. Open PRs by `Closes #<issue>`.
6. Open PRs by symptom keywords.
7. Open PRs by exact error message, if available.
8. Open PRs by likely files/functions, if known.
9. Closed/merged PRs when canonical/superseding/approved.
10. Maintainer or ClawSweeper direction.
11. Assignee, claim, owner hints.
12. Stop labels.

With GATE-GO, all required searches for exactly one candidate may run in one read-only pass.
This does not authorize code deep dive, patch planning, checkout, proof, tests, or GitHub write.

## Gate Decisions

FREE:
- issue is open or clearly canonical
- no open/canonical/superseding PR
- no owner/assignee/claim blocker
- no maintainer or ClawSweeper counter-direction
- no hard stop label
- fix layer seems appropriate
- all required searches ran

BLOCKED:
- open/canonical/superseding PR found
- maintainer/ClawSweeper names another direction
- hard stop label
- assignee/claim/owner blocks it
- issue is closed/superseded

UNCLEAR:
- required search could not run
- contradictory results
- possible overlap with another PR
- unclear fix layer
- unclear maintainer direction
- stale without clean freshness exception

## Gate Output

```text
Phase: GATE
Candidate:
Ownership Gate: FREE | BLOCKED | UNCLEAR

Issue:
- status:
- freshness:
- labels:

Issue comments:
- relevant direction:

Open PR duplicate search:
- by issue number:
- by Fixes/Closes:
- by symptom:
- by error text:
- by files/functions:

Closed/canonical search:
- result:

Claim/assignee/maintainer direction:
- result:

Stop labels:
- result:

Decision:
- FREE/BLOCKED/UNCLEAR because ...

Next only with Operator OK:
Recommended:
- <copyable next command>
Why:
- <one sentence>
Alternatives:
- WAIT
```

If not clearly FREE:

```text
STOP.
Do not build.
Do not prove.
Do not argue.
```
