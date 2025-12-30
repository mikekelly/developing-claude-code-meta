<overview>
This reference explains the purpose and content of each section in the standard CLAUDE.md template. Use this when installing or auditing a project's CLAUDE.md.
</overview>

<section name="line-count-reminder">
**First line:**
```
> Keep this file under 100 lines. Project specifics live in package README.md files.
```

**Purpose**: Reminds both humans and agents that CLAUDE.md should stay lean. The 100-line limit is a forcing function to push project-specific content to README files.

**Why it matters**: Without this reminder, CLAUDE.md tends to accumulate content over time as developers add "just one more thing."
</section>

<section name="critical-instruction">
**Tags**: `<critical-instruction>` (can have multiple)

**Purpose**: Non-negotiable behavioural directives that override default agent behaviour.

**Standard content**:
1. "Act as a peer, not an assistant" — Encourages constructive pushback
2. "Proactively invoke skills" — Ensures agents use available skills

**When to add custom instructions**: Only for genuinely critical behaviour. Examples:
- Security requirements: "Never commit secrets to git"
- Domain constraints: "All monetary calculations must use decimal, not float"
- Communication rules: "Always explain trade-offs before implementing"

**Avoid**: Using this section for project knowledge or technical details.
</section>

<section name="agent-hierarchy">
**Tag**: `<agent-hierarchy>`

**Purpose**: Defines how root agents and sub-agents should behave differently.

**Key distinctions**:
- **Root agent** (has AskUserQuestion tool): Interacts with user, delegates execution
- **Sub-agent** (no AskUserQuestion): Executes tasks, coordinates via files

**Why it matters**: Prevents sub-agents from trying to ask questions they can't ask, and encourages root agents to delegate rather than doing everything themselves.

**Should rarely be customised**. The standard hierarchy works for most projects.
</section>

<section name="principles">
**Tag**: `<principles>`

**Purpose**: Core values that guide agent decision-making across all tasks.

**Standard principles**:
- **Context is a public good**: Delegate to conserve context
- **Load context just-in-time**: Don't read everything upfront
- **Tests are the documentation**: Trust tests over markdown
- **Markdown is ephemeral**: Working docs get deleted
- **Permanent docs are minimal**: Only architecture in markdown
- **KISS**: Don't over-engineer
- **Small diffs**: Focused changes
- **Always explain the why**: Include reasoning

**Customisation**: Generally keep the standard principles. Add project-specific principles sparingly, only if they fundamentally change how work should be approached.
</section>

<section name="orientation">
**Tag**: `<orientation>`

**Purpose**: Points the agent to the README.md for project-specific information.

**Standard content**:
```
@README.md provides project overview and links to package documentation.
```

**Customisation**: Update if README is in a different location or has a different name.
</section>

<section name="task-management">
**Tag**: `<task-management>`

**Purpose**: Defines how tasks are tracked and coordinated.

**Standard approach**:
- `TODO.md` as the issue tracker
- `DONE.md` as the audit trail
- `docs/{feature}/` for planning breakdowns

**Why TODO.md over external tools**: Keeps task state in the repo, visible to agents without API calls, version-controlled alongside code.

**Customisation**: If the project uses a different task management approach (e.g., GitHub Issues), update this section to match.
</section>

<section name="development-workflow">
**Tag**: `<development-workflow>`

**Purpose**: Defines the standard workflow for implementing changes.

**Standard steps**:
1. Research — Read tests to understand current behaviour
2. Plan — Write plan in `docs/`
3. Reflect — Review critically, get user input on trade-offs
4. Baseline — Ensure existing tests pass
5. Implement — Build with tests
6. Clean up — Delete plan, tests are the authority

**Key insight**: Plans are deleted because tests are the lasting documentation. If behaviour isn't tested, it's not guaranteed.

**Customisation**: Adjust if project has different workflow requirements (e.g., requires code review before merge).
</section>

<section name="test-driven-development">
**Tag**: `<test-driven-development>`

**Purpose**: Establishes TDD philosophy and practices.

**Key points**:
- Tests define behaviour; implementation makes tests pass
- Outside-in approach (user perspective first)
- Failing test before fix
- Prefer real integrations over mocks
- Tag slow tests for fast feedback during development

**Customisation**: Adjust testing philosophy if project has different requirements (e.g., heavily mocked tests due to external constraints).
</section>

<section name="finding-information">
**Tag**: `<finding-information>`

**Purpose**: Reinforces that tests are the source of truth.

**Standard content**:
```
> **Tests are the documentation.** Read tests to understand the behaviour of the system and its components. If behaviour isn't tested, it's not guaranteed.
```

**Why it matters**: Prevents agents from trusting stale documentation over executable tests.
</section>

<section name="definition-of-done">
**Tag**: `<definition-of-done>`

**Purpose**: Clear criteria for when a task is complete.

**Standard criteria**:
1. Tests pass
2. Task is completed
3. No documentation that should be a test remains
4. Code is committed (and pushed if remote exists)

**Customisation**: Add project-specific completion criteria if needed (e.g., "Changelog updated", "Type checking passes").
</section>

<section_checklist>
When auditing a CLAUDE.md, verify these sections exist and contain appropriate content:

| Section | Required | Customisable |
|---------|----------|--------------|
| Line count reminder | Yes | No |
| critical-instruction | Yes (at least peer + skills) | Add sparingly |
| agent-hierarchy | Yes | Rarely |
| principles | Yes | Add sparingly |
| orientation | Yes | Update path if needed |
| task-management | Yes | Match project approach |
| development-workflow | Yes | Adjust to project needs |
| test-driven-development | Yes | Adjust to testing philosophy |
| finding-information | Yes | No |
| definition-of-done | Yes | Add project-specific criteria |
</section_checklist>
