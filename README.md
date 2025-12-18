# Coding Agent Infrastructure Template

A template for adapting [claude-code-infrastructure-showcase](https://github.com/diet103/claude-code-infrastructure-showcase) to any tech stack with AI coding agents.

**Purpose:** This repository is the adaptation layer - it helps you create customized instances of the showcase for your specific project needs. The final output is a self-contained directory you copy to your project.

---

## What's Included

This template provides the **adaptation layer** for [claude-code-infrastructure-showcase](https://github.com/diet103/claude-code-infrastructure-showcase). When you create an instance, you get:

### 🤖 10 Specialized Agents (Tech-Agnostic)
Autonomous agents that work with any framework:
- `code-architecture-reviewer` - Review code architecture
- `code-refactor-master` - Comprehensive refactoring
- `documentation-architect` - Create documentation
- `frontend-error-fixer` - Fix frontend errors
- `plan-reviewer` - Validate implementation plans
- `refactor-planner` - Plan code reorganization
- `web-research-specialist` - Research technical issues
- `auth-route-tester` - Test authenticated routes
- `auth-route-debugger` - Debug authentication issues
- `auto-error-resolver` - Fix compilation errors

### 🔌 2 Essential Hooks
Enable skill auto-activation for any tech stack:
- `skill-activation-prompt.sh` - Auto-suggests skills
- `post-tool-use-tracker.sh` - Tracks file changes

### 🛠️ Template Skills
Skills you can adapt to your tech stack:

| Skill | Purpose | Use Case |
|-------|---------|----------|
| **skill-developer** | Create new skills | ✅ Always portable |
| **backend-dev-guidelines** | Backend patterns | Template for backend frameworks |
| **frontend-dev-guidelines** | Frontend patterns | Template for frontend frameworks |
| **route-tester** | Route testing | Template for API/auth testing |
| **error-tracking** | Monitoring patterns | Template for error tracking |

### 📚 Dev Directory Pattern
Methodology for maintaining project context across sessions.

---

## Quick Start: Create Your Custom Instance

Use your AI coding agent to create a customized instance of this template for your specific tech stack.

### The Workflow
```
User: "Create an instance of this template using React as frontend and Express as backend"

AI Agent:
1. Reads this template
2. Creates output/react-express-instance/ with customized configs
3. Updates skill-rules.json for your paths
4. Creates settings.json for your setup
5. Provides copy instructions

You:
1. Copy output/react-express-instance/* to your project
2. Run: chmod +x .claude/hooks/*.sh
3. Done - ready to use
```

### What the AI Agent Creates

The AI will generate a **self-contained directory** in `output/[your-project-name]/` containing:

```
output/react-express-instance/
├── .claude/
│   ├── agents/            # All 10 agents (portable)
│   ├── hooks/             # Essential hooks configured
│   ├── skills/            # Template skills + your rule paths
│   └── settings.json      # Your project config
├── dev/                   # Dev docs methodology
└── AGENT_SETUP_VERIFY.md  # Quick verification steps
```

### Your Copy-Paste Command
```bash
# After AI creates output/react-express-instance/
cp -r output/react-express-instance/* ~/your-project/
cd ~/your-project && chmod +x .claude/hooks/*.sh
```

---

## For Template Maintainers: Internal Workflow

This section is for maintainers who enhance this adaptation template.

### When a User Requests Setup

The AI follows this workflow:

1. **User Prompt:** "Create instance using React + Express"
2. **AI Action:** Reads `TEMPLATE_USAGE.md` for detailed steps
3. **AI Creates:** `output/react-express-instance/` with:
   - All agents copied
   - Hooks configured
   - Skills selected (skill-developer + template skills)
   - `skill-rules.json` with project-specific paths
   - `settings.json` customized
   - `AGENT_SETUP_VERIFY.md` for verification

4. **AI Instructs:** Copy command to user's project

### Maintaining the Template

**Golden Rule:** Never modify template files with tech-specific code.

**Additions to this template should:**
- Be tech-agnostic
- Work as building blocks
- Support the `output/` pattern

**See `TEMPLATE_USAGE.md` for:** Detailed questionnaire, customization examples, and complete workflow.

---

## Usage Examples

### Using an Agent (Tech-Agnostic)

**Example: Review your architecture**
```
User: "Use the code-architecture-reviewer agent to check my controllers"

Agent will:
- Analyze all controller files
- Check for pattern consistency
- Validate against best practices
- Return detailed report with fixes
```

**Example: Plan a refactor**
```
User: "Use the refactor-planner agent to plan breaking down Dashboard.tsx"

Agent will:
- Analyze the component
- Suggest extraction strategy
- Create step-by-step plan
- Estimate effort
```

### Skills Auto-Activate

Skills activate based on **file patterns and keywords**, working with any tech stack:

```
User: "Create a new route for user profile"

Skill reads your skill-rules.json:
- Checks if you're editing backend files
- Matches against keyword "route"
- Suggests relevant patterns from the template

You write your code - skill provides guidance
for YOUR framework (Express, Fastify, NestJS, etc.)
```

### Using Dev Docs

**For complex tasks spanning multiple sessions:**

```bash
# Start a task
/dev-docs implement multi-service architecture

# Creates 3 files in dev/active/implement-multi-service-architecture/
# - plan.md: Strategic overview
# - context.md: Current state & decisions
# - tasks.md: Checklist

# After context reset:
# Claude reads these files and resumes instantly
```

---

## Customization

### Path Patterns

**This is the most important customization.** Update `.claude/skills/skill-rules.json` to match your project structure:

```json
{
  "skills": {
    "your-skill-name": {
      "fileTriggers": {
        "pathPatterns": [
          "src/**/*.ts",           // ← Update these paths!
          "backend/**/*.ts",
          "services/**/*.ts"
        ]
      }
    }
  }
}
```

**Example Common patterns:**
- `**/*.ts` - All TypeScript files
- `api/**/*.ts` - API routes only
- `src/**/controller/*.ts` - Controller patterns
- `frontend/**/*.tsx` - React components

### Selecting Skills

**The template provides example skills.** Choose based on your needs:

- **skill-developer**: Always include - lets you create new skills
- **Other skills**: Copy as templates, then adapt for your tech stack

Example flow:
```
User has: Vue 3 + Fastify + MongoDB
→ Copy: skill-developer
→ Copy: backend-dev-guidelines (as template)
→ Create: vue-fastify-skill (custom)
```

### Configure settings.json

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
    "name": "your-project-name",
    "type": "monorepo" | "single-app" | "microservices"
  }
}
```

---

## Directory Structure

### Template Root (This Repository)
```
.claude/
├── agents/          # 10 specialized agents (tech-agnostic)
├── hooks/           # 2 essential hooks + config
├── skills/          # 5 example skills + skill-rules.json
└── README.md        # Per-skill documentation

