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

## Physics in one paragraph

A planet crossing its star blocks a fraction of the light equal to the ratio of their disk areas: depth ≈ (R<sub>planet</sub> / R<sub>star</sub>)². So R<sub>planet</sub> = R<sub>star</sub> × √depth. The time between dips is the orbital period. The box-shaped model used here ignores **limb darkening** (the star's edge looks dimmer than its center), which is the main reason a simple estimate can differ slightly from published values.

---

## Results

| | My estimate | NASA Exoplanet Archive |
|---|---|---|
| Period (days) | 0.94136 | 0.94145 |
| Radius (Earth radii) | 14.61 (13.27 to 15.95) | 13.90 |

---
