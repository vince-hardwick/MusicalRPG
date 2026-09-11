# Issue tracker: GitHub

Issues and specs live in GitHub Issues. Use the `gh` CLI, resolving
the repository from the Git remote.

## Operations

- Read an issue with `gh issue view <number> --comments`; include its
  labels when assessing its state.
- List issues with `gh issue list`, using state and label filters
  appropriate to the task.
- Create issues with `gh issue create`.
- Add comments with `gh issue comment <number>`.
- For multiline bodies, write the text to a file and use `--body-file`.
- Apply or remove labels with `gh issue edit <number> --add-label`
  or `--remove-label`.
- Close completed issues with `gh issue close <number>`.

When a skill says to publish to the issue tracker, create a GitHub
issue. When it says to fetch a ticket, read that issue and its comments.

## Pull requests as a triage surface

PRs as a request surface: no.

## Wayfinding operations

- Map: one issue labelled `wayfinder:map`.
- Child ticket: a native GitHub sub-issue of the map, labelled
  `wayfinder:research`, `wayfinder:prototype`, `wayfinder:grilling`
  or `wayfinder:task`.
- If sub-issues are unavailable, link each child in a task list in
  the map and include `Part of #<map>` in the child.
- Blocking: use native GitHub issue dependencies. The dependency API
  requires the blocker's database issue ID, not its issue number.
  If dependencies are unavailable, use `Blocked by: #<number>` in
  the child.
- Frontier: select open, unassigned children with no open blockers,
  in map order.
- Claim: assign the selected ticket to the driving developer before
  starting work.
- Resolve: comment with the answer, close the ticket, and add a
  brief linked pointer to the map's Decisions so far.
