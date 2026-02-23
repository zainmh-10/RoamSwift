# Repository Guidelines

## Project Structure & Module Organization
Primary application code lives in `src/` using Next.js App Router.
- `src/app/`: route segments, page components, global layout/styles, and API routes under `src/app/api/*/route.ts`.
- `src/components/`: reusable UI components (PascalCase files, e.g., `Header.tsx`).
- `src/lib/`: client/server utilities and hooks (`use*` hooks in camelCase, server helpers in `src/lib/server/`).
- `src/types/`: shared TypeScript interfaces.
- `data/mock-db.json`: file-backed mock persistence used by API endpoints.
- `scripts/api-security-check.mjs`: integration-style API/security smoke checks.

## Build, Test, and Development Commands
Use Node 20+ and npm.
- `npm run dev`: start local dev server (Turbopack) at `http://localhost:3000`.
- `npm run build`: create a production build.
- `npm run start`: run the production server from the build output.
- `npm run lint`: run ESLint across the repo.
- `npm run typecheck`: run strict TypeScript checks with no emit.
- `npm run security:test`: run API/security checks (starts the app and validates endpoint behavior).

CI (`.github/workflows/ci.yml`) runs: `lint`, `typecheck`, `security:test`, `build`. Keep local changes passing these before opening a PR.

## Coding Style & Naming Conventions
- Language: TypeScript (`strict: true`) with React 19 + Next.js 16.
- Indentation: 2 spaces; keep formatting consistent with existing files.
- Components: PascalCase (`ImageGrid.tsx`); hooks/utils: camelCase (`useAppData.ts`).
- API handlers: `route.ts` under the corresponding `src/app/api/<feature>/` folder.
- Use `@/*` import alias for `src/*` where practical.
- Styling uses Tailwind CSS v4 utility classes in JSX.

## Testing Guidelines
There is currently no Jest/Vitest suite. Validation is centered on:
- `npm run typecheck`
- `npm run lint`
- `npm run security:test`

When adding or changing API behavior, extend `scripts/api-security-check.mjs` with a focused scenario and expected status/error shape.

## Commit & Pull Request Guidelines
Git history is minimal (`Initial commit`), so follow a clear, short, imperative subject line (for example: `Add leaderboard input validation`).
- Keep commits scoped to one logical change.
- PRs should include: purpose, key files changed, test evidence (command outputs), and screenshots for UI updates.
- Link related issues/tasks when applicable.
