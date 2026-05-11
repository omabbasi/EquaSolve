# EquaSolve

**A single-file, browser-based engineering equation solver.**

EquaSolve is a self-contained HTML/JavaScript application that solves systems of nonlinear algebraic equations, ordinary differential equations (ODEs), parametric sweeps, optimization problems, regression fits, and sensitivity / uncertainty analyses — all from a single HTML file that runs in any modern web browser. No installation, no compilation, no internet connection at runtime.

Built-in libraries provide thermophysical properties for 38 working fluids (water/steam, air, common gases, hydrocarbons, alcohols, and HFC/HFO/natural refrigerants), heat-transfer and pipe-flow correlations, psychrometric routines, exergy and second-law analysis, and interactive *P–h*, *T–s*, *P–v*, psychrometric, and Moody charts.

---

## Try it now

**Option 1 — Live demo (recommended for first-time users):**
Open **https://omabbasi.github.io/EquaSolve/** in your browser.

**Option 2 — Download and run locally:**
1. Download `EquaSolve_V1_3_35.html` from this repository.
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

---

## Quick example

```
// Refrigeration cycle COP with R134a
T_evap = -10 [C]
T_cond = 40 [C]
m_dot = 0.05 [kg/s]

// State 1: saturated vapor leaving evaporator
h_1 = h_R134a(T = T_evap, x = 1)
s_1 = s_R134a(T = T_evap, x = 1)
P_1 = P_sat_R134a(T = T_evap)

// State 2: isentropic compression
P_2 = P_sat_R134a(T = T_cond)
h_2 = h_R134a(P = P_2, s = s_1)

// State 3: saturated liquid leaving condenser
h_3 = h_R134a(T = T_cond, x = 0)

// Performance
Q_dot_evap = m_dot * (h_1 - h_3)
W_dot_comp = m_dot * (h_2 - h_1)
COP = Q_dot_evap / W_dot_comp
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
with Embedded Thermophysical Properties, Optimization, and Interactive Visualization.
> *[Journal name, volume, pages]*. https://github.com/omabbasi/EquaSolve

A `CITATION.cff` file will be added once the accompanying paper is published.

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
1. The version number (currently V1.3.35)
2. The browser and operating system used
3. A minimal example that reproduces the problem
