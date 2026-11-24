---
inclusion: always
---
# Tech

- A **live web app that runs in the browser**: **TypeScript + Vite**, no backend, no accounts, no API keys. It deploys as static files to **Cloudflare Pages** (free) from the `main` branch.
- Tests: **Vitest** for unit tests and **fast-check** for property-based tests of every safety rule. `npm test` runs them all; `npm run build` must pass before any merge to `main`.
- Layout (at the repo root, next to `.kiro/`):
  - `src/core/` safety core (lamp state machine, conflict table, Safety Lock). No imports from the rest of the app.
  - `src/sim/` traffic micro-simulation (vehicles, queues, discharge, seeded randomness).
  - `src/controllers/` fixed-time, actuated, pre-emption, two-regime trigger, recovery, modes and fallback ladder.
  - `src/detect/` simulated camera, siren and GPS/dispatch, plus the fusion rules.
  - `src/ui/` the dashboard (junction drawing, countdown panel, controls, bilingual sign, results).
  - `src/config.ts` **one** file with every tunable value (amber, all-red, minimum greens, gap, leads, vehicle shares, seeds), each marked ASSUMPTION or with its source.
  - `tests/` mirrors `src/`.
- Drawing: SVG or Canvas, no heavy game engine. Smooth on a mid-range phone.
- Small functions, clear names, plain-English comments, strict TypeScript.
- Windows PC, Node.js LTS. Explain any install step one command at a time.
- Open-source libraries only, with their licences listed in the README.
