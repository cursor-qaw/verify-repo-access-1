# AGENTS.md

## Cursor Cloud specific instructions

### Workspace layout

This workspace contains **two independent git repositories** under `/agent/repos/`:

| Directory | Remote | App |
|-----------|--------|-----|
| `verify-repo-access-1` | `cursor-qaw/verify-repo-access-1` | Create React App todo SPA (this repo) |
| `verify-repo-access-2` | `cursor-qaw/verify-repo-access-2` | Same app (separate clone) |

There is no backend, database, or Docker. Each repo is a standalone frontend with in-memory state.

### Running services

Only one CRA dev server can bind port **3000** by default. To run both repos simultaneously, set `PORT` for the second instance (e.g. `PORT=3001 npm start`).

Standard CRA commands (run from inside each repo directory):

- **Dev server:** `BROWSER=none npm start` → http://localhost:3000
- **Tests (CI):** `CI=true npm test -- --watchAll=false`
- **Build:** `npm run build`

See `README.md` for the full CRA script reference.

### Lint note

`npx eslint src` reports a parse error in `src/special-number.js` (legacy octal literal). This file is an intentional fixture and is not imported by the app. `npm run build` compiles successfully.

### Multi-repo workflow

Run git commands from the correct repo directory. Both repos share the same structure and scripts.
