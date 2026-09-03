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

When a new build is produced:

1. Save it over `EquaSolve.html`.
2. Commit with the version as the subject line (e.g. `v1.3.98`).
3. Tag it: `git tag v1.3.98`.
4. Drop the originally-named copy into `Archive/`.

Keeping the canonical filename stable is what makes `git diff v1.3.95 v1.3.97` work.
Do not rename `EquaSolve.html` to a versioned name — that breaks every diff.

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

Release checklist: update `EquaSolve.html`, copy it to root as `EquaSolve_V1_3_NN.html`,
refresh `index.html` to match, bump the two version strings in `README.md` and `version:`
in `CITATION.cff`, add the build to `Archive/`, commit, tag.

## Resolved

`v1.3.35` was once missing from local disk entirely. It was recovered from this GitHub
repository and verified byte-identical (SHA-256) to the copy attached to the EquaSolve
project on claude.ai. It is the version cited by the CAE journal submission and by
`../Figure_1_EquaSolve_V1_3_35.py`.
