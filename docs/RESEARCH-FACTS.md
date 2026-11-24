# Research facts the demo may cite

_Only items checked in Rajdeep's research report (20 Nov 2026). Label every use. Do not add new numbers without a source._

| Statement | Label | Source |
|---|---|---|
| No adaptive/AI signal with automatic ambulance priority found running, piloted or tendered in Kolkata or West Bengal (Nov 2026) | NOT FOUND (wide search) | Research report Part 1 |
| Ambulance signal priority in Kolkata is arranged by hand, per trip ("green corridors") | FACT | News reports cited in report Part 2.7 |
| Independent studies: adaptive control cuts delay about 0–30% | FACT | Report Part 4.1 |
| Emergency pre-emption cuts emergency travel time through signals about 14–23% | FACT | Report Part 4.2 |
| MUTCD 4D.27: during the change to pre-emption, yellow and red clearance "shall not be shortened or omitted" | FACT | mutcd.fhwa.dot.gov, Part 4D |
| Kolkata saturation flow 1,200–1,400 PCU/h/lane (Exide, Hazra, Rashbehari) | FACT | Maitra et al., J. Transport Literature, 2015 |
| A 30 s warning clears only about 30–40 m of queue; 100–250 m needs about 60–145 s | ESTIMATE | Report Part 5.6 (working shown) |
| SUMO has no built-in signal pre-emption; it must be scripted via TraCI | FACT | sumo.dlr.de/docs/Simulation/Emergency.html |
| SIGMA (arXiv 2608.18263) simulates four Kolkata-modelled junctions in SUMO | FACT | arxiv.org/abs/2608.18263 |
| Bengaluru amber-skipping complaints, Sep 2025 | FACT | Report Part 3.4 |

Everything else (vehicle shares, arrival rates, speeds) is an **ASSUMPTION** in `src/config.ts`.

## More checked facts (from the full report, read 25 Nov)
| Statement | Label | Source |
|---|---|---|
| A 13 km organ green corridor in Kolkata took 13 minutes, with police holding signals by hand | FACT | Millennium Post (report 2.7) |
| Kolkata Police ran a short AI queue-length signal trial at Patuli, EM Bypass, in Oct 2024; no result reported since | FACT (outcome UNKNOWN) | Times of India via Bengalinfo (report 2.4) |
| Google Green Light timing advice is applied by hand at about 13 Kolkata junctions; it has no emergency function | CLAIM (Google) | sites.research.google/greenlight (report 2.3) |
| Kolkata spent ₹2.49 crore on red-light cameras at 20 junctions (Jan 2026): enforcement, not signal control | FACT | Millennium Post (report 2.5) |
| Udaipur trialled a siren-triggered AI signal at one junction (late 2025), about ₹10 lakh | FACT; results NOT FOUND | Drishti IAS (report 3.3) |
| Camera + siren fusion: 100% precision but 87.1% recall, so it misses about 1 ambulance in 8; GPS must be the main trigger | FACT (abstract) | Kristiawan et al., ETASR 16(2), 2026 |
| Kolkata was the 2nd slowest city in the world in TomTom 2024 (34 min 33 s per 10 km) | FACT | Business Standard, Jan 2025 |
