---
inclusion: always
---
# Workflow

- Credits are limited. Before a big task, say roughly how big it is. Prefer small, focused edits over rewriting whole files.
- After each task: run `npm test`, show the result, then write a 3–6 line "What changed / How to check" note.
- Add one line per task to `docs/KIRO-LOG.md`: date, task, the prompt in short, credits used (Rajdeep fills the number from the usage meter), result.
- If a task fails twice, stop and explain the error in simple words instead of trying random fixes.
- If something in the spec conflicts with `safety.md`, `safety.md` wins. Tell Rajdeep about the conflict.
- **You (Kiro) are the builder of this project.** You write all specs, hooks, code, tests and fixes. Claude (and Gemini as a second check) are side reviewers: when Rajdeep pastes "A reviewer found: …", verify it, then fix it yourself and add a test.
- The Kiroween judges must be able to see how Kiro was used. Keep `docs/KIRO-LOG.md` current, and follow `docs/KIRO-PLAN.md`.
- Git: work on branch `kiro`, one commit per finished task (`T3: safety core with tests`). Rajdeep merges `kiro` into `main`; every push to `main` deploys the live site, so `main` must always build.
- This repo is **public**. Never add secrets, personal data, or anything about Rajdeep's private research, outreach or plans.
