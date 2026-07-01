# GW_project

This repository contains two related sub-projects exploring gravitational-wave detector data from complementary angles: one focused on characterising noise anomalies in real detector data, the other on modeling how new physics (a dark matter density spike) would imprint itself on a clean inspiral waveform.

## Repository Structure

- **`gw_noise_anomaly/`** - Anomaly characterisation of noise in LIGO detector data using window-function diagnostics.
- **`gw_dm_spike_inspiral/`** - Toy post-Newtonian inspiral pipeline for detecting dark matter spike-induced dephasing.

---

## gw_noise_anomaly/

### Anomaly Characterisation of Noise in Gravitational Wave Detector Data

#### Overview

The goal of this project is to test whether the choice of window function carries diagnostic information about the nature of noise anomalies in LIGO detector data. Different glitch types (blips, scattered light arches, power line harmonics) occupy distinct regions of the time-frequency plane, and different windows are differentially sensitive to these morphologies.

We systematically apply multiple window functions and bandpass ranges to segments of LIGO O3 data containing known glitches, and measure how well each combination characterises the local noise. The resulting quality landscape across window-bandpass combinations is then used as input to a machine learning classifier.

Central hypothesis: window preference correlates with glitch morphology, and segments where no window achieves good characterisation may indicate a previously unclassified type of anomaly.

#### Current Status

**Completed:**
- Data retrieval pipeline for LIGO O3 segments via GWOSC
- Implementation and comparison of multiple window functions (Tukey, Hann, Hamming, Blackman) across known glitch types
- Quality metric for evaluating window-bandpass performance on noise segments

**In progress:**
- Building a labelled dataset of window-performance results across glitch classes
- Designing the ML classifier to predict optimal window choice from noise morphology

**Next steps:**
- Apply the trained classifier to noise-only segments to flag potential unclassified anomalies

#### Tools and Libraries
Python, GWOSC, gwpy, Astropy, NumPy, Matplotlib

#### Contents
- `GW_windows.ipynb` - main notebook containing data retrieval, window/bandpass comparison, and quality metric analysis
- `figures/` - contains generated ASD and quality metric in different frequency bands plots of GW190521 (event) and some glitch types.
- `data/` - all files have not been uploaded to the repo for sizing issues, but contains downloaded hdf5 files from GravitySpy O3a catalogues and GWOSC GWTC according to the required time durations, all H1 data so far.

---

## gw_dm_spike_inspiral/

### Dark Matter Spike Dephasing in Post-Newtonian Inspiral Waveforms

#### Overview

I'm building a toy gravitational-wave analysis pipeline that starts from a binary black hole's masses, derives the chirp mass, and uses the leading-order post-Newtonian approximation to generate a "clean" vacuum-GR inspiral waveform, modeling how orbital frequency, phase, and strain amplitude evolve over time purely from Newtonian gravity plus relativistic radiation-reaction corrections, deliberately stopping before merger since PN breaks down there and since the interesting physics for our purposes lives in the slow, cumulative inspiral anyway.

The next step is to add a dynamical-friction correction term (simulating drag from a dark matter density spike) to this same frequency evolution, generate a second "disturbed" waveform, and compare the two - looking specifically for phase drift (dephasing) that accumulates over many orbital cycles as the signature of dark matter's gravitational influence.

The eventual goal is to test this same comparison against real public strain data and published masses from LIGO/Virgo events via GWOSC.

#### Tools and Libraries
Python, GWOSC, gwpy, Astropy, NumPy, Matplotlib

---

## How the two projects connect

Both projects sit on top of the same GWOSC data-retrieval and signal-processing foundation, but probe detector data from opposite directions:

- **`gw_noise_anomaly/`** works *outward-in* - starting from real noisy detector segments and asking what characterises anomalies well enough to flag something as potentially "new."
- **`gw_dm_spike_inspiral/`** works *inward-out* - starting from a clean theoretical waveform and asking what a specific new-physics effect (a DM spike) would look like once imprinted on it.

The intended convergence point is real strain data: the dephasing signature modeled in `gw_dm_spike_inspiral/` is, in effect, a candidate for the kind of "unclassified anomaly" that `gw_noise_anomaly/`'s classifier is designed to flag. Once both pipelines are validated independently, a natural extension is to check whether events flagged by the noise-anomaly classifier show dephasing patterns consistent with the DM-spike model, and vice versa, using the DM-spike waveform as a targeted template to search noise-anomaly-flagged segments.