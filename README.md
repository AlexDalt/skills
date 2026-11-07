# Skills

Agent skills: slash commands and behaviors for real engineering. This is a customised fork of [mattpocock/skills](https://github.com/mattpocock/skills), living at [AlexDalt/skills](https://github.com/AlexDalt/skills), tuned to my own tastes and workflows.

Skills split on one axis: who can invoke them. **User-invoked** skills are reachable only when you type them (e.g. `/grill-me`); their job is to orchestrate. **Model-invoked** skills can be invoked by you _or_ reached for automatically by the agent when the task fits; they hold the reusable discipline.

## Commands

### Engineering

Skills for daily code work.

**User-invoked**

- **`/ask-matt`**: [ask-matt](./skills/engineering/ask-matt/SKILL.md): ask which skill or flow fits your situation. A router over the user-invoked skills in this repo.
- **`/grill-with-docs`**: [grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md): a relentless interview to sharpen a plan or design, which also builds the project's domain model (sharpening terminology and updating `GLOSSARY.md` and ADRs) as it goes.
- **`/triage`**: [triage](./skills/engineering/triage/SKILL.md): move issues through a state machine of triage roles. For incoming work you didn't create: bug reports, feature requests, anything that arrives raw.
- **`/improve-codebase-architecture`**: [improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md): scan a codebase for deepening opportunities, present them as a visual HTML report, then grill through whichever one you pick.
- **`/setup`**: [setup](./skills/engineering/setup/SKILL.md): configure this repo for the engineering skills (issue tracker, triage label vocabulary, domain doc layout). Run once per repo before using the other engineering skills.
- **`/to-spec`**: [to-spec](./skills/engineering/to-spec/SKILL.md): turn the current conversation into a spec and publish it to the issue tracker. No new interview, just synthesise what you've already discussed.
- **`/to-tickets`**: [to-tickets](./skills/engineering/to-tickets/SKILL.md): break any plan, spec, or conversation into a set of tracer-bullet tickets, each declaring its blocking edges, written as text in a local file, or as native blocking links on a real tracker.
- **`/implement`**: [implement](./skills/engineering/implement/SKILL.md): build the work described by a spec or a single ticket, driving `/tdd` at pre-agreed seams and closing out with `/code-review`.
- **`/implement-spec`**: [implement-spec](./skills/engineering/implement-spec/SKILL.md): implement a whole spec on one integration branch. Works the tickets as a task graph, running implementer subagents across the ready frontier for maximum concurrency, then closes out with `/code-review`.
- **`/wayfinder`**: [wayfinder](./skills/engineering/wayfinder/SKILL.md): plan a huge, multi-session effort as a shared map of decision tickets on the issue tracker, and resolve them one at a time until the way to the destination is clear.
- **`/retro`**: [retro](./skills/engineering/retro/SKILL.md): after a session, suggest improvements to the coding agent's environment (navigation, automated checks, coding standards, steering files, tooling), most severe first.

**Model-invoked**

- **`/prototype`**: [prototype](./skills/engineering/prototype/SKILL.md): build a throwaway prototype to answer a design question, either a single shareable HTML file for state/logic questions, or several radically different UI variations toggleable from one route.
- **`/diagnosing-bugs`**: [diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md): disciplined diagnosis loop for hard bugs and performance regressions: build a tight feedback loop that goes red on this bug, then minimise, hypothesise, instrument, fix, regression-test.
- **`/research`**: [research](./skills/engineering/research/SKILL.md): investigate a question against high-trust primary sources and capture the findings as a cited Markdown file in the repo, run as a background agent.
- **`/tdd`**: [tdd](./skills/engineering/tdd/SKILL.md): test-driven development with a red-green-refactor loop. Builds features or fixes bugs one vertical slice at a time.
- **`/domain-modeling`**: [domain-modeling](./skills/engineering/domain-modeling/SKILL.md): actively build and sharpen a project's domain model: challenge terms against the glossary, stress-test with edge-case scenarios, and update `GLOSSARY.md` and ADRs inline.
- **`/codebase-design`**: [codebase-design](./skills/engineering/codebase-design/SKILL.md): shared discipline and vocabulary for designing deep modules: a lot of behaviour behind a small interface, placed at a clean seam, testable through that interface.
- **`/code-review`**: [code-review](./skills/engineering/code-review/SKILL.md): two-axis review of the diff since a fixed point, **Standards** (repo coding standards, plus a Fowler smell baseline) and **Spec** (does it faithfully implement the originating issue/spec), run as parallel subagents so neither pollutes the other.
- **`/pr`**: [pr](./skills/engineering/pr/SKILL.md): the shape a pull request body should take: a summary as the smallest visual that makes the change clear, before/after evidence that it works, and a merge-danger call (one-way or two-way door, plus blast radius).
- **`/wizard`**: [wizard](./skills/engineering/wizard/SKILL.md): generate an interactive bash wizard that walks a human through steps only they can perform: provisioning infrastructure, setting up credentials or CI secrets, walking an unfamiliar third-party dashboard, or running a one-off migration or cutover.

### Productivity

General workflow tools, not code-specific.

**User-invoked**

- **`/grill-me`**: [grill-me](./skills/productivity/grill-me/SKILL.md): get relentlessly interviewed about a plan or design until every branch of the design tree is resolved.
- **`/handoff`**: [handoff](./skills/productivity/handoff/SKILL.md): compact the current conversation into a handoff document so another agent (or a fresh harness, directory, or colleague) can continue the work.
- **`/teach`**: [teach](./skills/productivity/teach/SKILL.md): teach the user a new skill or concept over multiple sessions, using the current directory as a stateful teaching workspace.
- **`/to-questionnaire`**: [to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md): turn a decision you can't answer alone into a Markdown questionnaire for the one person who can, filled in async, or together over a meeting. It grills you about the send (who it's for, what you need back), not the subject.
- **`/wait-what`**: [wait-what](./skills/productivity/wait-what/SKILL.md): fire this the moment a message doesn't land. The agent re-pitches it with the context you're missing, in plain English, using your `GLOSSARY.md` vocabulary.

