# GW_project
Anomaly of Noise Characterisation in GW Detector data

The goal of this project is to see whether the choice of window function carries diagnostic information about the nature of noise anomalies. Different glitch types blips, scattered light arches, power line harmonics occupy distinct regions of the time-frequency plane, and different windows are differentially sensitive to these morphologies. We systematically apply multiple window functions and bandpass ranges to segments of LIGO O3 data containing known glitches, and measure how well each combination characterizes the local noise. The resulting quality landscape across window-bandpass combinations is then used as input to a machine learning classifier.

The central hypothesis is that window preference correlates with glitch morphology, and that segments where no window achieves good characterization might mean a new class of anomaly. 
