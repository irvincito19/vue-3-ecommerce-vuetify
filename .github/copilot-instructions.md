<!-- .github/copilot-instructions.md - Guidance for AI coding agents working on this repo -->
# Project snapshot

This repository is a small Vue 3 + TypeScript app scaffolded for an e-commerce demo. It uses Vite as the bundler, Pinia for state, Vue Router for routing, and `script setup` single-file components.

**Quick start (commands)**
- Install: `npm install`
- Dev server: `npm run dev` (runs `vite`)
- Build (with type-check): `npm run build` (runs `type-check` then `build-only`)
- Preview production build: `npm run preview`
- Type check only: `npm run type-check` (runs `vue-tsc --build`)
- Lint: `npm run lint` (runs both `lint:oxlint` and `lint:eslint`)

**Where to look first**
- App entry: `src/main.ts` — creates the app, installs Pinia and the router, and mounts `<App/>`.
- Router: `src/router/index.ts` — route definitions; `About` is lazy-loaded using dynamic import.
- State: `src/stores/*` — Pinia stores using the Composition API style (see `src/stores/counter.ts`).
- Views and components: `src/views/*` and `src/components/*` — components use `<script setup lang="ts">` and SFCs.
- Vite config & aliases: `vite.config.ts` — sets `@` => `src` and enables dev plugins (e.g. `vite-plugin-vue-devtools`).

**Important repo conventions and patterns**
- TypeScript + `script setup`: Components use `lang="ts"` and `script setup`. Prefer the Composition API idioms already used in stores and components.
- Pinia stores use `defineStore` with the setup-style API that returns refs/computeds/functions (see `src/stores/counter.ts`).
- Path alias: import `@/...` to reference files under `src` (configured in `vite.config.ts`). Keep imports consistent with this alias.
- Route lazy-loading: follow the existing pattern for larger routes (use dynamic `() => import('...')`).
- Dev-only helper: `TheWelcome.vue` triggers a fetch to `/__open-in-editor?file=README.md` — this is a development helper, not a production API.

**Build & CI considerations**
- The `build` script runs type-checking first (`vue-tsc --build`) — do not bypass type checks when changing types or public APIs.
- Linting uses two flows: `oxlint` and `eslint`. `npm run lint` runs both (via `npm-run-all2` / `run-s`). Use the same commands to keep CI parity.

**Files that commonly change together**
- When adding a new page: add a view in `src/views`, register route in `src/router/index.ts` (prefer lazy-load), and add navigation in `App.vue` or the relevant component.
- When adding global styles: update `src/assets/main.css` or `src/assets/base.css`.

**Examples (explicit references)**
- App bootstrap: `src/main.ts` — lines where Pinia/router are applied.
- Small store example: `src/stores/counter.ts` — demonstrates ref/computed/defineStore pattern.
- Route example: `src/router/index.ts` — shows `createWebHistory(import.meta.env.BASE_URL)` and lazy route for About.
- Dev helper usage: `src/components/TheWelcome.vue` — uses the `/__open-in-editor` endpoint and lists tooling suggestions.

**If you add tests**
- There are no tests configured by default. The project mentions Vitest/Cypress/Playwright in `TheWelcome.vue`. If adding tests, follow the Vite + Vitest setup: add `vitest` and configuration in `vite.config.ts` or a separate `vitest.config.ts`.

**What to avoid changing without confirmation**
- `vite.config.ts` aliases and dev plugins — other parts rely on `@` alias.
- `package.json` scripts that chain lint/type-check/build — CI may expect those commands.

If anything in this file is unclear or you'd like more detail (for example: preferred testing setup, component naming conventions, or sample PR/branching workflows), tell me which area to expand and I will iterate.
