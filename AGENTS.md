# Repository Guidelines

## Project Structure

NailFlow is an internal salon dashboard built with React 19, React Router 8, TypeScript, Vite 8, and Tailwind CSS 4.

- `app/routes.ts` registers routes, and `app/routes/home.tsx` is the dashboard entry point. `app/root.tsx` defines the shared document layout.
- `app/features/dashboard/` owns the dashboard. Organize feature code by type in `pages/` for screen composition, `components/` for UI, `model/` for data contracts, and `data/` for sample data or data access.
- `app/app.css` holds global styles. Use `DESIGN.md` as the dashboard design reference. Put static assets that need a public URL in `public/`.

## Build, Test, and Development

Use Node.js 24 to match GitHub Actions.

- `npm ci` installs dependencies from `package-lock.json`.
- `npm run dev` starts the development server, typically at `http://localhost:5173`.
- `npm run typecheck` generates React Router types and runs TypeScript. `npm test` runs the same check through the CI entry point.
- `npm run build` creates the production build. Run `npm run start` afterward to serve it locally.

## Coding Style and Naming

Use the container/presentational pattern. Route modules supply data and wire up navigation. Feature pages compose the screen and pass typed props to components. When a feature needs server data, call its data access functions from a React Router loader or action. Create folders as needed and move UI into `app/components/` when multiple features share it.

Follow the surrounding TypeScript and JSX style. Use two-space indentation, double quotes in imports, and semicolons. Name component files and components in PascalCase, such as `MetricCard.tsx`, and use camelCase for data modules, such as `dashboardData.ts`. Follow the lowercase route filename pattern in `app/routes/home.tsx`. Use Tailwind utilities for component styles and follow the design reference for visual changes. The project has no configured formatter or linter.

## Testing

Run `npm test` and `npm run build` before opening a PR. The repository currently uses type checking as its automated test and defines no test framework, test filename convention, or coverage threshold. For UI changes, open the dashboard locally and verify the affected behavior at desktop and narrow viewport widths.

## Branches, Commits, and Pull Requests

Name new work branches `type/short-change-description`. Use the same types as for commits. Write the name in lowercase English and separate words with hyphens, as in `feat/add-appointment-filters` or `fix/redirect-active-sessions`.

Write commit messages in English and lowercase using `type: short description`. Use a bare type such as `feat`, `fix`, or `docs`. Examples include `fix: redirect active sessions to the dashboard` and `docs: document commit conventions`.

Open PRs against `main`, explain what changed and how you verified it, link any related issue, and include screenshots when the UI changes.
