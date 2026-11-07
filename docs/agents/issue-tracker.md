# Issue tracker: GitHub

Issues and specs live in GitHub Issues in `AlexDalt/skills`.
Use the `gh` CLI from this repo.

## Conventions

- Create: `gh issue create --title "..." --body-file <file>`.
- Read: `gh issue view <number> --json number,title,body,labels,comments`.
- List: `gh issue list --state open --json number,title,body,labels`.
- Comment: `gh issue comment <number> --body "..."`.
- Apply or remove labels: `gh issue edit <number> --add-label "..."`
  or `--remove-label "..."`.
- Close: post an explanation with `gh issue comment`, then use
  `gh issue close <number>`. For rejections, use `--reason "not planned"`.

Before the first issue creation of a session, check
`gh repo view --json nameWithOwner`. The target must be `AlexDalt/skills`;
if it differs, use `--repo AlexDalt/skills` explicitly.

## Parent issues and blocking

Use GitHub native sub-issues and issue dependencies where available.

With gh 2.94+:
- Create a child: `gh issue create --parent <parent> ...`.
- Attach an existing child:
  `gh issue edit <parent> --add-sub-issue <child>`.
- Add a blocker:
  `gh issue edit <child> --add-blocked-by <blocker>`.

With older gh, use the GitHub API:
- Attach a child:
  `gh api --method POST repos/AlexDalt/skills/issues/<parent>/sub_issues -F sub_issue_id=<child-db-id>`.
- Add a blocker:
  `gh api --method POST repos/AlexDalt/skills/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`.

Get database IDs with
`gh api repos/AlexDalt/skills/issues/<number> --jq .id`.
These are database IDs, not issue numbers or node IDs.

Where native relationships are unavailable, put `Part of #<parent>`
and `Blocked by: #<n>, #<n>` at the top of the child body.
A child is unblocked when every blocker is closed.

Count open native blockers with
`gh api repos/AlexDalt/skills/issues/<number> --jq .issue_dependencies_summary.blocked_by`.

## Pull requests as a triage surface

**PRs as a request surface: no.**

## Skill operations

“Publish to the issue tracker” means create a GitHub issue.
“Fetch the relevant ticket” means read that issue.

## Wayfinding operations

- Map: one issue labelled `wayfinder:map`, holding Notes,
  Decisions-so-far, and Fog.
- Child: a sub-issue labelled `wayfinder:<type>`, where type is
  `research`, `prototype`, `grilling`, or `task`.
- Frontier: open children in map order with no open blockers
  and no assignee.
- Claim: `gh issue edit <number> --add-assignee @me`.
- Resolve: comment with the answer, close the child, and append
  a gist and link to the map's Decisions-so-far.
