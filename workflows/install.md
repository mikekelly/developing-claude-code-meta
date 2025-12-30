<required_reading>
Read these before proceeding:
1. standard/CLAUDE.md — The canonical CLAUDE.md to install
2. references/progressive-disclosure.md — Context on README distribution
</required_reading>

<process>
## Step 1: Verify Target Project

Check the target project:
```bash
ls -la {project_path}
```

Confirm:
- [ ] Project directory exists
- [ ] No existing CLAUDE.md (if exists, suggest migrate workflow instead)
- [ ] README.md exists (or will need to create one)

## Step 2: Assess Project Structure

Identify key directories that will need README.md files:
```bash
find {project_path} -type d -name "src" -o -name "packages" -o -name "lib" -o -name "apps" | head -20
```

Note packages/modules that have distinct domains and will benefit from their own README.md.

## Step 3: Install CLAUDE.md

Copy `standard/CLAUDE.md` to the project root exactly as-is. Do not modify it.

The standard CLAUDE.md is designed to work universally. Project-specific information belongs in README.md files, not in CLAUDE.md.

## Step 4: Create Root README.md (if missing)

If no README.md exists, create one with:
- Project name and one-line description
- Quick start (how to run locally)
- Project structure overview with links to package READMEs
- Links to key documentation

**Keep it under 50 lines.** Deep details go in package READMEs.

## Step 5: Create Package READMEs

For each significant package/directory identified in Step 2:

Create a README.md with:
- What this package does (1-2 sentences)
- Key files and their purposes
- Domain-specific patterns or conventions
- Links to related packages

**Each README should be 20-50 lines.**

## Step 6: Verify Installation

Run a quick check:
```bash
wc -l {project_path}/CLAUDE.md
cat {project_path}/CLAUDE.md | head -5
```

Confirm:
- [ ] CLAUDE.md matches `standard/CLAUDE.md` exactly
- [ ] First line contains the "Keep this file under 150 lines" reminder
</process>

<success_criteria>
Installation is complete when:
- [ ] CLAUDE.md installed at project root (exact copy of `standard/CLAUDE.md`)
- [ ] Root README.md exists with project overview
- [ ] At least one package README.md created (if packages exist)
- [ ] Agent can navigate from CLAUDE.md → README.md → package READMEs
</success_criteria>
