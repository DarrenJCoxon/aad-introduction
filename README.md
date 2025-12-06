# Usage Guide

### For New Projects

1. **Create CLAUDE.md** in project root
   - Customize tech stack section
   - Add project-specific standards

2. **Create `.claude/agents/`** folder
   - Add agent templates you need
   - Customize for your workflow

3. **Create `docs/stories/`** folder
   - Use story template for new work

### Workflow

```
1. Scrum Master creates story → Status: Draft
2. Team reviews and approves → Status: Approved
3. Developer implements → Status: Review
4. QA validates → Status: Done
```

### Invoking Agents

When using Claude Code, reference agents by name:
- "Use the scrum-master agent to create a story for..."
- "Use the story-implementer agent to build this feature..."
- "Use the qa-validator agent to review this story..."
- "Use the debugger agent to investigate this issue..."

---

## 5. Customization Tips

### Adapt for Your Stack

**React Native:**
- Change file organization for mobile structure
- Update styling to use StyleSheet or styled-components

**Vue/Nuxt:**
- Adjust component patterns for Vue SFCs
- Update imports and file extensions

**Python/Django:**
- Replace Prisma with Django ORM patterns
- Update test framework to pytest

**Different Package Managers:**
- Replace `pnpm` with your choice
- Update all command examples

### Add Project-Specific Rules

Add sections for:
- Specific libraries (e.g., "Always use date-fns, never moment.js")
- API patterns (e.g., "All endpoints must return pagination metadata")
- Naming conventions (e.g., "Use kebab-case for file names")
- Deployment requirements

---

**Last Updated:** December 2024
**License:** MIT - Use freely in your projects