**Model-invoked**

- **`/grilling`**: [grilling](./skills/productivity/grilling/SKILL.md): interview the user relentlessly about a plan, decision, or idea until every branch of the design tree is resolved. The reusable interview primitive behind `grill-me`, `grill-with-docs`, `triage`, `wayfinder`, and `improve-codebase-architecture`.
- **`/writing-for-agents`**: [writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md): writing documents for agents: skills, AGENTS.md/CLAUDE.md, and any doc an agent reaches by a pointer.

## Suggested workflows

The flows below are grounded in the [`ask-matt`](./skills/engineering/ask-matt/SKILL.md) router.

- **Configure a repo:** `/setup` once before its first engineering workflow.
- **Choose a starting point:** `/ask-matt` with the situation you are facing.
- **Small change:** `/grill-with-docs` → `/implement`. Use `/tdd` directly for a concrete behaviour that only needs test-first implementation.
- **Multi-session feature:** `/grill-with-docs` → `/to-spec` → `/to-tickets` → `/implement` per ticket, blockers first. Keep planning in one context through ticket creation; start fresh for each ticket.
- **Parallel implementation:** `/to-spec` → `/to-tickets` → `/implement-spec` to work ready tickets on one integration branch.
- **Existing plan:** `/implement` for a ticket or spec; `/implement-spec` for a whole spec with an associated ticket graph.
- **Incoming requests:** `/triage` → `/implement` for agent-ready issues. Tickets from `/to-tickets` do not need another triage pass.
- **Hard bug or regression:** `/diagnosing-bugs` → `/retro` to fix the problem and identify preventive improvements.
- **Architecture upkeep:** `/improve-codebase-architecture` → explore the chosen candidate → `/to-spec` and `/to-tickets` if it needs a larger build.
- **Huge, uncertain effort:** `/wayfinder` → `/to-spec` → `/to-tickets` → implementation. Wayfinding resolves decisions, not deliverables.
- **Unanswered design question:** `/research` for evidence or `/prototype` for a runnable answer, then bring the findings back into planning.
- **Review and delivery:** `/code-review` against a fixed base → `/pr` when preparing a pull request → `/retro` before clearing the session. Implementation skills already include code review.
- **Change directory, harness, or collaborator:** `/handoff` to make the conversation portable.
- **Non-code decision:** `/grill-me`; use `/to-questionnaire` when the answer needs someone else's input, or `/wait-what` when an explanation does not land.
