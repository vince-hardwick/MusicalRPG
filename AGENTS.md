# Agent instructions

## Agent skills

### Issue tracker

Issues and specs live in GitHub Issues. For tracker operations,
read `docs/agents/issue-tracker.md`.

### Triage labels

Use the five default triage roles. For their mapping and meanings,
read `docs/agents/triage-labels.md`.

### Domain docs

Use a single-context layout. Before exploring domain concepts or
design decisions, read `docs/agents/domain.md`.

## Scratch files

Store untracked repository scratch artefacts only in the existing
`scratch/` directory at the repository root. If it is absent, stop and
ask where to work.

Use `scratch/` for ephemeral or disposable files, including archived/cold
or disposable single-use handoff documents. It is not a general store
for active working records.

This location overrides alternative scratch or temporary locations in
invoked skills, including the handoff skill's OS temporary directory.

Do not treat every ignored path as disposable scratch.

## Closeout

End every final response with a concise recommended next action supported by the task's routed owners.