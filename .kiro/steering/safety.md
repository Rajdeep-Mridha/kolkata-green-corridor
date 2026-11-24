---
inclusion: always
---
# Safety rules (never break these)

1. **Amber and all-red are fixed per approach** and come only from config at start-up. No code path may shorten or skip them: not in automatic, supervised or manual mode, not during pre-emption, not during recovery.
2. **The safety core owns the lamps.** Controllers, detectors, the dashboard and the operator can only send *requests*. The core accepts or rejects them and logs every rejection as `SAFETY_LOCK`.
3. The safety core (`src/core/`) must **not import the simulation, the UI or any AI/ML code**. Plain TypeScript only, so it can be tested alone.
4. A conflict table defines which movements may be green together. Conflicting greens are impossible; minimum green and pedestrian clearance are always served.
5. **"No data" from a detector means "demand present"**, never "empty".
6. Only an **authenticated GPS/dispatch request** (vehicle ID + expiry) can trigger pre-emption on its own. Camera alone or siren alone can only raise an operator alert. Camera AND siren together → alert. Every request expires.
7. The simulated ambulance **does not run red lights**. Any benefit must come from the signal design.
8. Two ambulances in conflict: first come, first served; the second waits and is logged.
9. Every rule above has a test, and rules 1, 4 and 5 also have fast-check property tests. **A change that breaks a safety test is never accepted.** Fix the code, never weaken the test.
