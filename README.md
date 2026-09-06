# EquaSolve

**A single-file, browser-based engineering equation solver.**

[![Paper DOI](https://img.shields.io/badge/paper-10.5541%2Fijot.1978096-blue)](https://doi.org/10.5541/ijot.1978096)
[![Software DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22278667.svg)](https://doi.org/10.5281/zenodo.22278667)
[![License](https://img.shields.io/badge/License-Apache%202.0-green)](LICENSE)
[![Live demo](https://img.shields.io/badge/demo-omabbasi.github.io%2FEquaSolve-orange)](https://omabbasi.github.io/EquaSolve/)

Accepted in the *International Journal of Thermodynamics* — [doi:10.5541/ijot.1978096](https://doi.org/10.5541/ijot.1978096).
The issue appears in **December 2026**; the DOI begins resolving once it is published.

EquaSolve is a self-contained HTML/JavaScript application that solves systems of nonlinear algebraic equations, ordinary differential equations (ODEs), parametric sweeps, optimization problems, regression fits, and sensitivity / uncertainty analyses — all from a single HTML file that runs in any modern web browser. No installation, no compilation, no internet connection at runtime.

Built-in libraries provide thermophysical properties for 38 working fluids (water/steam, air, common gases, hydrocarbons, alcohols, and HFC/HFO/natural refrigerants), heat-transfer and pipe-flow correlations, psychrometric routines, exergy and second-law analysis, and interactive *P–h*, *T–s*, *P–v*, psychrometric, and Moody charts.

---

## Try it now

**Option 1 — Live demo (recommended for first-time users):**
Open **https://omabbasi.github.io/EquaSolve/** in your browser.

**Option 2 — Download and run locally:**
1. Download the highest-numbered `EquaSolve_V1_3_*.html` in this repository — currently **`EquaSolve_V1_3_103.html`**. This is the same build the live demo serves.
2. Double-click the file. It will open in your default browser.
3. That's it. No setup required.

The application works fully offline once loaded. The same file runs on Windows, macOS, Linux, Android, and iOS, on any browser released in the last five years.

---

## Features

### Problem types
- **Algebraic equations** — nonlinear systems solved by sequential substitution or Newton–Raphson with LU factorization and line search
- **ODEs / DAEs** — RK4 (fixed-step), RK45 (adaptive Dormand–Prince), and SDIRK (stiff-stable implicit)
- **Optimization** — Nelder–Mead with penalty constraints; Differential Evolution for global search
- **Regression** — Levenberg–Marquardt with confidence intervals, *R²*, RMSE
- **Sensitivity analysis** — derivative-based and finite-difference matrices
- **Uncertainty propagation** — GUM (ISO/IEC Guide to the Expression of Uncertainty in Measurement) framework
- **Parametric sweeps** — 1D and 2D, with automatic plotting
- **Pareto front analysis** — multi-objective constrained optimization

### Domain libraries
- **38 working fluids**, including:
  - Water / steam
  - Air, nitrogen, oxygen, hydrogen, helium, argon, CO₂
  - Hydrocarbons: methane, ethane, propane, butane, pentane, isopentane, hexane
  - Alcohols: methanol, ethanol
  - HFC refrigerants: R134a, R32, R22, R410A, R404A, R407C, R507A, R152a, R125, R143a, R245fa, R448A, R454B, R123
  - HFO refrigerants: R1234yf, R1234ze
  - Natural refrigerants: R717 (ammonia), R744 (CO₂), R290 (propane), R600a (isobutane), R1270 (propylene)
- **Heat-transfer correlations**: Dittus–Boelter, Gnielinski, NTU-effectiveness, LMTD
- **Pipe-flow analysis**: Moody friction factor, Colebrook–White, laminar/turbulent regime detection
- **Psychrometrics**: ω, φ, *h*, *T*<sub>wb</sub>, *T*<sub>dp</sub>, with 1-atm and elevation support
- **Exergy analysis**: flow and non-flow exergy, irreversibility, second-law efficiency

### User interface
- Unified problem specification language with bracketed unit syntax `[unit]`
- MATLAB-style `...` line continuation
- Automatic problem classification
- Syntax highlighting with error-line detection
- Interactive *P–h*, *T–s*, *P–v* thermodynamic diagrams
- Psychrometric and Moody charts
- Multi-sheet workspace with print-ready report export
- Automatic curve-intersection finder for parametric sweeps — tick **✛ Intersections** to mark where any plotted curves cross, with coordinates listed under the plot

---

## Quick example

```
// Refrigeration cycle (vapor-compression) with R-134a
T_evap = -10 [degC]
T_cond = 40  [degC]

P_low  = Psat_R134a(T_evap)
P_high = Psat_R134a(T_cond)

// State 1: saturated vapour leaving evaporator
h1 = hg_R134a(T_evap)
s1 = sg_R134a(T_evap)

// State 2: isentropic compression
h2 = h_Ps_R134a(P_high, s1)
T2 = T_Ph_R134a(P_high, h2)

// State 3: saturated liquid leaving condenser
h3 = hf_R134a(T_cond)

// State 4: isenthalpic throttle
h4 = h3

// Performance
COP = (h1 - h4) / (h2 - h1)
```

Paste into the Equations tab and press **Solve**. Results are supported with full unit and can be exported as a multi-sheet report.

Additional worked examples — including a Rankine cycle, an air-standard Brayton cycle, a fin-design optimization, and a psychrometric air-conditioning process — are built into the application and accessible from the **Examples** menu.

---

## System requirements

- Any modern web browser (Chrome, Edge, Firefox, Safari) released in the last five years
- ~5 MB of disk space for the HTML file
- ~100 MB RAM for typical problems
- No internet connection required after the initial download

EquaSolve has been tested on Microsoft Edge, Google Chrome, and Mozilla Firefox on Windows 10/11, macOS, Ubuntu, Android, and iOS.

---

## Citation

If you use EquaSolve in academic work, please cite:

> Al-Abbasi, O. (2026). EquaSolve: A Zero-Installation Browser-Based Engineering Equation Solver
> with Embedded Thermophysical Properties, Optimization, and Interactive Visualization.
> *International Journal of Thermodynamics* (accepted; issue scheduled for December 2026).
> https://doi.org/10.5541/ijot.1978096

Volume, issue, and page numbers are assigned when the issue is published in December 2026
and will be added here then. Until then the DOI is the stable identifier — note that it
does not resolve until the publisher registers it.

BibTeX:

```bibtex
@article{AlAbbasi2026EquaSolve,
  author  = {Al-Abbasi, Omar},
  title   = {{EquaSolve}: A Zero-Installation Browser-Based Engineering Equation
             Solver with Embedded Thermophysical Properties, Optimization,
             and Interactive Visualization},
  journal = {International Journal of Thermodynamics},
  year    = {2026},
  note    = {Accepted; issue scheduled for December 2026},
  doi     = {10.5541/ijot.1978096},
  url     = {https://doi.org/10.5541/ijot.1978096}
}
```

A machine-readable [`CITATION.cff`](CITATION.cff) is also provided, so GitHub's
"Cite this repository" button returns this reference.

### Citing the software itself

The reference above cites the *paper*. To cite the *code* — which is what you need when a
result depends on the exact build you ran — use the Zenodo archive:

| | DOI |
|---|---|
| **All versions** (resolves to the latest) | [10.5281/zenodo.22278667](https://doi.org/10.5281/zenodo.22278667) |
| **v1.3.100** specifically | [10.5281/zenodo.22278668](https://doi.org/10.5281/zenodo.22278668) |

Cite the paper for the method, the version DOI for reproducibility. Every release is
archived on Zenodo with the complete `Archive/` history attached.

---

## Version archive

The repository root carries only the current release. Every earlier build is preserved in
`Archive/` — all 68 versions from V1.234 (April 2026) through V1.3.103, under their
original filenames. Each is also a git tag dated from its original release.

```bash
ls Archive/                       # every build ever released
git tag                           # v1.234 ... v1.3.103, in release order

# what changed between two releases
git diff --no-index Archive/EquaSolve_V1_3_102.html Archive/EquaSolve_V1_3_103.html
```

Reproducing a result from an earlier paper means taking that version straight from
`Archive/` — for example `Archive/EquaSolve_V1_3_35.html`.

---

## License

EquaSolve is released under the **Apache License 2.0**. You are free to use, modify, and redistribute it for academic, educational, or commercial purposes, provided that the license notice is preserved. See the [LICENSE](LICENSE) file for the full text.

---

## Author

**Dr. Omar Al-Abbasi**
Associate Professor of Mechanical Engineering
University of Bahrain

GitHub: [@omabbasi](https://github.com/omabbasi)

---

## Acknowledgements

EquaSolve was developed as a free, lightweight alternative to commercial equation-oriented solvers for engineering education and research. The thermophysical property models are based on published Helmholtz-energy equations of state for each fluid; full references are listed in the accompanying paper.

---

## Reporting issues and contributing

Bug reports, feature requests, and pull requests are welcome via the [Issues](https://github.com/omabbasi/EquaSolve/issues) tab. When reporting a numerical issue, please include:
1. The version number (currently V1.3.103)
2. The browser and operating system used
3. A minimal example that reproduces the problem
