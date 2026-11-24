# Kolkata Green Corridor (app): instructions for every AI tool

This is the **public app repo**. Kiro builds it for Kiroween 2026. It deploys live to Cloudflare Pages from `main`.

## Read first
1. `README.md`, then `docs/STATE.md` and `docs/DECISIONS.md`.
2. `docs/DEMO-BRIEF.md` (what to build) and `docs/KIRO-PLAN.md` (how to use Kiro fully).
3. Kiro also reads `.kiro/steering/` on every prompt.

## Roles
| Who | Role | Where | Never |
|---|---|---|---|
| **Kiro** | **Builder** | Branch `kiro` | — |
| **Rajdeep** | Owner: prompts Kiro, tests, merges `kiro` into `main`, deploys, records the video, submits | all | — |
| **Claude** | Side reviewer only: reads commits, reports bugs in plain English | No branch here; works in the private research repo | Write or fix app code, specs, hooks or steering in this repo |
| **Gemini** | Optional second fact-checker; images | — | App code |

Devin, Cursor and ChatGPT are not used here. Every bug a reviewer finds goes back to Kiro as a prompt: `A reviewer found: … Fix it and add a test.`

## The owner
Rajdeep (GitHub `Rajdeep-Mridha`), Kolkata, Windows PC. B.Com graduate; this is his first Kiro project. Simple words, one step at a time, explain how to check each change.

## Scope
Camera-based adaptive traffic signals with safe ambulance priority for crowded Indian cities; **Kolkata is the first case**. Everything shown is simulated and must be labelled so.

## Rules
1. This repo is **public**. No secrets, no personal data, nothing from the private research repo (outreach, RTIs, plans, contacts).
2. Safety rules in `.kiro/steering/safety.md` are never weakened, and their tests are never deleted.
3. Facts in the app or docs come only from `docs/RESEARCH-FACTS.md`, with their labels. Never invent numbers.
4. `main` must always build: it is the live site. Work on `kiro`; Rajdeep merges.
5. Commit as `Rajdeep-Mridha` / `353650603+Rajdeep-Mridha@users.noreply.github.com`. Merge on the computer, not GitHub's website button.
6. Ask Rajdeep before pushing, changing hosting, or changing repo settings.
7. Update `docs/STATE.md` at the end of each work session.
