# Kiro plan: how this project uses Kiro, fully

_Kiro is the builder of this project. This page lists every Kiro feature we use, why, and the proof the judges will see. Kiroween rules (re-read 25 Nov 2026): "Insufficient use of Kiro will result in disqualification", and "Technological Implementation" (20% of the score) asks how thoroughly and skilfully Kiro was used, whether a variety of Kiro tools was used, and whether there was experimentation._

## 1. What the judges score (each 20%)
| Criterion | What they ask | How this project answers |
|---|---|---|
| Potential impact | A real problem for a real audience | Kolkata ambulances wait at red lights; police make green corridors by hand, trip by trip |
| Technological implementation | Depth and variety of Kiro use | Every feature in section 2, logged |
| Design | A complete, polished product, not a proof of concept | A finished dashboard: phone and laptop, clear story, bilingual sign |
| Innovation | New idea or unusual combination | Traffic simulator + safety lock + simulated camera/siren/GPS + web dashboard, for Kolkata |
| Presentation | Video shows it working end to end; clear pitch | The 3-minute video plan (DEMO-BRIEF §7) |

Judges may score from the video and text alone, so the video and README must stand on their own.

## 2. Kiro features and the proof each leaves
| Kiro feature | How we use it | Proof |
|---|---|---|
| **Spec-driven development** | One spec `green-corridor-demo`: requirements (EARS) → design → tasks T1–T13 | `.kiro/specs/green-corridor-demo/`, ticked tasks, commits `T1: …` |
| **Steering** | `product.md`, `safety.md`, `tech.md`, `workflow.md`. Kiro refreshes them in its own words at the start (Step 2b of the guide) | `.kiro/steering/`; one moment where `safety.md` stops an unsafe change |
| **Agent hooks** (at least 3) | (1) On save in `src/core/` or `src/controllers/`: run `npm test`, failures first. (2) On a finished spec task: add a KIRO-LOG line. (3) Manual "Explain last change" in plain English | `.kiro/hooks/`; a screenshot of a hook catching a failing test |
| **Property-based testing** | fast-check tests generate thousands of random command sequences and prove the safety rules hold: amber and all-red never shortened, never two conflicting greens, "no data" always counts as demand | `tests/core/safety.properties.test.ts`; one bug PBT found that unit tests missed |
| **Custom agent** | A "safety reviewer" agent that only reads `src/core/` changes against `safety.md` and reports problems | Its config in `.kiro/`; one review it caught |
| **Agent chat (vibe coding)** | Small fixes, UI polish, error explanations | Prompts in `docs/KIRO-LOG.md`; a spec-vs-vibe comparison in the write-up |
| **Kiro CLI** | Try it once, e.g. to run the scenario runner or a review | One paragraph in the write-up: IDE vs CLI |
| **MCP or Kiro powers** (only if useful and free) | E.g. a documentation server, or a power with TypeScript/testing best practice | Mention only if really used |
| **Model choice** | Cheaper model for small edits; stronger model for the safety core and pre-emption | Credit numbers in KIRO-LOG |

## 3. Rules that keep it "built with Kiro"
- Every line of app code is written by Kiro. Claude and Gemini only report bugs or check facts; the fix is a Kiro prompt.
- One task per prompt. Commit after each finished task on branch `kiro`.
- After each task, log: date, task, short prompt, credits before → after, result (`docs/KIRO-LOG.md`).
- Take 1–2 screenshots a day of Kiro doing something visible. Save them in `docs/kiro-screens/` (nothing personal on screen).

## 4. Credits
- Now: about 1,110 (plan + trial; the plan ends 1 Dec). Coming: 4,000 Kiroween credits (redeem by 4 Dec while logged in with GitHub; only for this entry; expire 31 Dec).
- Budget (ESTIMATE): spec + steering ~300 · tasks ~2,000 · fixes ~1,000 · reserve ~700.
- If more than 40% is used before T7, drop the "should have" items in DEMO-BRIEF §3.

## 5. Bonus prizes worth entering
| Bonus | Rule (official) | Plan |
|---|---|---|
| Blog post | Public post on a third-party blog about Kiro and the build, saying it was written for Kiroween 2026; top 100 get 2,000 credits | Substack, published 3–4 Dec, in Rajdeep's own words |
| Social Blitz | Post must **start** with `#KiroweenHackathon26`, say your favourite thing about Kiro and how it changed your approach; judged on original thoughts, not AI writing | X @Rajdeep__Mridha and LinkedIn, his own words |
| Best Demo | Highest presentation score within the top 10% | The video |
| Not eligible | Student prize (not enrolled), Startup prize, Ghost of Kiroween Past | — |
