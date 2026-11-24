# Demo brief: Kolkata Green Corridor (for Kiro spec mode)

_Condensed by Claude on 25 Nov 2026 from Rajdeep's research (kept in a separate private repo). Kiro turns this into `.kiro/specs/green-corridor-demo/` (requirements, design, tasks). If anything here conflicts with `.kiro/steering/safety.md`, safety.md wins._

## 1. Purpose
**Scope:** camera-based adaptive traffic signals with safe ambulance priority for crowded Indian cities; Kolkata is the first case.

A **live browser app**: one simulated Kolkata-style four-way junction where anyone can send an ambulance from any road and watch the signals give it a **safe, transparent, logged** green, in automatic, supervised and manual modes, with a fallback ladder. One-line story: *"Police give organ transports a green corridor by hand. This gives one to every ambulance, safely."*

## 2. Users
- **Kiroween judges:** open the link on a laptop or phone, understand it in 30 seconds, play with it for 2 minutes.
- **Traffic engineers and professors (later):** check the safety logic and the tests.
- **Rajdeep:** shows it in emails, posts and meetings.

## 3. Features

### Must have (by 3 Dec)
1. **Junction:** four roads (N, S, E, W), two lanes each, stop lines, four zebra crossings, about 20 m across. Phase plan and a conflict table (which movements may be green together).
2. **Traffic micro-simulation:** cars, two-wheelers, autos and buses arrive at random (seeded), queue at red, discharge at about 1,300 PCU/h/lane (FACT range 1,200–1,400, Maitra et al. 2015); off-peak and peak demand. All shares and rates are ASSUMPTIONS in `src/config.ts`.
3. **Safety core** (`src/core/`): owns the lamps; fixed amber (3.0–3.3 s) and all-red (2.4–3.0 s) per road from config; minimum green 10 s (pre-emption minimum 5 s); pedestrian clearance; conflict table; rejects unsafe requests and logs `SAFETY_LOCK`.
4. **Controllers:** fixed-time (today's baseline, 60–90 s cycle) and actuated (skip a road with no demand; gap-out only after minimum green, gap 3 s; never skip the same road twice in a row; failed camera = demand present; pedestrian recall every second cycle).
5. **Detection (simulated):** camera counts and queues with a failure switch; **authenticated GPS/dispatch request** (vehicle ID, ETA, direction, expiry); siren detector (100–200 m, random false triggers from horns). Fusion: only the GPS request can trigger alone; camera AND siren → operator alert.
6. **Ambulance pre-emption sequence** (section 4), including recovery and the two-ambulance rule.
7. **Two-regime trigger:** off-peak at ETA 30 s; peak "pre-flush" at 60 s (configurable 45–90 s) when the queue is over 40 m.
8. **Modes:** A automatic; B supervised (operator approves plan changes within 30 s, no approval = no change; ambulances stay automatic); C manual (advance or hold only; can never remove amber or all-red; officer ID and reason logged).
9. **Dashboard:** animated top-down junction; lamps; queue bars; ambulance with ETA; a step-by-step countdown panel; buttons "Send ambulance from N/S/E/W", peak on/off, mode switch, failure buttons; the Safety Lock badge; the bilingual sign "AMBULANCE APPROACHING, CLEAR LANE / অ্যাম্বুলেন্স আসছে, রাস্তা ছাড়ুন"; a permanent "Simulated traffic, not field results" label. Works on phone and laptop.
10. **Deploy:** static build on Cloudflare Pages from `main`.

### Should have (in this order, if credits and days allow)
11. Fallback ladder levels 1–6 with failure injection (link loss, camera loss, most cameras lost, conflict detected, power loss).
12. Results tab: fixed-time vs actuated vs actuated + ambulance priority over seeded runs (average delay, ambulance time, cross-street delay), labelled "simulated".
13. Light Halloween night skin ("an ambulance racing through haunted gridlock"): fog, glowing lamps. Never hides the safety message.
14. Fake-ambulance test (siren only → alert, no change).
15. Optional sound: siren, and a spoken bilingual warning (browser speech).

### Out of scope
Real camera video, real siren audio analysis, multiple junctions, real maps, field calibration, any server. The app says so.

## 4. The pre-emption timeline (off-peak, ETA 30 s trigger)
| Step | Rule |
|---|---|
| T −30 s | Authenticated GPS request arrives. Check ID, direction, expiry, mode, lockout. |
| Ambulance road already green | **Extend it** (priority). Skip the steps below. |
| Otherwise | The conflicting green runs to a **pre-emption minimum of 5 s** (at once if it already ran 5 s). A running walk signal ends; people already crossing get about 6 s flashing don't-walk. |
| Then | **Amber 3.0–3.3 s** (never shortened) → **all-red 2.4–3.0 s** (never shortened). |
| About T −18 s | Ambulance road turns green; the queue in front clears. |
| T 0 | The ambulance crosses; release when it is more than 20 m past the stop line. |
| Cap | **Pre-emptive maximum 60–90 s** → forced exit + operator alarm (stuck or false request). |
| Release | Amber → all-red → **exit phase** to the most-starved road with at least the normal 10 s minimum green. |
| Recovery | Shortway back to the plan over 2–3 cycles. Lockout: no non-emergency priority during recovery; a second real ambulance is still served. |
| Two ambulances on conflicting roads | First come, first served by ETA; the second waits for the full amber + all-red; operator alerted. |

Sources: MUTCD 4D.27 ("shall not be shortened or omitted" during pre-emption), ITE/FHWA formula: FACT. The values are RECOMMENDATIONS for a traffic engineer to confirm.

**Why two regimes (ESTIMATE):** the queue's start-up wave moves back at about 2.35 m/s, so a 30 s warning clears only about 30–40 m of queue; 100 m needs about 62–67 s and 250 m about 141–146 s.

## 5. Tasks (paste into spec mode; Kiro may refine)
| Task | What | Done when |
|---|---|---|
| T1 | Skeleton: Vite + TypeScript (strict), Vitest, fast-check, folders from `tech.md`, `src/config.ts`, `npm test` and `npm run build` scripts | Page opens locally; one test passes; build passes |
| T2 | Junction model and conflict table; static drawing | Junction drawn; conflict table tested |
| T3 | **Safety core** + unit tests + **property tests** | fast-check proves: amber/all-red never shortened; no conflicting greens; no data = demand |
| T4 | Traffic micro-simulation (seeded) | Queues grow and clear sensibly; same seed = same run |
| T5 | Fixed-time and actuated controllers | Tests for every rule |
| T6 | Detection: camera, GPS request, siren; fusion | Tests: only GPS triggers alone |
| T7 | Pre-emption sequence, recovery, two-ambulance rule | Tests check every step's timing |
| T8 | Two-regime trigger | Peak run shows 30 s failing and 60 s working |
| T9 | Modes A/B/C (and the fallback ladder if time) | Each mode tested; manual can't cut amber |
| T10 | Dashboard UI and controls | Works on phone and laptop |
| T11 | Results tab, Halloween skin, polish | Looks finished |
| T12 | README "run it yourself", Kiro write-up from the log | A stranger can run it from the README |
| T13 | Video (Rajdeep) | Public YouTube link, under 3 minutes |

## 6. Schedule (IST)
| Date | Work |
|---|---|
| Wed 25 Nov | Install Node.js LTS. Open `D:\dev\kolkata-green-corridor\app` in Kiro on branch `kiro` |
| Thu 26 Nov | Kiro reads the repo, rewrites steering in its own words, writes the spec, adds hooks and the safety-reviewer agent; T1–T2; first deploy |
| Fri 27 Nov | **T3 safety core + property tests** (whole day) |
| Sat 28 Nov | T4, T5 |
| Sun 29 Nov | T6, T7 |
| Mon 30 Nov | T8, T9; credit check; downgrade the Kiro plan before 1 Dec |
| Tue 1 Dec | T10 dashboard |
| Wed 2 Dec | T11 polish; video script and practice take |
| Thu 3 Dec | T12; T13 video; **submit**; blog and social posts |
| Fri 4 Dec | Buffer; last day to redeem the credit code |

**Credit rule:** write the meter reading in `docs/KIRO-LOG.md` after every task. If more than 40% of the credits you have are gone before T7 is done, drop the "should have" items.

## 7. The 3-minute video (keep under 2:55)
| Time | Show | Say |
|---|---|---|
| 0:00–0:20 | The problem, then the app | "Police give organ transports a green corridor by hand. Ordinary ambulances wait at red." |
| 0:20–0:50 | Normal traffic: an empty road skipped; amber never cut | "The signal stops wasting green on empty roads, but never cuts amber." |
| 0:50–1:40 | Send an ambulance: each step on the countdown panel; recovery | "Every step is fixed, tested and logged." |
| 1:40–2:10 | Rush hour: 30 s fails, 60 s pre-flush works | "At rush hour the queue needs a minute to clear." |
| 2:10–2:35 | Manual "force green" during amber → Safety Lock refuses; camera failure | "Manual control can choose the phase, never remove safety time." |
| 2:35–2:55 | Kiro spec, hooks, property tests, the safety-reviewer agent; the live link | "Built with Kiro. Simulated traffic; real field data next." |

## 8. Submission checklist
Live URL · public repo · MIT licence visible in the About section · `/.kiro` at the root (specs, steering, hooks) · description + Kiro write-up · video under 3 min, public on YouTube, no copyrighted music · category Frankenstein · disclosure of Claude's side role.
