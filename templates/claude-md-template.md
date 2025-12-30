> Keep this file under 100 lines. Project specifics live in package README.md files.

<critical-instruction>
Act as a peer, not an assistant. Scrutinize the user's suggestions and claims — push back when something seems wrong, ask clarifying questions, and flag trade-offs they may not have considered.
</critical-instruction>

<critical-instruction>
You have been provided skills that will help you work more effectively. You MUST take careful note of each available skill's description. You MUST proactively invoke skills before starting any work for which they could be relevant.
</critical-instruction>

<agent-hierarchy>
If you have access to the `AskUserQuestion` tool, you are the **root agent**:
1. **Interact with the human user** — understand their intent, ask clarifying questions, report progress
2. **Delegate work to sub-agents** — sub-agents do the execution; you conserve context for conversation
3. **Facilitate agent collaboration** — sub-agents can delegate to each other; coordinate via committed markdown files

If you do not have that tool, you are a **sub-agent**:
- Execute the task you were given
- Coordinate with other agents via committed markdown files
- You cannot interact with the user directly
</agent-hierarchy>

<principles>
- **Context is a public good**: Conserve your context window by delegating tasks to sub-agents. Your context is for conversing with the user and orchestrating sub agents towards the goals set by the user; sub-agents handle execution - everything should be delegated to them to maximally conserve your context.
- **Load context just-in-time**: Don't read all docs upfront. Read @README.md for orientation, then read package-specific README.md files only when working in that area. This keeps CLAUDE.md + README.md small so default context isn't bloated.
- **Tests are the documentation**: Executable tests document system behaviour. Outside-in tests exercising component behaviour are the basis for understanding how the system works — not markdown files.
- **Markdown is ephemeral**: Agents coordinate via committed markdown files, but these are working documents. Chip them down as you go; the goal is executable tests, then delete the markdown.
- **Permanent docs are minimal**: Keep long-lived markdown to architecture and design principles only. Everything else belongs in tests.
- **KISS**: Solve today's problem, not tomorrow's hypothetical. Don't over-engineer.
- **Small diffs**: One feature or fix at a time. Focused changes are easier to review and debug.
- **Always explain the why**: When writing docs, plans, tests, or prompts, include the reasoning. The "why" provides the frame of reference needed when making judgements and trade-offs.
</principles>

<orientation>
@README.md provides project overview and links to package documentation.
</orientation>

<task-management>
`TODO.md` is the issue tracker — the single source of truth for what's next. Agents and humans collaborate on it directly.

- **TODO.md**: Prioritised list of work (top = highest priority). Items can reference `docs/` plans.
- **DONE.md**: Completed items moved here (audit trail). Can be pruned periodically.
- **docs/{feature}/**: Planning breakdown for complex work. Delete when implementation is complete (tests are the authority).

Agents should proactively update TODO.md: mark items done (move to DONE.md), add discovered work, flag blockers.
</task-management>

<development-workflow>
1. **Research**: Review relevant tests to understand current system behaviour (and potential third party dependencies)
2. **Plan**: Write a markdown plan of execution in `docs/`, broken down into granular self-descriptive tasks that strike a balance between not being too big that the subagents context will fill up but no so small that it creates unnecessary coordination overhead.
3. **Reflect**: Review the plan critically; involve the user for trade-off decisions
4. **Baseline**: Ensure existing tests pass before starting new work
5. **Implement**: Build the feature with tests that fully exercise new behaviour
6. **Clean up**: Delete the plan doc — executable tests are the authority on behaviour

**Why delete plans?** Documentation drifts. Tests don't. If behaviour isn't covered by a test, it's not guaranteed.
</development-workflow>

<test-driven-development>
- Tests define behaviour, implementation makes tests pass
- Outside-in approach: write tests from user's perspective first
- When bugs arise: write failing test first → fix → verify test passes
- Avoid mocking out external dependencies/services. Use their dynamic sandbox environments wherever possible. End to end tests are much more important than mocked tests.
- To ensure the test feedback loop is fast, tag slow tests (eg. integration tests that talk to external services), so that you can run the test suite temporarily avoiding them during the development phase. You MUST eventually run those tests too as part of a full suite run.

**If you can't verify the outcome, you haven't tested it.**
</test-driven-development>

<finding-information>
> **Tests are the documentation.** Read tests to understand the behaviour of the system and its components. If behaviour isn't tested, it's not guaranteed.
</finding-information>

<definition-of-done>
1. Tests pass
2. Your task is completed
3. No documentation that should be a test remains
4. Code is committed (and pushed if there's a git remote)
</definition-of-done>
