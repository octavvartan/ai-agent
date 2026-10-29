# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This is an early-stage TypeScript project. The goal is an AI agent service. At this time, the code is
one Express server in `src/index.ts` with one route (`GET /health`). The `@anthropic-ai/sdk` package
is installed, but no code uses it yet.

## Commands

- `npm run dev` — run `src/index.ts` with `tsx` in watch mode (no build step).
- `npm run build` — compile `src/` to `dist/` with `tsc`.
- `npm start` — run the compiled server from `dist/index.js`. Run `npm run build` first.
- `npm run typecheck` — type check only, no output files.
- `npm run format` / `npm run format:check` — Prettier write / check.

There is no test runner and no linter. `npm test` fails on purpose. Use `npm run typecheck` and
`npm run format:check` to verify changes.

The server port comes from the `PORT` environment variable (default `3000`). `.env` is in
`.gitignore`. `npm run dev` and `npm start` load it with `--env-file-if-exists=.env`. If the file
does not exist, the server starts without it.

## Toolchain constraints

- Node.js `>=24`, TypeScript 7, native ESM (`"type": "module"`).
- `module`/`moduleResolution` is `nodenext`. Relative imports must use the `.js` extension
  (for example, `import { x } from "./agent.js"` for `src/agent.ts`).
- `verbatimModuleSyntax` is on. Import types with `import type` or the inline `type` modifier,
  as `src/index.ts` does for `Request` and `Response`.
- `strict` and `noUncheckedIndexedAccess` are on. An index access on an array or a record gives
  `T | undefined`, so the code must handle `undefined`.
- Prettier: double quotes, semicolons, trailing commas, line width 100.
