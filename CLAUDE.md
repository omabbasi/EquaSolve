# EquaSolve — working notes

## What this is

EquaSolve is a general engineering equation solver distributed as **one self-contained
HTML file** — no build step, no dependencies, no server. Open `EquaSolve.html` in a
browser and it runs. Author: Dr. Omar Al-Abbasi, Mechanical Engineering, University of
Bahrain. It is the subject of an academic paper; the most recent submission package targets the
*International Journal of Thermodynamics*.

## How development actually happens

Builds are produced whole, not patched incrementally, and are versioned by filename
(`EquaSolve_V1_3_97.html`). Historically each new build landed in `~/Downloads`, which
is why sixty-odd versions accumulated there. **That is no longer the source of truth —
this repo is.**

**The repository root holds exactly one build: the current release.** Every earlier
version lives in `Archive/` and nowhere else. Do not leave old releases at the root.

When a new build is produced:

1. `git rm` the previous release from the root.
2. Add the new build to the root as `EquaSolve_V1_3_NN.html`.
3. Copy the same file into `Archive/` under that name.
4. Commit with the version as the subject line (e.g. `v1.3.98`), then `git tag v1.3.98`.
5. Bump the version strings in `README.md` and `version:` in `CITATION.cff`.

To compare two builds, diff the archived copies directly — this needs no shared filename
and always works:

```bash
git diff --no-index Archive/EquaSolve_V1_3_89.html Archive/EquaSolve_V1_3_97.html
```

Builds up to v1.3.97 also share a canonical path (`EquaSolve.html`) inside their own
commits, so `git diff v1.3.89 v1.3.97 -- EquaSolve.html` still works for that range. That
file was removed from the root on 3 Sep 2026; releases after v1.3.97 will not have it.

## Conventions that matter

- **Never rewrite line endings.** `.gitattributes` marks HTML/Python as binary-ish on
  purpose. A whole-file CRLF flip would make every diff useless.
- **Version numbers are not semver.** `1.3.97` is a running counter; `1.4` exists and
  sits chronologically *between* `1.3.15` and `1.3.16`. Order by commit date, not by
  parsing the number.
- Sub-revisions use a fourth component (`v1.3.42.3`) — same-day iterations on a build.

## Repo is inside OneDrive

The working tree lives under `D:\OneDrive - University of Bahrain\`. The packed
repository is small (~1 MB for all 62 builds, thanks to delta compression), so sync
is not a practical problem, but avoid long-running git operations while OneDrive is
actively syncing.

## Publishing

`origin` is https://github.com/omabbasi/EquaSolve — **public**. Pushing to `main` is
publishing; treat every push as outward-facing.

GitHub Pages serves the live demo at https://omabbasi.github.io/EquaSolve/. The workflow
`.github/workflows/deploy-latest.yml` runs on any push touching a root-level
`EquaSolve_V*.html`, picks the newest by `sort -V | tail -1`, and deploys it.

Two traps in that mechanism:

- **`sort -V` ranks `v1.4` above `v1.3.97`.** An `EquaSolve_V1_4.html` in the repo root
  would silently become the live demo, serving an April build as "latest". The historical
  `v1.4` build is safe inside `Archive/` only because the glob is root-only — keep it there.
- **Only root-level files are globbed.** Publishing a release means copying it to the root
  as `EquaSolve_V1_3_NN.html`, not just committing it to `Archive/`.

Because the root holds only one release, `sort -V` now has a single candidate — but keep
the rule anyway: exactly one `EquaSolve_V*.html` at the root, everything else in
`Archive/`. See the release steps under "How development actually happens".

There is no committed `index.html`. The workflow generates its own at deploy time
(`cp "$latest" _site/index.html`), so the root does not need one. This holds only while
Pages is served from GitHub Actions; if it is ever switched to "deploy from branch", a
root `index.html` becomes load-bearing again.

## Resolved

`v1.3.35` was once missing from local disk entirely. It was recovered from this GitHub
repository and verified byte-identical (SHA-256) to the copy attached to the EquaSolve
project on claude.ai. It is the version cited by the CAE journal submission and by
`../Figure_1_EquaSolve_V1_3_35.py`.
