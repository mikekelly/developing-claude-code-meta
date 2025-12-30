<required_reading>
Read these before proceeding:
1. references/progressive-disclosure.md — Principles being audited against
2. references/claude-md-sections.md — Expected CLAUDE.md sections
</required_reading>

<process>
## Step 1: Gather Project Information

Collect key metrics:
```bash
# CLAUDE.md line count
wc -l {project_path}/CLAUDE.md

# README.md presence
find {project_path} -name "README.md" -type f | head -20

# Package/module structure
find {project_path} -type d -name "src" -o -name "packages" -o -name "lib" -o -name "apps" 2>/dev/null | head -10
```

## Step 2: Audit CLAUDE.md

Read and analyse:
```bash
cat {project_path}/CLAUDE.md
```

**Check list:**

| Criterion | Pass | Fail |
|-----------|------|------|
| Under 100 lines | ≤100 lines | >100 lines |
| Has line count reminder | First line warns about limit | Missing |
| Contains agent behaviour | Workflow, TDD, task management | Missing sections |
| No project-specific tech | No API docs, env vars, schemas | Contains technical details |
| Has orientation section | Points to README.md | Missing navigation |
| Uses XML structure | Semantic tags | Plain text or markdown headings |

**Content classification:**
For each major section, classify as:
- **Correct** — Agent behaviour, belongs in CLAUDE.md
- **Misplaced** — Project knowledge, should be in README.md
- **Redundant** — Obvious to Claude, should be removed

## Step 3: Audit README Distribution

For each significant package/directory:

```bash
# Check if README exists
ls {package_path}/README.md 2>/dev/null || echo "MISSING"
```

| Package | Has README | Content Quality |
|---------|------------|-----------------|
| root | Yes/No | Good/Sparse/Bloated |
| packages/api | Yes/No | Good/Sparse/Bloated |
| packages/web | Yes/No | Good/Sparse/Bloated |

**README quality criteria:**
- **Good**: 20-100 lines, covers purpose + key files + patterns
- **Sparse**: <20 lines, missing essential context
- **Bloated**: >150 lines, should be split or moved to tests

## Step 4: Check Navigation Chain

Test the agent navigation path:

1. **CLAUDE.md → README.md**
   - Does CLAUDE.md point to README.md?
   - Is the path correct?

2. **README.md → Package READMEs**
   - Does root README link to package docs?
   - Are links valid?

3. **Package READMEs → Code**
   - Do READMEs reference actual files?
   - Are key entry points documented?

## Step 5: Generate Audit Report

Create a summary:

```markdown
# CLAUDE.md Audit Report

## Summary
- **CLAUDE.md**: {line_count} lines ({PASS/FAIL} ≤100)
- **README coverage**: {count}/{total} packages have READMEs
- **Navigation**: {COMPLETE/INCOMPLETE}

## Issues Found

### Critical (must fix)
- ...

### Warnings (should fix)
- ...

### Suggestions (nice to have)
- ...

## Recommended Actions
1. ...
2. ...
```

## Step 6: Provide Recommendations

Based on findings, recommend:

**If CLAUDE.md too large:**
→ Run migrate workflow

**If READMEs missing:**
→ List specific packages needing documentation

**If navigation broken:**
→ Identify broken links and suggest fixes

**If content misplaced:**
→ Specify what content should move where
</process>

<audit_checklist>
**CLAUDE.md Conformance:**
- [ ] Line count ≤ 100
- [ ] First line contains limit reminder
- [ ] Has `<critical-instruction>` section
- [ ] Has `<principles>` section
- [ ] Has `<orientation>` pointing to README.md
- [ ] Has `<task-management>` section
- [ ] Has `<development-workflow>` section
- [ ] Has `<test-driven-development>` section
- [ ] Has `<definition-of-done>` section
- [ ] No project-specific technical details
- [ ] Uses XML tags (not markdown headings)

**README Distribution:**
- [ ] Root README.md exists
- [ ] Root README under 100 lines
- [ ] Each major package has README.md
- [ ] Package READMEs cover purpose + key files
- [ ] No README over 150 lines (should split)

**Navigation:**
- [ ] CLAUDE.md → README.md link works
- [ ] README.md → package READMEs linked
- [ ] All links valid

**Content Placement:**
- [ ] Tech stack in README.md (not CLAUDE.md)
- [ ] API docs in relevant package README
- [ ] Environment setup in README.md
- [ ] Testing commands in README.md or CONTRIBUTING.md
</audit_checklist>

<success_criteria>
Audit is complete when:
- [ ] All metrics gathered
- [ ] CLAUDE.md analysed against checklist
- [ ] README distribution assessed
- [ ] Navigation chain tested
- [ ] Audit report generated
- [ ] Actionable recommendations provided
</success_criteria>
