# Claude Code React + TypeScript Template

A production-ready template for React + TypeScript projects with Claude Code's skill auto-activation system. This template includes best practices, development guidelines, and automated workflows to maintain code quality.

## What's Included

### Skills (Auto-Activating Development Guidelines)
- **frontend-dev-guidelines** - React/TypeScript/MUI v7 patterns (BLOCKING guardrail)
- **backend-dev-guidelines** - Node.js/Express/TypeScript patterns
- **skill-developer** - Meta-skill for creating custom skills
- **route-tester** - API testing with JWT authentication

### Hooks (Automation System)
- **skill-activation-prompt** - Automatically suggests relevant skills based on:
  - Keywords in your prompts
  - Files you're editing
  - Code patterns detected
- **post-tool-use-tracker** - Tracks file changes for context awareness

### Agents (Specialized Task Handlers)
- **code-architecture-reviewer** - Comprehensive code review against project standards and best practices
- **web-research-specialist** - Expert internet researcher for technical problem solving

### Configuration
- Pre-configured `skill-rules.json` with React/TypeScript paths
- `.gitignore` for clean repositories
- Hook dependencies ready to install

## Quick Start

### 1. Clone This Template
```bash
git clone <your-repo-url> my-new-project
cd my-new-project
```

### 2. Install Hook Dependencies
```bash
cd .claude/hooks
npm install
cd ../..
```

### 3. Start Your Project
```bash
# Initialize your own project structure
npm init -y
# or
npm create vite@latest . -- --template react-ts
```

### 4. Customize (Optional)
Edit `.claude/skills/skill-rules.json` to match your project structure:
- Update `pathPatterns` for your directory layout
- Add domain-specific keywords
- Adjust enforcement levels

## How It Works

### Auto-Activation
Skills automatically suggest themselves when you:
- Mention keywords: "React component", "MUI", "backend", "API route"
- Edit files: `src/**/*.tsx`, `src/api/**/*.ts`
- Write code: `import React`, `<Grid`, `router.get()`

### Example
```
You: "I want to create a new React component with MUI"

Claude Code will see:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 SKILL ACTIVATION CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📚 RECOMMENDED SKILLS:
  → frontend-dev-guidelines

ACTION: Use Skill tool BEFORE responding
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Available Skills

### Frontend Development Guidelines
**Path:** `.claude/skills/frontend-dev-guidelines/`

Comprehensive React/TypeScript/MUI v7 patterns including:
- Component patterns with Suspense
- Data fetching (TanStack Query)
- MUI v7 compatibility (Grid uses `size={{}}` not `xs/sm`)
- Performance optimization
- TypeScript standards

**Enforcement:** BLOCKING (prevents MUI v6→v7 migration errors)

### Backend Development Guidelines
**Path:** `.claude/skills/backend-dev-guidelines/`

Node.js/Express/TypeScript patterns including:
- Layered architecture (Routes → Controllers → Services → Repositories)
- BaseController pattern
- Prisma ORM patterns
- Zod validation
- Sentry error tracking

**Enforcement:** SUGGEST (helpful guidance)

### Skill Developer
**Path:** `.claude/skills/skill-developer/`

Meta-skill for creating custom skills:
- Trigger types (keywords, intent patterns, file patterns)
- Configuration schema
- Hook mechanisms
- Troubleshooting guide

### Route Tester
**Path:** `.claude/skills/route-tester/`

API testing with JWT cookie-based authentication patterns.

## Available Agents

Agents are specialized autonomous task handlers that can be invoked using the Task tool for complex, multi-step operations.

### Code Architecture Reviewer
**Path:** `.claude/agents/code-architecture-reviewer.md`

Conducts comprehensive code reviews across your full tech stack:
- **Quality Assessment** - TypeScript strictness, error handling, naming conventions
- **Design Scrutiny** - Identifies technical debt and non-standard approaches
- **Integration Validation** - API patterns, database operations
- **Architectural Fit** - Code placement, separation of concerns

**Usage:** Invoke after completing major features for quality assurance
**Output:** Saves findings to `./dev/active/[task-name]/[task-name]-code-review.md`
**Model:** Sonnet (cost-effective for analysis)

### Web Research Specialist
**Path:** `.claude/agents/web-research-specialist.md`

Expert internet researcher for technical problem solving:
- Crafts 5-10 search query variations for comprehensive coverage
- Searches GitHub issues, Reddit, Stack Overflow, forums, blogs, docs
- Specializes in debugging assistance and finding similar issues
- Provides executive summaries with actionable recommendations

**Usage:** Invoke when stuck on errors, need library comparisons, or architectural decisions
**Output:** Structured findings with sources and recommendations

### How to Use Agents

Agents are invoked through Claude Code's Task tool:

```
User: "Review the authentication code I just wrote"
Claude: [Uses Task tool with agent: code-architecture-reviewer]

