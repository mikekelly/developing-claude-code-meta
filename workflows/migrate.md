<required_reading>
Read these before proceeding:
1. The existing CLAUDE.md in the target project
2. templates/claude-md-template.md — The target structure
3. references/progressive-disclosure.md — Principles for content distribution
</required_reading>

<process>
## Step 1: Analyse Existing CLAUDE.md

Read the existing file:
```bash
cat {project_path}/CLAUDE.md
wc -l {project_path}/CLAUDE.md
```

Categorise each section into:

**KEEP in CLAUDE.md** (agent behaviour):
- Critical instructions about communication style
- Agent hierarchy/role definitions
- Workflow patterns (TDD, task management)
- Definition of done
- Orientation pointers to README.md

**MOVE to README.md** (project knowledge):
- Tech stack details
- API endpoint documentation
- Database schema information
- Environment variable lists
- Third-party service configurations
- Testing commands/scripts
- Build/deploy procedures

**DELETE** (redundant or stale):
- Obvious information Claude already knows
- Duplicated content
- Outdated instructions

## Step 2: Map Content to Destinations

Create a migration plan:

| Content | Current Location | New Location | Reason |
|---------|------------------|--------------|--------|
| ... | CLAUDE.md line X | README.md | Project knowledge |
| ... | CLAUDE.md line Y | packages/api/README.md | API-specific |
| ... | CLAUDE.md line Z | DELETE | Redundant |

## Step 3: Create/Update README Files

For each destination identified:

**Root README.md:**
- Project overview
- Quick start
- Architecture overview
- Links to package READMEs

**Package README.md files:**
- Module-specific context
- Key files and patterns
- Domain-specific conventions

## Step 4: Replace CLAUDE.md

Replace the existing CLAUDE.md with the standard template from `templates/claude-md-template.md`.

Customise only:
- `<orientation>` — Point to actual README.md location
- `<critical-instruction>` — Add project-specific agent behaviour if essential

**Do NOT add project knowledge back into CLAUDE.md.**

## Step 5: Verify Migration

Check the result:
```bash
wc -l {project_path}/CLAUDE.md
wc -l {project_path}/README.md
find {project_path} -name "README.md" | wc -l
```

Confirm:
- [ ] New CLAUDE.md is under 100 lines
- [ ] All moved content is accessible via README.md chain
- [ ] No orphaned content (everything moved or deliberately deleted)

## Step 6: Test Agent Navigation

Simulate an agent's path:
1. Read CLAUDE.md — Get agent behaviour instructions
2. Read README.md — Get project overview
3. Navigate to package README — Get domain-specific context

If any step feels incomplete, add content to the appropriate README.
</process>

<common_content_migrations>
**Tech stack → Root README.md**
```
# Before (CLAUDE.md)
We use React 18, TypeScript, and Vite for the frontend.
The backend is Node.js with Express and PostgreSQL.

# After (README.md)
## Tech Stack
- Frontend: React 18, TypeScript, Vite
- Backend: Node.js, Express, PostgreSQL
```

**API documentation → packages/api/README.md**
```
# Before (CLAUDE.md)
The API has these endpoints:
- GET /users - List users
- POST /users - Create user

# After (packages/api/README.md)
## Endpoints
See route definitions in `src/routes/`. Key endpoints:
- /users — User management
- /auth — Authentication
```

**Environment variables → Root README.md**
```
# Before (CLAUDE.md)
Required env vars: DATABASE_URL, API_KEY, JWT_SECRET

# After (README.md)
## Environment
Copy `.env.example` to `.env`. Required variables documented in the example file.
```

**Testing commands → Root README.md or CONTRIBUTING.md**
```
# Before (CLAUDE.md)
Run tests with: npm test
Run specific test: npm test -- --grep "pattern"

# After (README.md)
## Development
- `npm test` — Run test suite
- `npm run dev` — Start dev server
```
</common_content_migrations>

<success_criteria>
Migration is complete when:
- [ ] Old CLAUDE.md content fully categorised (keep/move/delete)
- [ ] New CLAUDE.md installed (under 100 lines)
- [ ] Moved content placed in appropriate README.md files
- [ ] Content navigation tested (CLAUDE.md → README.md → package READMEs)
- [ ] No project-specific technical details remain in CLAUDE.md
</success_criteria>
