# Finding an Exoplanet in TESS Data

Detecting a planet orbiting the star WASP-18 from NASA TESS space-telescope data, and measuring its orbital period and radius with uncertainty.

**Method:** Box Least Squares period search → phase folding → transit depth → planet radius, with bootstrap + Monte Carlo uncertainty. Results are checked against the NASA Exoplanet Archive.

**Tools:** Python, lightkurve, astropy, NumPy, pandas, matplotlib, Jupyter Lab, uv

---

## Setup (with uv)

```bash
uv init exoplanet-transits
cd exoplanet-transits
uv add lightkurve astropy numpy pandas matplotlib jupyterlab
uv run jupyter lab
```

Open `exoplanet_transits.ipynb` and run all cells. The first run downloads about 20 MB of TESS data.

**Test mode:** set `USE_SIMULATED = True` in the first cell. The notebook then runs on a fake light curve with a planet of known size planted in it, and should recover the planted period and radius almost exactly. Running this first proves the code works before trusting it on real data.

---

## Plan

| Week | Goal | Done when |
|---|---|---|
| 1 | Set up the uv environment and GitHub repo. Run test mode. Read the Physics section below. | Test mode recovers the planted planet. First commit pushed. |
| 2 | Switch to real data (`USE_SIMULATED = False`). Get the download and cleaning steps working. | You see the dips by eye in the cleaned light curve. |
| 3 | Run the BLS search and fold. Compare your period to NASA's. | Folded plot shows one clean dip. Period matches to 4+ decimal places. |
| 4 | Radius and uncertainty. Write the "What I found" section in your own words. | Radius is within ~10% of NASA's value, and you can explain why it's off. |
| 5 | Polish: run 2–3 more TESS sectors, clean up plots, finish this README with your results and one key figure. | A stranger can understand the project from this page alone. |
| Stretch | Fit a real transit model (`batman`) with MCMC (`emcee`) for a Bayesian radius posterior. Or try a smaller, harder planet. | |

**Git habit:** commit at the end of every work session with a message saying what changed. A steady commit history looks good to recruiters.

---

## Physics in one paragraph

A planet crossing its star blocks a fraction of the light equal to the ratio of their disk areas: depth ≈ (R<sub>planet</sub> / R<sub>star</sub>)². So R<sub>planet</sub> = R<sub>star</sub> × √depth. The time between dips is the orbital period. The box-shaped model used here ignores **limb darkening** (the star's edge looks dimmer than its center), which is the main reason a simple estimate can differ slightly from published values.

---

## Results

*(Fill in after Week 4.)*

| | My estimate | NASA Exoplanet Archive |
|---|---|---|
| Period (days) | 0.94136 | 0.94145 |
| Radius (Earth radii) | 14.61 (13.27 to 15.95) | 13.90 |

---

## Resume bullet (fill in your numbers)

> **Exoplanet Transit Detection** | Python, lightkurve, astropy, Jupyter
> – Built a Python pipeline to detect exoplanet transits in NASA TESS light curves using Box Least Squares period search and phase folding.
> – Estimated orbital period and planet radius with bootstrap and Monte Carlo uncertainty propagation, matching NASA Exoplanet Archive values within X%.
> – Validated the pipeline on simulated light curves with injected planets before applying it to real data.
