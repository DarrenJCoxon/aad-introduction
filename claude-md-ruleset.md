NOTE TO AI AGENT: Please review the below sample CLAUDE.md file and amend to suit this project. Read the PRD, architecture, UI UX and epics and edit to suit. DO NOT exceed the number of lines of this CLAUDE.md to avoid passing unecessary information to the AI agents:

---

## Package Manager
Use `pnpm` exclusively. Never npm or yarn. Add dependencies to the correct workspace package.json (apps/web, packages/db, packages/types, packages/ui) — not root.


## 250-Line Limit
All logic files (.tsx, .ts, route.ts, actions.ts, .test.ts) MUST be < 250 lines. Exempt: schema.prisma (or drizzle equivalent), package.json, config files, .md files.

## No Hard-Coded Styles
NEVER write Tailwind utility classes or inline styles in components. ALL UI must use pre-styled shadcn components from `apps/web/src/components/ui/`. This is the single most important rule — the design system is baked into the components. Compose them, don't customize with raw classes.

## No Hard-Coded Strings, Routes, gradients, or Emojis
- User-facing strings: define in constants file, then import
- URL paths: import from routes file
- Icons: use Lucide React (`lucide-react`), never emojis
- Gradients: never use generic gradients: these make apps look like they were coded with AI and must be avoided

## Service Layer
Never call Prisma/Drizzle or external APIs (Stripe, Qdrant, OpenRouter) directly from routes/actions/components. All such logic must go through service functions in `services/(backend)/`.

## Type Safety
- Import Prisma/Drizzle types from `packages/db`, Zod schemas from `packages/types` — never duplicate types
- Never use `: JSX.Element` as a return type (causes build errors). Omit it or use `React.ReactNode`

## Validation
All API route and Server Action inputs must be validated with Zod schemas from `packages/types`.

## Auth
NextAuth.js v5 (Auth.js). Database sessions only — never JWT. Never write session tokens to localStorage.

## Git Workflow
- Feature branches from `staging`. PRs against `staging`. Only `staging` merges to `main`
- Never bare `git stash` — always `git stash --include-untracked` to avoid losing untracked files
- Never use force commands

## QA After Every Story
When implementing stories: Implement -> QA Validate (qa-validator agent) -> Fix -> next story. Never skip QA or batch stories without validating each one.

## Testing
Always ensure Vitest is used and never skipped. All tests must pass before the story can be marked as complete. There can be no exceptions. 

## Supabase Port Quirk
Port 5432 (session pooler) for migrations. Port 6543 (transaction pooler) for app runtime. If migrations hang, check the port.
