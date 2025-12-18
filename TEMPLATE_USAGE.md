# Template Usage Workflow

## Overview

This document describes the **standard workflow** for using the Coding Agent Infrastructure Template to set up assisted codebases for any AI coding agent (Claude Code, Gemini CLI, Cline, RooCode, etc.).

---

## The Golden Rule

> **NEVER modify template files with specific tech implementations**

Instead:
1. Gather comprehensive tech specifications from the user
2. Create a customized version in the `output/` directory
3. User copies from `output/` to their project

---

## Workflow Steps

### Step 1: Gather Tech Stack Specifications

When a user says: **"Setup a coding agent assisted codebase for me, using React as frontend and Node.js as backend"**

#### ⚠️ CRITICAL: You must ask detailed questions before proceeding

### Frontend Questionnaire

**Framework & Language:**
- What frontend framework and version are you using?
  - React 18+? Vue 3? Angular? Svelte?
- TypeScript or JavaScript?
  - If TypeScript, what version and configuration?

**UI Components:**
- What UI library are you using?
  - Material-UI (MUI) v5 or v7?
  - Ant Design?
  - Chakra UI?
  - Tailwind CSS + custom components?
  - Or vanilla CSS/styled-components?

**State Management:**
- How do you manage application state?
  - Redux Toolkit?
  - Zustand?
  - TanStack Query (React Query)?
  - Context API?
  - Or other solution?

**Routing:**
- What routing solution?
  - TanStack Router?
  - React Router v6?
  - Next.js App Router?
  - Vue Router?

**Data Fetching:**
- How do you fetch and cache data?
  - TanStack Query?
  - SWR?
  - RTK Query?
  - Custom hooks?

**Build Tool:**
- Vite? Create React App? Next.js? Other?

**Key Libraries:**
- Form handling? (React Hook Form, Formik, etc.)
- Date handling? (date-fns, dayjs, etc.)
- HTTP client? (Axios, fetch, etc.)

### Backend Questionnaire

**Framework & Language:**
- What backend framework and version?
  - Express.js? Fastify? NestJS? Koa?
- TypeScript or JavaScript?
  - If TypeScript, what version and configuration?

**Database:**
- What database and ORM?
  - PostgreSQL + Prisma?
  - MongoDB + Mongoose?
  - MySQL + Sequelize?
  - Other?

**Authentication:**
- How do users authenticate?
  - JWT tokens?
  - Session-based?
  - OAuth? (Google, GitHub, etc.)
  - Keycloak? Auth0? Clerk?

**API Style:**
- REST? GraphQL? gRPC?

**Key Libraries:**
- Validation? (Zod, Joi, class-validator, etc.)
- Error tracking? (Sentry, etc.)
- Testing? (Jest, Mocha, etc.)

**Architecture Pattern:**
- Layered architecture (routes → controllers → services → repositories)?
- Feature-based structure?
- Other patterns?

### Project Structure

**Repository Layout:**
- Monorepo? Polyrepo? Separate frontend/backend repos?
- Where is the frontend code located? (root? `frontend/`? `web/`?)
- Where is the backend code located? (root? `backend/`? `api/`? `server/`?)

**Existing Codebase:**
- Starting from scratch or adding to existing project?
- Any existing conventions or patterns I should follow?
- Team preferences or standards?

### Step 2: Create Output Directory Structure

Once you have the complete tech stack, create a **self-contained directory** that users can copy directly to their project:

```
output/[project-name]/
├── CLAUDE.md              # PROJECT-SPECIFIC documentation (main user guide)
├── .claude/
│   ├── agents/            # Copied from template (all are tech-agnostic)
│   ├── hooks/             # Copied from template (essential hooks)
│   ├── skills/            # SELECTIVELY copied based on tech stack
│   └── settings.json      # CUSTOMIZED for their specific setup
├── dev/
│   └── [tech]-guide.md    # CUSTOMIZED with their patterns and examples
└── AGENT_SETUP_VERIFY.md  # Quick setup verification steps
```

**Important:** The `CLAUDE.md` in the output directory is the MAIN documentation for the user. It replaces the need for a README with copy instructions.

### Step 3: Selectively Copy Components

**Always Copy (Tech-Agnostic):**
- ✅ All agents (`.claude/agents/*`) - 11 specialized agents
- ✅ Essential hooks (`.claude/hooks/skill-activation-prompt.*`, `post-tool-use-tracker.sh`)
- ✅ skill-developer (`.claude/skills/skill-developer/`) - meta-skill for creating skills

**Conditionally Copy (Tech-Specific):**

