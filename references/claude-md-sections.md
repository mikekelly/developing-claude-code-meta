<overview>
This reference explains the purpose of each section in the standard CLAUDE.md. The standard CLAUDE.md (`standard/CLAUDE.md`) should be copied exactly into projects — it is not customised. This reference helps you understand why each section exists.
</overview>

<section name="line-count-reminder">
**First line:**
```
> Keep this file under 150 lines. Project specifics live in package README.md files.
```

**Purpose**: Reminds both humans and agents that CLAUDE.md should stay lean. The 150-line limit is a forcing function to push project-specific content to README files.

**Why it matters**: Without this reminder, CLAUDE.md tends to accumulate content over time as developers add "just one more thing."
</section>

<section name="critical-instruction">
**Tags**: `<critical-instruction>` (can have multiple)

**Purpose**: Non-negotiable behavioural directives that override default agent behaviour.

**Standard content**:
1. "Act as a peer, not an assistant" — Encourages constructive pushback
2. "Proactively invoke skills" — Ensures agents use available skills

**Note**: The standard CLAUDE.md includes these two critical instructions and should not be modified. Project-specific constraints belong in README.md files.
</section>

<section name="agent-hierarchy">
**Tag**: `<agent-hierarchy>`

**Purpose**: Defines how main agents and sub-agents should behave differently.

**Key distinctions**:
- **Main agent** (has Task tool): Interacts with user, delegates execution
- **Sub-agent** (no Task tool): Executes tasks, coordinates via files

**Delegation triggers**: Explicit criteria for when main agents must spawn sub-agents:
- Reading more than ~3 files
- Any code changes
- Running tests or builds
- Any task generating substantial output

**Why it matters**: Prevents sub-agents from trying to delegate when they can't, and **strongly encourages main agents to delegate rather than doing everything themselves**. Main agents that do execution work themselves will exhaust their context.
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
- **Leave it tidier**: Fix problems you encounter rather than working around them
</section>

<section name="behavioural-authority">
**Tag**: `<behavioural-authority>`

**Purpose**: Provides explicit precedence when sources of truth conflict.

**Precedence order**:
1. Passing tests (verified behaviour)
2. Failing tests (intended behaviour)
3. Explicit specs in docs/
4. Code (implicit behaviour)
5. External documentation

**Key rule**: "Fix-by-inspection is forbidden" — if you believe code is wrong, write a failing test first.

**Why it matters**: Agents encounter conflicting information (README says X, code does Y). Without explicit precedence, they guess or ask the user unnecessarily. This section eliminates ambiguity.

**Why failing tests rank second**: A failing test is evidence of intent — someone wrote down what the system *should* do. It's executable and was deliberately committed, making it more authoritative than prose specs.
</section>

<section name="orientation">
**Tag**: `<orientation>`

**Purpose**: Points the agent to the README.md for project-specific information.

**Standard content**:
```
@README.md provides project overview and links to package documentation.
```

**Note**: This assumes README.md is at the project root, which is the standard convention.
</section>

<section name="task-management">
**Tag**: `<task-management>`

**Purpose**: Defines how tasks are tracked and coordinated.

**Standard approach**:
- `TODO.md` as the issue tracker
- `DONE.md` as the audit trail
- `docs/{feature}/` for planning breakdowns

**Why TODO.md over external tools**: Keeps task state in the repo, visible to agents without API calls, version-controlled alongside code.
</section>

<section name="development-workflow">
**Tag**: `<development-workflow>`

**Purpose**: Defines the standard workflow for implementing changes.

**Standard steps**:
1. **Baseline first** — Run full test suite before any changes (this is step 1, not optional)
2. Research — Read tests to understand current behaviour
3. Plan — Write plan in `docs/`
4. Reflect — Review critically, get user input on trade-offs
5. Implement (TDD) — Write failing tests first, then implementation
6. Verify — Run full test suite again before considering work complete
7. Clean up — Delete plan, tests are the authority

**Key insight**: Baseline first ensures you know the system works before changing it. A failing test suite is a blocker. Plans are deleted because tests are the lasting documentation.
</section>

<section name="test-driven-development">
**Tag**: `<test-driven-development>`

**Purpose**: Establishes TDD philosophy and practices as non-negotiable.

**The TDD cycle**: RED → GREEN → REFACTOR
1. RED: Write a failing test first
2. GREEN: Write minimum implementation to pass
3. REFACTOR: Clean up while keeping tests green

**Non-negotiable rules**:
- Never write implementation without a failing test first
- Outside-in approach (user perspective first)
- Failing test before any bug fix
- Prefer real integrations over mocks
- Tag slow tests for fast feedback, but always run full suite before commit

**Why emphasised so strongly**: Agents tend to skip straight to implementation. This section makes clear that writing implementation without a failing test is not acceptable.
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
</section>

<section_checklist>
When auditing a CLAUDE.md, verify it matches `standard/CLAUDE.md` exactly. All sections are required and should not be modified.
</section_checklist>