dev/                 # Dev docs pattern methodology
└── README.md

README.md            # This file (master overview)
TEMPLATE_USAGE.md    # For maintainers creating output/ setups
output/              # User-specific setups (gitignored)
```

### After Installation (User Project)
```
your-project/
├── .claude/
│   ├── agents/
│   │   ├── code-architecture-reviewer.md
│   │   ├── code-refactor-master.md
│   │   └── ... (all 10 agents)
│   ├── hooks/
│   │   ├── skill-activation-prompt.sh    # Make executable!
│   │   ├── skill-activation-prompt.ts
│   │   ├── post-tool-use-tracker.sh      # Make executable!
│   │   ├── package.json
│   │   └── package-lock.json
│   ├── skills/
│   │   ├── skill-rules.json              # UPDATE THIS!
│   │   ├── skill-developer/              # Create new skills
│   │   └── ... (other skills as needed)
│   └── settings.json                     # Hook configuration
└── dev/
    ├── README.md                         # Dev docs guide
    └── active/                           # Your task docs
```

---

## Verification Checklist

After setup, verify:

- [ ] `.claude/hooks/*.sh` files are executable (`chmod +x`)
- [ ] `skill-rules.json` has correct path patterns for your project
- [ ] `package.json` and `package-lock.json` exist in `.claude/hooks/`
- [ ] `settings.json` is properly formatted
- [ ] At least one skill directory exists in `.claude/skills/`

**Quick commands:**
```bash
# Check hooks executable
ls -la .claude/hooks/*.sh

# Validate JSON
cat .claude/settings.json | jq .

# Test hooks
cd .claude/hooks && npx ts-node skill-activation-prompt.ts
```

---

## Troubleshooting

### Skills not activating?
1. Check `.claude/skills/skill-rules.json` has your file paths
2. Verify hooks are executable (`chmod +x .claude/hooks/*.sh`)
3. Check `settings.json` lists the hooks

### Agents not working?
Agents are standalone `.md` files - should work immediately.
Usage: "Use the [agent-name] agent to [task]"

### Hook errors?
```bash
cd .claude/hooks && npm install
chmod +x *.sh
```

---

## Common Workflows

### 1. Code Review
```
User: "Use code-architecture-reviewer to check my controllers"
→ Returns analysis and fixes
```

### 2. Complex Tasks
```
User: "/dev-docs implement feature X"
→ Creates plan/context/tasks files

User: "Build using the plan"
→ Skills auto-suggest patterns

User: "Use plan-reviewer to validate"
→ Checks approach
```

### 3. Debugging
```
User: "Use frontend-error-fixer on build errors"
→ Analyzes and suggests fixes
```

### 4. Refactoring
```
User: "/dev-docs refactor module"
User: "Use refactor-planner for strategy"
User: "Use code-refactor-master to execute"
```

---

## Key Principles

1. **Tech-Agnostic**: Works with any framework, language, or architecture
2. **Agents**: Standalone `.md` files - copy and use immediately
3. **Skills**: Auto-activate based on YOUR file paths and keywords
4. **Hooks**: Enable automation - just make them executable
5. **Dev Docs**: Survive context resets for complex multi-session work
6. **Template**: Stays pure - customization happens in user projects via `output/`

---

## For Template Maintainers

This is a **template repository** - never add tech-specific code here.

**When users request setup:**
1. Read `TEMPLATE_USAGE.md`
2. Create `output/[project-name]/` with customized configs
3. Users copy from `output/` to their project
4. Template remains generic and reusable

The `output/` approach keeps this template universal while allowing infinite customization.

---

## More Information

- **Agents**: `.claude/agents/README.md` - Full agent documentation
- **Skills**: `.claude/skills/README.md` - Skill setup & configuration
- **Hooks**: `.claude/hooks/README.md` - Hook installation & troubleshooting
- **Dev Docs**: `dev/README.md` - Context management methodology
- **Workflow**: `TEMPLATE_USAGE.md` - Complete maintainer guide

---

**Version:** 1.0
**Last Updated:** 2025-12-18
**Tech Philosophy:** Universal, adaptable, framework-agnostic
