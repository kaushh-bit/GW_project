# GW_project

## Anomaly Characterisation of Noise in Gravitational Wave Detector Data

### Overview

The goal of this project is to test whether the choice of window function carries diagnostic information about the nature of noise anomalies in LIGO detector data. Different glitch types (blips, scattered light arches, power line harmonics) occupy distinct regions of the time-frequency plane, and different windows are differentially sensitive to these morphologies.

We systematically apply multiple window functions and bandpass ranges to segments of LIGO O3 data containing known glitches, and measure how well each combination characterises the local noise. The resulting quality landscape across window-bandpass combinations is then used as input to a machine learning classifier.

Central hypothesis: window preference correlates with glitch morphology, and segments where no window achieves good characterisation may indicate a previously unclassified type of anomaly.

### Current Status

Completed:
Data retrieval pipeline for LIGO O3 segments via GWOSC
Implementation and comparison of multiple window functions (Tukey, Hann, Hamming, Blackman) across known glitch types
Quality metric for evaluating window-bandpass performance on noise segments

In progress:
Building a labelled dataset of window-performance results across glitch classes
Designing the ML classifier to predict optimal window choice from noise morphology

Next steps:
Apply the trained classifier to noise-only segments to flag potential unclassified anomalies
Tools and Libraries
Python, GWOSC, gwpy, Astropy, NumPy, Matplotlib
Repository Structure
GW_windows.ipynb — main notebook containing data retrieval, window/bandpass comparison, and quality metric analysis

### Author
Kaushiki Roy, B.Sc. Physics, St. Xavier's College, Ahmedabad //
itskaushh@gmail.com