| User's Tech Stack | Copy This | Skip This |
|-------------------|-----------|-----------|
| React + MUI v7 | `frontend-dev-guidelines/` | `backend-dev-guidelines/` |
| React + other UI | Copy as template | Adapt patterns |
| Vue 3 | Copy as template | Adapt patterns |
| Express + Prisma | `backend-dev-guidelines/` | `frontend-dev-guidelines/` |
| Fastify + Prisma | Copy as template | Adapt patterns |
| NestJS + Prisma | Copy as template | Adapt patterns |
| Other frameworks | Copy as template | Adapt patterns |

**Optional Components:**
- `route-tester/` - If using JWT cookie auth
- `error-tracking/` - If using Sentry
- Additional hooks (build check, tsc check, etc.) - Only if build pipeline exists

### Step 4: Customize Settings

Create `.claude/settings.json` with:

```json
{
  "hooks": {
    "UserPromptSubmit": ["skill-activation-prompt"],
    "PostToolUse": ["post-tool-use-tracker"]
  },
  "permissions": {
    "allow": ["Skill(skill-developer)"],
    "deny": [],
    "ask": []
  },
  "project": {
    "type": "[frontend-type]",
    "backend": "[backend-type]",
    "framework": "[specific-framework]"
  }
}
```

### Step 5: Create Tech-Specific Documentation

Create `dev/[tech]-guide.md` with:
- Overview of tech stack
- Architecture patterns used
- Example code specific to their frameworks
- Best practices for their stack
- Custom skills to consider creating

### Step 6: Create Setup Instructions

Create `AGENT_SETUP_VERIFY.md` with quick verification steps:
- Configuration validation steps
- Verification commands
- Next steps
- Usage examples specific to their tech stack

**DO NOT include "how to copy" instructions** - the output directory is self-contained and users simply copy the entire directory to their project root.

---

## Example Workflow

### User Request

```
User: "Setup a coding agent assisted codebase for me, using React frontend and Node backend"
```

### Your Response

#### Phase 1: Gather Specifications

```
Great! I'll set up a coding agent assisted codebase for you. To customize it
properly, I need some details about your tech stack:

**Frontend Questions:**
1. What React version? (17, 18, or newer?)
2. TypeScript or JavaScript?
3. What UI library? (MUI v7, Ant Design, Chakra, Tailwind?)
4. State management? (Redux, Zustand, TanStack Query?)
5. Router? (React Router, TanStack Router?)

**Backend Questions:**
1. Node.js framework? (Express, Fastify, NestJS?)
2. Database and ORM? (PostgreSQL + Prisma, MongoDB + Mongoose?)
3. Authentication? (JWT, sessions?)
4. TypeScript or JavaScript?

**Project Structure:**
1. Monorepo or separate repos?
2. Where should code be located? (frontend/, backend/, etc.)

Please provide these details and I'll create a customized setup in the
output/ directory.
```

#### Phase 2: Create Output Directory

After getting specs:

```
Perfect! Based on your specs:
- React 18 with TypeScript, MUI v7, TanStack Query
- Express with TypeScript, Prisma, PostgreSQL
- JWT authentication
- Monorepo structure

Creating customized setup in output/react-express-setup/...
```

**Actions taken:**
```bash
mkdir -p output/react-express-setup

cp -r .claude/agents output/react-express-setup/.claude/
cp -r .claude/hooks output/react-express-setup/.claude/

cp -r showcase/.claude/skills/skill-developer output/react-express-setup/.claude/skills/
cp -r showcase/.claude/skills/frontend-dev-guidelines output/react-express-setup/.claude/skills/
cp -r showcase/.claude/skills/backend-dev-guidelines output/react-express-setup/.claude/skills/

cp -r dev output/react-express-setup/

# Create customized settings.json
echo '{...}' > output/react-express-setup/.claude/settings.json

# Create tech-specific documentation
echo '...' > output/react-express-setup/dev/REACT_EXPRESS_GUIDE.md
echo '...' > output/react-express-setup/AGENT_SETUP_VERIFY.md
```

#### Phase 3: Provide Instructions

```
✅ Customized setup complete in output/react-express-setup/!

**This is a self-contained coding agent setup. To use it:**

1. **Copy to your project:**
   cp -r output/react-express-setup/* ~/your-project/

2. **Review CLAUDE.md** - This is your main documentation with usage patterns

3. **Run setup verification:**
   cd ~/your-project && cat AGENT_SETUP_VERIFY.md

4. **Make hooks executable:**
   chmod +x .claude/hooks/*.sh  # Important!

That's it! Your coding agent assisted codebase is ready. See CLAUDE.md for detailed usage instructions.
```

