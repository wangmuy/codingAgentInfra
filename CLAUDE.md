# Claude Code Infrastructure Template

This repository provides a comprehensive Claude Code assisted codebase infrastructure template. When users clone this repo and use Claude Code with prompts like "setup a claude code assisted codebase for me, using X as frontend and Y as backend", Claude can reference the `showcase` submodule to set up a proper AI-assisted codebase infrastructure.

## ⚠️ Important: Template Workflow

**This is a TEMPLATE repository.** When assisting users:

1. Read **[TEMPLATE_USAGE.md](./TEMPLATE_USAGE.md)** BEFORE making any changes
2. **DO NOT** modify template files with specific tech implementations
3. **Gather comprehensive tech specs** from users first
4. **Create customized versions** in `output/` directory
5. Users copy from `output/` to their project

**See [TEMPLATE_USAGE.md](./TEMPLATE_USAGE.md) for the complete workflow.**

## Repository Structure

```
.claude/
├── agents/          # Specialized AI agents for complex tasks
├── commands/        # Slash command definitions
├── hooks/          # Event hooks for automation
└── skills/         # Context-aware skill system
dev/                # Tech-specific project tracking
showcase/           # Reference submodule (do not modify directly)
```

## What's Included

### Agents (11 specialized agents)
- **auth-route-debugger** - Debugs authentication route issues
- **auth-route-tester** - Tests authentication routes
- **auto-error-resolver** - Automatically resolves common errors
- **code-architecture-reviewer** - Reviews code architecture
- **code-refactor-master** - Assists with code refactoring
- **documentation-architect** - Creates project documentation
- **frontend-error-fixer** - Fixes frontend errors
- **plan-reviewer** - Reviews implementation plans
- **refactor-planner** - Plans refactoring strategies
- **web-research-specialist** - Conducts web research

See [showcase/.claude/agents/README.md](showcase/.claude/agents/README.md) for full documentation.

### Commands (3 commands)
- **dev-docs** - Accesses development documentation
- **dev-docs-update** - Updates development documentation
- **route-research-for-testing** - Researches routes for testing

### Hooks (Essential + Optional)
**Essential (Generic - always safe to use):**
- **skill-activation-prompt** - Auto-suggests skills based on user prompts
- **post-tool-use-tracker** - Tracks file changes for context management

**Optional (Require customization for specific project structures):**
See [showcase/.claude/hooks/README.md](showcase/.claude/hooks/README.md) for details on build hooks, TypeScript checking, etc.

### Skills (5 comprehensive skills)

1. **skill-developer** - Meta-skill for creating new skills (tech-agnostic)
2. **backend-dev-guidelines** - Backend development patterns (Express/Prisma)
3. **frontend-dev-guidelines** - Frontend development patterns (React/MUI v7)
4. **route-tester** - Route testing automation (JWT cookie auth)
5. **error-tracking** - Error tracking with Sentry

**Tech Compatibility:**
- **skill-developer**: Works with ANY tech stack
- **backend-dev-guidelines**: Requires Node.js/Express/Prisma/TypeScript
- **frontend-dev-guidelines**: Requires React 18+/MUI v7/TanStack/TypeScript
- **route-tester**: Requires JWT cookie-based authentication
- **error-tracking**: Works with most backends using Sentry

### Dev Directory
The `dev/` directory is for tech-specific project tracking and documentation. See [dev/README.md](dev/README.md) for usage patterns.

## How to Use This Template

### ⚠️ CRITICAL: Template Workflow

**This repository is a TEMPLATE.** When users ask you to "setup a Claude Code assisted codebase," follow this workflow:

1. **DO NOT modify template files with specific tech implementations**
2. **Gather comprehensive tech specifications** from user (see below)
3. **Create customized version in `output/` directory**
4. **User copies from `output/` to their project**

### Template Workflow Steps

#### Step 1: Gather Tech Stack Specifications

When user says: "setup a claude code assisted codebase for me, using React frontend and Node backend"

**You MUST ask comprehensive questions:**

**Frontend Questions:**
- What framework and version? (React 18+, Vue, Angular, etc.)
- UI library? (MUI v5/v7, Ant Design, Tailwind, etc.)
- State management? (Redux, Zustand, TanStack Query, etc.)
- Router? (TanStack Router, React Router, etc.)
- TypeScript or JavaScript?

**Backend Questions:**
- What framework and version? (Express, Fastify, NestJS, etc.)
- Database? (Prisma, Sequelize, Mongoose, etc.)
- Authentication? (JWT, session-based, etc.)
- Language? (TypeScript, JavaScript)

**Project Structure:**
- Monorepo, polyrepo, or separate repos?
- Where is the code located?
- Any existing conventions or patterns?

Keep asking until you have a complete picture.

#### Step 2: Create Output Directory

Create all customized files in:
```
output/
├── .claude/
│   ├── agents/          # (copied from template)
│   ├── hooks/           # (copied from template)
│   ├── skills/          # (selectively copied based on tech stack)
│   └── settings.json    # (customized for their tech stack)
├── dev/
│   └── [tech]-guide.md  # (customized with their patterns)
└── SETUP.md             # (project-specific setup instructions)
```

#### Step 3: Customize Components

