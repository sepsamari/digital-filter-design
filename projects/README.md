# Digital Filtering Projects

This folder contains Python and Jupyter Notebook experiments in digital signal processing, including FIR and IIR filter design, adaptive noise cancellation, and simulated robotics applications.

The notebooks explore how filters behave in practice through signal simulation, frequency-response analysis, time-domain plots, and quantitative comparisons.

## Featured Project: Robot IMU Filter Comparison

**Notebook:** [Robot_IMU_Filter_Comparison.ipynb](Robot_IMU_Filter_Comparison.ipynb)

### Problem

A robot's gyroscope measures angular velocity, but its readings can be affected by random sensor noise and periodic motor vibration. Filtering these measurements requires a balance between reducing interference and preserving rapid changes when the robot turns.

This project uses **simulated gyroscope data**, not measurements collected from a physical robot.

### Simulation setup

- **Sampling frequency:** 200 Hz
- **Duration:** 10 seconds
- **Robot motion:** straight movement, a left turn at 0.6 rad/s, and a right turn at -0.4 rad/s
- **Random sensor noise:** zero-mean Gaussian noise with a standard deviation of 0.05 rad/s
- **Motor vibration:** frequency changes from 35 Hz to 55 Hz at 5 seconds, while amplitude increases from 0.12 to 0.22 rad/s
- **Adaptive-filter reference:** a signal correlated with the motor vibration, with a fixed phase offset

### Methods compared

1. **FIR low-pass:** 31-tap filter, 10 Hz cutoff
2. **IIR low-pass:** second-order Butterworth filter, 10 Hz cutoff
3. **LMS:** two-tap adaptive motor-vibration cancellation
4. **NLMS:** two-tap normalized adaptive motor-vibration cancellation
5. **Combined LMS + IIR:** LMS output processed by the same IIR low-pass filter

### Results

The root mean square error (RMSE) is calculated against the known simulated angular velocity.

| Method | RMSE (rad/s) | 50% left-turn response delay |
| --- | ---: | ---: |
| Unfiltered measurement | 0.1354 | — |
| FIR | 0.0849 | 75 ms |
| **IIR** | **0.0451** | **20 ms** |
| LMS | 0.0535 | 0 ms* |
| NLMS | 0.0533 | 0 ms* |
| LMS + IIR | 0.0463 | Not measured |

*The 0 ms result means the adaptive-filter output crossed half of the target turn rate at the first sample of the turn. It does not imply zero processing latency. At 200 Hz, the sampling interval is 5 ms.*

### Main finding

**The second-order IIR filter was the preferred option for this simulation.** It achieved the lowest overall RMSE with a relatively short measured response delay. LMS and NLMS preserved the onset of sudden turns more closely, but retained more independent sensor noise. Adding LMS before IIR did not improve RMSE compared with IIR alone.

These results apply to the simulated signals and chosen filter settings; they do not establish that IIR is always the best choice for real robot IMUs.

### How to run

Open [Robot_IMU_Filter_Comparison.ipynb](Robot_IMU_Filter_Comparison.ipynb) in Jupyter Notebook or JupyterLab and run the cells in order.

The notebook uses **Python, NumPy, SciPy, and Matplotlib**.

## Other Notebooks

### FIR and IIR filter design

- [Manual_FIR_NotchFilter.ipynb](Manual_FIR_NotchFilter.ipynb)
- [Manual_FIR_Bandpass_Design.ipynb](Manual_FIR_Bandpass_Design.ipynb)
- [Manual_FIR_IIR_Lowpass_Design.ipynb](Manual_FIR_IIR_Lowpass_Design.ipynb)
- [Manual_IIR_filter.ipynb](Manual_IIR_filter.ipynb)
- [Manual_IIR_Bandpass_Design.ipynb](Manual_IIR_Bandpass_Design.ipynb)
- [IIR_Notch_Bandwidth_Design.ipynb](IIR_Notch_Bandwidth_Design.ipynb)

### Adaptive filtering and noise analysis

- [LMS_Adaptive_Noise_Cancellation.ipynb](LMS_Adaptive_Noise_Cancellation.ipynb)
- [Adaptive_LMS_Changing_Noise.ipynb](Adaptive_LMS_Changing_Noise.ipynb)
- [Normalized_LMS_Filter.ipynb](Normalized_LMS_Filter.ipynb)
- [Periodic_vs_White_Noise_Filtering.ipynb](Periodic_vs_White_Noise_Filtering.ipynb)

### Robotics application

- [Robot_Sensor_Filtering.ipynb](Robot_Sensor_Filtering.ipynb)

---

**Note:** These notebooks are learning and experimental projects. Their results are intended to illustrate filtering concepts and trade-offs, not to validate a deployed robot control system.