---

## Common Tech Stack Examples

### Example 1: React + Express + Prisma

**Components to copy:**
- frontend-dev-guidelines (if using MUI v7)
- backend-dev-guidelines
- route-tester (if using JWT cookie auth)
- error-tracking

**Settings:**
```json
{
  "project": {
    "type": "react",
    "backend": "express",
    "framework": "React 18 + MUI v7 / Express + Prisma"
  }
}
```

### Example 2: Vue 3 + Fastify + MongoDB

**Components to copy:**
- skill-developer (as template for Vue patterns)
- error-tracking

**Settings:**
```json
{
  "project": {
    "type": "vue",
    "backend": "fastify",
    "framework": "Vue 3 / Fastify + Mongoose"
  }
}
```

**Note:** frontend-dev-guidelines and backend-dev-guidelines are for React/MUI and Express/Prisma specifically. For other frameworks, use them as templates to create custom skills.

### Example 3: Mobile (React Native, Flutter, Android, iOS)

**Components to copy:**
- skill-developer
- Select agents based on needs

**Settings:**
```json
{
  "project": {
    "type": "mobile",
    "backend": "[none|firebase|custom]",
    "framework": "React Native / Flutter / Android / iOS"
  }
}
```

---

## Checklist for Template Usage

Before providing the customized setup, verify:

- [ ] Gathered all frontend tech details (framework, UI lib, state management)
- [ ] Gathered all backend tech details (framework, database, ORM)
- [ ] Understood project structure (paths, repo type)
- [ ] Identified which skills match their tech stack
- [ ] Created `output/[project-name]/` directory
- [ ] Copied all agents (tech-agnostic)
- [ ] Copied essential hooks
- [ ] Selectively copied skills based on tech compatibility
- [ ] Created customized `.claude/settings.json`
- [ ] Created `dev/[tech]-guide.md` with tech-specific patterns
- [ ] Created `AGENT_SETUP_VERIFY.md` with clear instructions
- [ ] Verified no template files were modified
- [ ] Provided clear copy instructions to user

---

## Troubleshooting

### Problem: User didn't provide enough tech details
**Solution:** Keep asking questions until you have a complete picture. It's better to ask more than assume.

### Problem: Unclear whether a skill is compatible
**Solution:** Check the skill's requirements in `showcase/.claude/skills/[skill-name]/SKILL.md`. When in doubt, copy as template rather than full implementation.

### Problem: Hooks require project-specific paths
**Solution:** Note this in AGENT_SETUP_VERIFY.md and provide instructions for customization. Use placeholder paths that users can replace.

### Problem: Template files were accidentally modified
**Solution:** Revert the changes immediately. Use `git status` to check for unintended modifications.

---

## Why This Workflow Exists

### The Problem It Solves

Without this workflow:
- Template gets specific tech implementations → becomes unusable for others
- No clear separation between template and implementation
- User can't distinguish template patterns from project-specific code
- Difficult to maintain and update the template

With this workflow:
- Template remains generic and reusable
- Clear separation: template in root, customized versions in `output/`
- User gets exactly what they need without affecting the template
- Easy to create multiple setups for different tech stacks

### Real-World Scenario

```
User 1: "Setup for React + Express"
User 2: "Setup for Vue + Fastify"
User 3: "Setup for Android"

Without workflow:
- Template files get overwritten each time → chaos

With workflow:
- output/react-express-setup/
- output/vue-fastify-setup/
- output/android-setup/
- Template remains untouched ✅
```

---

## For Template Developers

When improving this template:

1. **Always test the template workflow**
   - Ask yourself: "Would this change make the template less generic?"

2. **Add examples to showcase/ not to root**
   - The showcase submodule contains examples
   - Don't add tech-specific examples to the template root

3. **Document any new components**
   - Update this file when adding new workflows
   - Clearly mark what's template vs. example

4. **Maintain the `output/` directory pattern**
   - Any automation should respect this workflow
   - Create subdirectories per tech stack

5. **Keep compatibility with multiple coding agents**
   - This template should work with Claude Code, Gemini CLI, Cline, RooCode, and other AI coding agents
   - Avoid vendor-specific features in core components

---

## References

- **CLAUDE.md** - Main template documentation
- **showcase/** - Example implementations
- **showcase/CLAUDE_INTEGRATION_GUIDE.md** - Integration guide
- **dev/README.md** - Dev docs methodology

---

**Document Version:** 1.0
**Last Updated:** 2025-11-24
**Maintained by:** Claude Code Template System
