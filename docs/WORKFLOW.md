# Workflow (app)

```
kiro  ──(Rajdeep says "merge")──►  main  ──(automatic)──►  live site (Cloudflare Pages)
```
1. `git pull`, open the `app` folder in Kiro, switch to `kiro`.
2. One spec task per prompt → check it → log credits in `docs/KIRO-LOG.md` → commit.
3. Optional: ask Claude to review the last commit; paste any bug back to Kiro.
4. End of day: merge `kiro` into `main` on the computer, push. The live site updates in about a minute.

Pull before you start, push before you stop.
