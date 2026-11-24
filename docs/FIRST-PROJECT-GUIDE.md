# Your first Kiro project: step by step

_For Rajdeep. Plain steps, in order. Each prompt in a box is ready to paste into Kiro's chat._

## Words you'll meet
- **Repo**: the project folder plus its history (git).
- **Branch**: a separate line of work. `main` = finished; `kiro` = Kiro builds here.
- **Commit**: a saved checkpoint with a message.
- **Push**: send commits to GitHub.
- **Spec**: Kiro's plan in three files: requirements (what), design (how), tasks (steps).
- **Steering**: rule files Kiro reads on every prompt (`.kiro/steering/`).
- **Hook**: an automatic action, e.g. "run the tests when I save a file".
- **Vibe vs Spec**: Vibe = free chat; Spec = planned build. Use **Spec** for this project.

## Step 0. Install the tools (one time, about 30 minutes)
1. **Git** is already installed. Nothing else to do here.
2. **Node.js LTS** from nodejs.org (Windows installer, default options). Check in a new terminal: `node --version` and `npm --version`. (Python and SUMO are not needed for this app.)
3. Restart Kiro after installing.

## Step 1. Open the project in Kiro
Kiro → File → Open Folder → **`D:\dev\kolkata-green-corridor\app`** (the `app` folder, not its parent). Check that the switcher at the bottom left shows the branch **`kiro`**.

The parent folder `D:\dev\kolkata-green-corridor` holds two separate projects:
- `app\` → the **public** repo `kolkata-green-corridor` (this one; Kiro works here; it goes live).
- `research\` → the **private** repo `kolkata-green-corridor-research` (your research; never public; Kiro never opens it).

## Step 2. First prompt: let Kiro read and confirm
```
Read AGENTS.md, every file in .kiro/steering, and docs/DEMO-BRIEF.md.
Then tell me in 5-8 plain sentences what this project is, what the safety rules are,
and what you will build first. Do not write any code yet.
```
If its summary misses the safety core or the two-regime trigger, correct it before going on.

## Step 2b. Let Kiro make the steering its own
```
Read the four files in .kiro/steering. Rewrite each in your own words so it guides you best,
keeping every rule in safety.md exactly. Show me the changes before saving.
```
This makes the steering Kiro-made work, which judges look for.

## Step 3. Make the spec
Switch the chat to **Spec** mode, then:
```
Create a spec called green-corridor-demo from docs/DEMO-BRIEF.md.
Requirements: use EARS style, one requirement per feature in section 3 "Must have".
Design: follow the folder layout in .kiro/steering/tech.md; the safety core must not import the simulation or the UI.
Tasks: follow T1-T13 in section 5, each with a clear "Done when" test.
Stop after each of the three files so I can review it.
```
Read each file. You can say "change X" as many times as you need. Commit when you're happy: message `Spec: requirements, design, tasks`.

## Step 4. Hooks, a custom agent and property tests (the Kiro features judges look for)
Paste these one at a time:
```
Create 3 Kiro hooks: (1) when any file in src/core/ or src/controllers/ is saved, run npm test
and show failures first; (2) when a spec task is marked done, remind me to add a line to
docs/KIRO-LOG.md; (3) a manual hook "Explain last change" that explains the last commit in plain English.
```
```
Create a custom agent called safety-reviewer. It only reads changes in src/core/ and checks them
against .kiro/steering/safety.md, then lists any rule that could be broken. It never edits code.
```
When you reach task T4 (safety core), also ask:
```
Add property-based tests with fast-check that generate random command sequences and prove:
amber and all-red are never shortened, two conflicting greens never show, and no data means demand.
```
Try the Kiro CLI once (for example to run the tests) so the write-up can compare IDE and CLI.

## Step 5. Build, one task at a time
In `tasks.md`, click **Start task** next to T1 (or type "Do task T1 only"). After each task:
1. Read Kiro's "What changed / How to check".
2. Do the check yourself (run the command it gives).
3. Look at Kiro's credit meter, write the number in `docs/KIRO-LOG.md`.
4. Commit: `T1: project skeleton`.
5. (Optional) Ask Claude: "Review the last commit on branch kiro in D:\dev\kolkata-green-corridor\app for bugs. Do not edit code." Paste their findings back to Kiro as: `A reviewer found: ... Fix it and add a test.`

## Step 6. When things go wrong
- Error message → copy the whole message into Kiro: `This error appeared when I ran ...: <paste>. Explain it simply, then fix it.`
- Kiro is going in circles (2 failed attempts) → stop. Ask Claude to diagnose; give Kiro the diagnosis.
- Never accept a fix that deletes or weakens a safety test.

## Step 7. Merge and push (always your decision)
When a task works, commit on `kiro`. Merging `kiro` into `main` and pushing is always your decision: nothing goes to GitHub without your yes.

## Step 7b. Put the app online (once, after T1 works)
1. Merge `kiro` into `main` and push (ask Claude to help the first time).
2. Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git → choose `kolkata-green-corridor`. Approving GitHub access is your click.
3. Settings: production branch `main`; framework preset **Vite**; build command `npm run build`; output folder `dist`.
4. Deploy. You get a free address like `kolkata-green-corridor.pages.dev`. From now on every push to `main` updates the live site in about a minute, and every push to `kiro` gets its own preview link.
5. Put the live address in the README and in the repo's About section.

## Step 8. Submission week (2–3 Dec)
The app is already live from Step 7b. Finish the README and "how I used Kiro" from KIRO-LOG → record the video (free screen recorder, captions, no music) → submit on Devpost **by 3 Dec evening IST**. The repo is already public.
