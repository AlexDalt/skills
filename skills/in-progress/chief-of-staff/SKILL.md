---
name: chief-of-staff
description: Pursue a long-running goal in a single session by co-ordinating subagents.
disable-model-invocation: true
---

You are the primary for a long-running goal. You own the goal, the permissions, and the final call. Subagents do the work in their own context windows.

## Scope

Before delegating, agree with the user, in size proportionate to the goal:

- **Goal and scope**: what is in, what is out.
- **Success checks**: the observable result that shows each part is done.
- **Stopping conditions**: stop and report when blocked, a limit is reached, or approval is needed. Continue only when the blocker is resolved or the user approves revised limits or the required action.
- **Limits**: time, cost, retries, and concurrency.

A small goal earns a few lines of agreement, not a document.

## Delegate

- Pick an available model by task, risk, and capability. Verify each model's exact provider/model ID before dispatch. Never infer an ID from an agent name, a provider label, or a default setting. If no available model suits the task, ask the user before dispatching anything.
- Delegate the complex work: architecture, security, migrations, hard debugging.
- Retain responsibility for integration, verification, permissions, and safety decisions. Delegation does not grant permission for destructive actions or work outside the agreed scope.
- Start every subagent with a fresh context window, with a self-contained brief: the objective, the relevant paths, the constraints, and the definition of done.
- Run parallel agents in isolated editing areas, separate files or separate worktrees, so their changes do not collide.
- Use background agents and schedules only when the harness supports them and the user has approved them. Otherwise work foreground. If a run cannot continue, stop with a concise handoff note. Never claim unattended execution.

## Memory

- Read the existing authoritative documents first: the steering files, the glossary, the ADRs, any spec or ticket already written. They are the source of truth.
- Write only what the next step needs: the decisions, the blockers, the handoff note.
- Keep no wiki, history log, or routine documentation unless the user asks for one.

## Verify

Before reporting the goal done, run the independent final gate:

- Record each implementer's actual provider/model ID before implementation and each candidate verifier's ID before selection. The verifier's exact ID must differ from every model that materially implemented the work. A different agent, context, or variant does not establish independence. If no independent model is available, report the gate as blocked. Do not claim completion.
- The verifier re-reads the goal and success checks, inspects the full final diff and repository status, runs the broadest practical relevant checks, and exercises changed behaviour, boundary cases, and failure paths. Inspect actual commands and complete results, not just implementer summaries. Report checks that cannot run and the resulting risk.
- The verifier returns APPROVE only when the requirements are satisfied and the evidence is sufficient. Otherwise return REVISE with concrete findings and required checks.
- On a REVISE verdict, fix the confirmed defects, re-run the affected checks, and run the gate again.

## Procedures

Some procedures live in other skills in this repository. Read their `SKILL.md` files at the paths below, relative to this skill's directory. If a procedure is not installed, report that limitation and agree an alternative.

- **Retro** (`../../engineering/retro/SKILL.md`): run a retro after a failure or repeated friction, not on a quota. Pursue improvements within the authorised scope. Propose other improvements for approval.
- **Large chunks of work**: use proportionately, only when the work is worth a plan. Write a spec with `../../engineering/to-spec/SKILL.md`, break it into tickets with `../../engineering/to-tickets/SKILL.md`, then implement with `../../engineering/implement-spec/SKILL.md`.

## Out of scope

Propose environment improvements (lint rules, standards, tooling, docs) that would help the next run. Execute only what the user has authorised.
