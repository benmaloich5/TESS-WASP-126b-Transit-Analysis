# TESS Transit Analysis of WASP-126 b

Analysis of the transiting exoplanet WASP-126 b (TIC 25155310 b) using
TESS photometric data.

## Overview

This project demonstrates a basic workflow for analyzing an exoplanet
transit using publicly available TESS data. The light curve was obtained
from the TESS SPOC pipeline and analyzed to determine the orbital period
and transit parameters.

The analysis includes:

- TESS light-curve extraction and preprocessing
- Orbital period determination using a Box Least Squares (BLS) periodogram
- Phase-folding of the light curve
- Transit modeling with BATMAN (Kreidberg 2015)
- Initial parameter estimation using a least-squares fit
- Markov Chain Monte Carlo (MCMC) parameter estimation using `emcee` (Foreman-Mackey et al. 2013)
- Posterior distributions and parameter uncertainties
- Conversion of fitted parameters into physical quantities

## Results

The BLS period search gives an orbital period of approximately

$$
P = 3.289\ \mathrm{days}.
$$

The MCMC analysis gives:

| Parameter | Result |
|---|---:|
| $R_p/R_\star$ | $(7.73\pm 0.01)\times10^{-2}$ |
| $a/R_\star$ | $7.73\pm 0.08$ |
| $i$ | $88.05^{+0.31}_{-0.27}\$ deg |

Using a stellar radius of approximately $1.27\ R_\odot$, the estimated
planet radius is approximately

$$
R_p \approx 0.98\ R_J,
$$

and the estimated semi-major axis is approximately

$$
a \approx 0.036\ \mathrm{AU}.
$$

The resulting parameters are consistent with the known properties of
WASP-126 b, a hot-Jupiter-type exoplanet.

## Methods

### Data

TESS light curves were obtained using the `Lightkurve` package. Only
120-second cadence observations from the SPOC pipeline were used, and
the available sectors were stitched together into a single light curve.

### Period Determination

A Box Least Squares periodogram was used to search for periodic transit
signals. The strongest signal corresponds to an orbital period of
approximately 3.289 days.

### Transit Modeling

The phase-folded light curve was modeled using `BATMAN`, assuming a
circular orbit and quadratic limb darkening.

The fitted parameters were:

- Transit phase offset ($\phi_0$)
- Planet-to-star radius ratio ($R_p/R_\star$)
- Scaled semi-major axis ($a/R_\star$)
- Orbital inclination ($i$)

An initial least-squares fit was used to obtain starting values for the
MCMC analysis.

### MCMC

Posterior distributions were sampled using the `emcee` package with
32 walkers and 20,000 steps. The first 2,000 steps were discarded as
burn-in.

The posterior medians and 16th/84th percentiles were used as the final
parameter estimates and uncertainties.

## References

The analysis makes use of the following software and resources:

- Kreidberg, L. (2015), *batman: BAsic Transit Model cAlculatioN in Python*,
  Publications of the Astronomical Society of the Pacific, 127, 1161.
  https://doi.org/10.1086/683602

- Foreman-Mackey, D., Hogg, D. W., Lang, D., & Goodman, J. (2013),
  *emcee: The MCMC Hammer*, Publications of the Astronomical Society of the Pacific,
  125, 306.
  https://doi.org/10.1086/670067

- Lightkurve Collaboration et al. (2018),
  *Lightkurve: Kepler and TESS time series analysis in Python*, Astrophysics Source Code Library, record ascl:1812.013.
  https://ui.adsabs.harvard.edu/abs/2018ascl.soft12013L
  
## Puropse

This project was developed as a small portfolio project to practice
exoplanet transit analysis and Bayesian parameter estimation using
real observational data.

## Repository Contents

```text
.
├── WASP126b_TESS_Transit_Analysis.ipynb
└── README.md