User: "Research best practices for React state management in 2025"
Claude: [Uses Task tool with agent: web-research-specialist]
```

You can also explicitly request an agent:
```
"Use the code architecture reviewer to analyze my latest changes"
"Have the web research specialist find solutions for this error"
```

## Customizing for Your Project

### Update Path Patterns
Edit `.claude/skills/skill-rules.json`:

```json
"frontend-dev-guidelines": {
  "fileTriggers": {
    "pathPatterns": [
      "src/**/*.tsx",           // Your frontend path
      "app/**/*.tsx",           // Or app directory
      "packages/ui/**/*.tsx"    // Or monorepo package
    ]
  }
}
```

### Add Custom Keywords
```json
"promptTriggers": {
  "keywords": [
    "component",
    "your-custom-term",
    "domain-specific-word"
  ]
}
```

### Adjust Enforcement
```json
"enforcement": "suggest"  // Non-blocking suggestions
"enforcement": "block"    // Requires skill before proceeding
"enforcement": "warn"     // Shows warning but allows
```

## File Structure

```
.
├── .claude/
│   ├── skills/
│   │   ├── backend-dev-guidelines/     (12 files)
│   │   ├── frontend-dev-guidelines/    (11 files)
│   │   ├── skill-developer/            (7 files)
│   │   ├── route-tester/               (1 file)
│   │   └── skill-rules.json            (master configuration)
│   │
│   ├── agents/
│   │   ├── code-architecture-reviewer.md
│   │   └── web-research-specialist.md
│   │
│   ├── hooks/
│   │   ├── skill-activation-prompt.sh
│   │   ├── skill-activation-prompt.ts
│   │   ├── post-tool-use-tracker.sh
│   │   ├── package.json
│   │   └── node_modules/               (gitignored)
│   │
│   └── settings.json                    (hook configuration)
│
├── .gitignore
├── README.md
└── INFRASTRUCTURE_SUMMARY.md            (detailed documentation)
```

## Maintenance

### Update Skills
Skills are just markdown files - edit them directly:
```bash
vim .claude/skills/frontend-dev-guidelines/SKILL.md
```

### Add New Skills
1. Create skill directory: `.claude/skills/my-skill/`
2. Add `SKILL.md` with frontmatter
3. Register in `skill-rules.json`
4. Test with manual activation

See `skill-developer` skill for detailed instructions.

### Test Hook System
```bash
export CLAUDE_PROJECT_DIR="$(pwd)"
echo '{"session_id":"test","transcript_path":"/tmp/test","cwd":"'$(pwd)'","permission_mode":"acceptEdits","prompt":"create a React component"}' | bash .claude/hooks/skill-activation-prompt.sh
```

## Tech Stack Compatibility

### Frontend
- React 18+
- TypeScript
- MUI v7 (Material-UI)
- TanStack Query
- TanStack Router
- Vite

### Backend
- Node.js
- Express
- TypeScript
- Prisma ORM
- Zod validation
- Sentry error tracking

### Flexible
You can remove skills that don't match your stack or create custom ones.

## Tips

1. **Start small** - Use 1-2 skills initially, add more as needed
2. **Customize paths** - Match your actual project structure
3. **Read skill content** - Each skill has detailed patterns and examples
4. **Create custom skills** - Use `skill-developer` to build project-specific skills
5. **Adjust enforcement** - Change from "block" to "suggest" if too restrictive

## Troubleshooting

### Skills not activating?
1. Check `skill-rules.json` pathPatterns match your files
2. Verify hooks are registered in `.claude/settings.json`
3. Run hook test command (see Maintenance section)

### Node modules issues?
```bash
cd .claude/hooks
rm -rf node_modules package-lock.json
npm install
```

### Want to disable a skill?
Remove it from `skill-rules.json` or set `"enforcement": "warn"`.

## Credits

Skills and infrastructure based on [claude-code-infrastructure-showcase](https://github.com/diet103/claude-code-infrastructure-showcase) by diet103.

## License

MIT - Use freely for your projects
