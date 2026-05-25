# Active modulation of zonal flows in modified Hasegawa–Wakatani turbulence

Reproduction code for the report *"Active modulation of zonal flows in modified
Hasegawa–Wakatani turbulence: a preliminary numerical verification study."*

This repository contains everything needed to regenerate all five figures and the
statistical tables in the report from scratch. The physics is a well-established
testbed (2D modified Hasegawa–Wakatani turbulence with an external zonal drive); the
point of the study is the verification workflow — parameter sweeps, an operational
window, and ensemble statistics — on a system simple enough to run and understand fully.

## What it does

A pseudo-spectral solver integrates the 2D modified Hasegawa–Wakatani equations on a
periodic box and adds an idealized external drive at the zonal scale,
`F_AC = F0 · cos(omega_AC · t) · cos(k_zf · x)`. The notebook then:

1. shows baseline (unforced) and forced field snapshots (Figures 1 & 2),
2. sweeps the drive amplitude `F0` and contrasts the time-averaged diagnostic with a
   single-snapshot one (Figures 3 & 4),
3. maps the operational window over the `(F0, omega_AC)` plane (Figure 5), and
4. establishes statistical significance with five-seed ensembles (the tables).

## How to run

**Google Colab (easiest):** upload `mhw_reproduce.ipynb`, then `Runtime → Run all`.
NumPy and Matplotlib are preinstalled.

**Locally:**

```bash
pip install -r requirements.txt
jupyter notebook mhw_reproduce.ipynb     # then Run All
```

Run the cells top to bottom. Cell 1 defines the solver and `run_sim(...)` once; every
later cell only calls it. Each figure cell saves a `Figure_N.png` next to the notebook.

Expected runtime: a few minutes on a typical laptop or Colab CPU. The 2D map (Cell 4)
is the slowest, since it runs the solver 48 times.

## Key result

With the drive at its optimum, `(omega_AC, F0) ≈ (0.06, 0.02)`, the time-averaged
turbulent energy falls to roughly a quarter of the unforced baseline (about a 76%
reduction). The suppression is statistically significant across five random seeds, and
the optimum sits inside a narrow operational window: too strong or too slow a drive
diverges, too fast a drive has almost no effect.

## Reproducibility notes

- All random seeds are fixed, so the printed numbers are identical run to run.
- The "divergence" cutoff used to mask the hatched region in Figure 5 (turbulent energy
  above three times the unforced baseline) is a **diagnostic threshold chosen for the
  plot, not a sharp physical boundary**.
- The optimum is resolved only to the grid spacing (Δω = 0.01) and is reported at fixed
  `F0`; a fully joint optimization over both parameters is left as future work.
- Results are at a single resolution (64×64) and box size (L = 20π); no exhaustive
  convergence study was performed.

## Files

| File | Purpose |
|------|---------|
| `mhw_reproduce.ipynb` | the notebook — produces all 5 figures and the tables |
| `requirements.txt`    | Python dependencies |
| `README.md`           | this file |

## AI assistance

The code was written with the help of an AI coding assistant (Anthropic's Claude). All
design decisions, simulations, verification choices, and interpretation of the results
are the author's own; every simulation was run and checked by the author.

## Author

Minhyuk Kim, Department of Physics and Astronomy, Sejong University, Seoul, Republic of Korea.