Only copy skills that match their tech stack:

| User's Tech Stack | Copy This | Skip This |
|-------------------|-----------|-----------|
| React + MUI v7    | `frontend-dev-guidelines` | `backend-dev-guidelines` |
| Express + Prisma  | `backend-dev-guidelines` | `frontend-dev-guidelines` |
| Other frameworks  | Copy as template only | Adapt patterns |

**Always copy:**
- All agents (tech-agnostic)
- Essential hooks (skill-activation, post-tool-use)
- skill-developer (meta-skill)

#### Step 4: Provide Setup Instructions

User copies `output/` to their project and follows customized `SETUP.md`.

### Why This Workflow?

**Before (Problem):**
```
User: "Setup for Android"
Claude: *modifies template files immediately*
Result: Template is now Android-specific, can't be reused
```

**After (Solution):**
```
User: "Setup for React + Node"
Claude: *creates output/react-node-setup/*
Result: Template remains generic, user gets customized version
```

This ensures:
✅ Template stays reusable
✅ User gets project-specific customization
✅ No conflicts with existing project files
✅ Clear separation between template and implementation

### For Claude Code (When Assisting Users)

When a user asks you to set up a Claude Code assisted codebase:

1. **Reference the Integration Guide**: The [showcase/CLAUDE_INTEGRATION_GUIDE.md](showcase/CLAUDE_INTEGRATION_GUIDE.md) contains step-by-step instructions for integrating components into user projects.

2. **Ask Clarifying Questions**: Always ask about:
   - Project structure (monorepo vs single app)
   - Tech stack (frontend/backend frameworks)
   - Where code is located

3. **Copy Components as Needed**: From this template, copy only the components relevant to their tech stack and needs.

4. **Customize for Their Setup**: Update paths, triggers, and configurations to match their project structure.

### Example User Prompts

**User**: "Setup a claude code assisted codebase for me, using React as frontend and Node.js as backend."

**Your approach**:
1. Copy `skill-activation-prompt` and `post-tool-use-tracker` hooks
2. Check if they use MUI v7 for frontend
   - If YES: Copy `frontend-dev-guidelines` skill
   - If NO: Ask if they want adapted version or skip
3. Check if they use Express with Prisma
   - If YES: Copy `backend-dev-guidelines` skill
   - If NO: Ask if they want adapted version or skip
4. Copy relevant agents (e.g., `code-architecture-reviewer`, `documentation-architect`)
5. Set up `dev/` directory structure
6. Configure hooks in `.claude/settings.json`

**User**: "Add everything from the showcase to my project"

**Your approach**:
1. Start with essentials: skill-activation hooks
2. Add relevant skills based on their tech stack (ask first!)
3. Copy agents (fully generic, always safe)
4. Set up dev directory
5. DON'T copy everything blindly - verify tech compatibility

## Quick Setup Commands

```bash
# Copy all agents (always safe)
cp -r .claude/agents/* $USER_PROJECT/.claude/agents/

# Copy essential hooks (always safe)
cp .claude/hooks/skill-activation-prompt.* $USER_PROJECT/.claude/hooks/
cp .claude/hooks/post-tool-use-tracker.sh $USER_PROJECT/.claude/hooks/

# Copy skills selectively (check tech requirements!)
cp -r .claude/skills/skill-developer $USER_PROJECT/.claude/skills/

# Copy dev directory
cp -r dev $USER_PROJECT/
```

## Important Notes

1. **DO NOT** modify the `showcase/` submodule directly - it's a reference
2. **ALWAYS** check tech stack compatibility before copying skills
3. **CUSTOMIZE** path patterns in skill-rules.json for user projects
4. **TEST** hooks before adding them to settings.json
5. **MAKE HOOKS EXECUTABLE**: `chmod +x .claude/hooks/*.sh`

## Documentation

- **Integration Guide**: [showcase/CLAUDE_INTEGRATION_GUIDE.md](showcase/CLAUDE_INTEGRATION_GUIDE.md) - Comprehensive guide for integrating components
- **Hook Configuration**: [showcase/.claude/hooks/CONFIG.md](showcase/.claude/hooks/CONFIG.md) - Hook setup and configuration
- **Skill Rules**: [showcase/.claude/skills/skill-rules.json](showcase/.claude/skills/skill-rules.json) - Example skill activation rules
- **Agent README**: [showcase/.claude/agents/README.md](showcase/.claude/agents/README.md) - All available agents

## Development Commands for This Template

### Install Hook Dependencies
```bash
cd .claude/hooks && npm install
```

### Validate JSON Files
```bash
# Check skill-rules.json syntax
cat .claude/skills/skill-rules.json | jq .

# Validate settings.json when created
cat .claude/settings.json | jq .
```

## Architecture Overview

This infrastructure template provides:

1. **Context-Aware Skills**: Skills that activate based on file types and user prompts
2. **Specialized Agents**: Standalone agents for complex, multi-step tasks
3. **Automation Hooks**: Event-driven automation for skill suggestions and tracking
4. **Project Documentation**: Structured dev directory for tracking project decisions
5. **Tech Agnostic Core**: Framework-agnostic patterns with tech-specific examples

The modular design allows selective adoption - users can take only what they need for their specific tech stack and project structure.