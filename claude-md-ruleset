Here is a **generic, template-based version** of the `CLAUDE.md` file. It abstracts the specific technologies (Next.js, Scaleway, etc.) into architectural patterns while maintaining the strict rigor, safety protocols, and structure of your original file.

Please fill in the `{{PLACEHOLDERS}}` with the tech stack appropriate to this project that you can find inside of PRD and/or the architecture documemt inside docs.

***

# CLAUDE.md - Build Standards & Architecture

## 1. AI & Inference Strategy (CRITICAL)

Define the model hierarchy to balance cost vs. intelligence. **Do not hallucinate model names.**

```typescript
// Example Implementation Pattern
export const models = {
  logic: provider.chat('{{HIGH_IQ_MODEL}}'),      // Complex reasoning, code generation
  fast: provider.chat('{{LOW_LATENCY_MODEL}}'),   // Routing, simple text, classifying
  embedding: '{{EMBEDDING_MODEL}}',               // Dimensions: {{DIMENSIONS}}
};
```

**Model Selection Rules:**
- **Logic Model:** Use for architectural decisions, complex refactoring, and verification.
- **Fast Model:** Use for simple UI copy, categorization, or initial routing.
- **Embedding Model:** Must match Vector DB dimensions strictly.

## 2. Package Management

**System Standard: pnpm**
- **Strict Rule:** Do not mix npm/yarn/pnpm. Lockfile conflicts break CI/CD.
- **Command:** `pnpm install | add | run`

## 3. Project Structure & Organization

Maintain separation of concerns. Do not mix business logic inside UI components.

```
project_root/
├── src/
│   ├── {{APP_ROUTER}}/      # Routes/Pages only
│   ├── components/          # Pure UI components (dumb)
│   ├── features/            # Feature-specific logic (smart)
│   ├── lib/                 # Singletons (DB, AI clients, Utils)
│   └── hooks/               # State logic
├── {{DB_FOLDER}}/           # Schema & Migrations
├── docs/                    # Architecture decisions (ADRs) & Specs
└── public/                  # Static assets
```

## 4. Tech Stack (Immutable)

| Layer | Technology | Region/Constraint | Purpose |
|-------|------------|-------------------|---------|
| Frontend | {{FRAMEWORK}} | {{REGION}} | UI & Client Logic |
| Database | {{DB_PROVIDER}} | {{REGION}} | Relational Data |
| Vector DB | {{VECTOR_PROVIDER}} | {{REGION}} | Semantic Search |
| AI Provider | {{AI_PROVIDER}} | {{REGION}} | Inference |

## 5. Data Access Layer

**Connection Rules:**
- Use connection pooling for Serverless/Edge environments.
- Use direct connections ONLY for migrations/deployments.

**ORM/Query Builder Standards:**
1. **Singleton Pattern:** Always import the DB client from a centralized `lib/db` file. Never instantiate a new client inside a route.
2. **Migrations:**
   - Commit schema and migration files together.
   - **NEVER** edit a migration file after it is applied.
   - **BANNED:** Commands that overwrite schema from DB (e.g., `db pull --force`) without backup.

## 6. Vector Database & RAG

```typescript
// Configuration Logic
// MUST match the Embedding Model dimensions exactly
await vectorDB.createCollection("{{COLLECTION_NAME}}", {
  vectors: { size: {{DIMENSIONS}}, distance: "Cosine" },
});
```

**Rule:** If the embedding model changes, a full database re-index is required.

## 7. Styling & UI Architecture

**Framework:** {{CSS_FRAMEWORK}} / {{UI_LIBRARY}}

**Rules:**
1. **Variables:** Use CSS variables for all colors/spacing (theme-able). No hardcoded hex values in components.
2. **Merging:** Use a utility (like `cn` or `clsx`) to merge tailwind/CSS classes.
   ```typescript
   // Correct
   className={cn("base-styles", condition && "active-styles")}
   ```
3. **Colocation:** Keep styles near the component or in a global theme file.

## 8. Type Safety & Code Quality

- **Strict Mode:** Enabled.
- **No `any`:** Use `unknown`, Generics, or specific interfaces.
- **Generated Types:** Prioritize types generated from the DB Schema (Single Source of Truth).
- **File Limits:**
  - Components: < 250 lines (break into sub-components).
  - Logic/API: < 200 lines (extract services).

## 9. API & Security Patterns

**Workflow:**
1. **Authenticate:** Check user session immediately.
2. **Validate:** Zod/Schema validation on all inputs.
3. **Execute:** Perform DB/AI operations.
4. **Error Handle:** Wrap in Try/Catch and return standardized error objects.

```typescript
// Pattern
export async function action(input: InputType) {
  const session = await auth();
  if (!session) throw new Error("Unauthorized");
  
  // ... logic
}
```

## 10. Data Sovereignty & Compliance

**Region Lock:** {{ALLOWED_REGIONS}}
- **Constraint:** No user data may leave the defined region(s).
- **AI Processing:** Ensure the AI inference endpoint is hosted within the compliance zone.

## 11. Git & Version Control

**BANNED COMMANDS:**
- `git reset --hard` (unless explicitly authorized for cleanup)
- `git clean -fd`
- `git push --force` on shared branches

**Workflow:**
- Feature Branch (`feat/name`) -> Pull Request -> Main.
- Commit messages must be descriptive.

## 12. Version Pinning

Keep core infrastructure stable.

```json
{
  "{{FRAMEWORK}}": "{{VERSION}}",
  "{{DB_CLIENT}}": "latest",
  "{{AI_SDK}}": "latest"
}
```

## 13. Quick Reference

| Do | Don't |
|---|---|
| Use `pnpm` | Use `npm` or `yarn` mixed |
| Import singletons (`lib/`) | `new Client()` in routes |
| Use CSS Variables | Hardcode Hex codes |
| `git reset --soft` | `git reset --hard` |
| Validate inputs (Zod) | Trust client inputs |
| Check Auth first | Run logic then check Auth |

## 14. Environment Variables

Ensure these are set in `.env.local` and CI/CD:

```env
# Database
DATABASE_URL=
DIRECT_URL=

# AI & Vector
AI_API_KEY=
VECTOR_DB_URL=
VECTOR_DB_KEY=

# Auth
AUTH_SECRET=
```
