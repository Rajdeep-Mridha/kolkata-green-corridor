# Kolkata Green Corridor

**Built with [Kiro](https://kiro.dev) for Kiroween 2026** · category: **Frankenstein**

A live web app showing how **camera-based traffic signals could give every ambulance a safe green**: a simulated Kolkata-style crossroads where you send an ambulance from any of the four roads and watch the signals make way, without ever cutting the amber or all-red that keep other road users safe.

> **Simulated traffic, not field results.** Every traffic input is a labelled assumption.

- **Live app:** _coming with the first build (Cloudflare Pages)_
- **Video (under 3 min):** _added by 3 Dec 2026_

## The problem
In Kolkata, police give organ transports a "green corridor" by holding signals by hand, trip by trip: one 13 km corridor took 13 minutes. An ordinary ambulance gets no signal priority at all. Cities that automated their signals hit a different problem: in Bengaluru in 2025, amber lights were skipped under manual override. The idea is to give every ambulance a green corridor, **safely**: crowded Indian cities first, Kolkata as the first case.

## What you can do in the app
- Watch a four-way junction run on its own: queues, skipped empty roads, never-shortened amber.
- **Send an ambulance** from North, South, East or West and follow each step: request checked → conflicting green finishes → amber → all-red → ambulance green → queue clears → recovery.
- Switch to **rush hour**: see why a 30-second warning fails and a 60-second "pre-flush" works.
- Try **manual mode** and press "force green" during amber: the **Safety Lock** refuses.
- Break a camera or the network and watch the junction step down its fallback ladder.
- Test a **fake ambulance** (siren only): it raises an alert but can't change the lights.

## How Kiro builds it
| Kiro feature | Used for |
|---|---|
| Spec-driven development | Requirements, design and tasks in `.kiro/specs/`, built task by task |
| Steering | Product, safety, tech and workflow rules in `.kiro/steering/` |
| Agent hooks | Tests on save, log reminders, plain-English change summaries |
| Custom agent | A safety reviewer that checks the safety core against the rules |
| Property-based testing | fast-check proves the safety rules hold for thousands of random command sequences |

Every line of app code is written in Kiro on the `kiro` branch; the full story is in [`docs/KIRO-WRITEUP.md`](docs/KIRO-WRITEUP.md) and [`docs/KIRO-LOG.md`](docs/KIRO-LOG.md).

## Run it yourself
_(Kiro fills this in with the first build: `npm install`, `npm run dev`, `npm test`.)_

## Honest disclosure
- **Builder: Kiro.** Specs, code, tests and fixes are made in Kiro during the Kiroween submission period (from 25 Nov 2026).
- **Side help: Claude.** The background research behind the facts in [`docs/RESEARCH-FACTS.md`](docs/RESEARCH-FACTS.md) and the first drafts of the planning notes and steering were prepared with Claude from Rajdeep's own research; Gemini was used to re-check facts. Claude also reviews commits and reports bugs; every fix is made in Kiro. No other AI writes app code.
- Nothing in this project existed before 30 Oct 2026.

## Licence
MIT. See [LICENSE](LICENSE).
