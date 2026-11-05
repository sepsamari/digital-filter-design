# Digital Filter Design with Python

This repository contains my practical exercises and projects in digital filter design as part of my Master's studies in Smart Systems Engineering at Hanze University of Applied Sciences.

The goal is to understand FIR, IIR, and adaptive filters by implementing them in Python and evaluating their performance on simulated signals.

## Featured Project: Robot IMU Filter Comparison

**[View the Jupyter Notebook](projects/Robot_IMU_Filter_Comparison.ipynb)** | **[Read the project overview and results](projects/README.md)**

In this project, I simulated a robot gyroscope measuring angular velocity during straight motion and left and right turns. I added Gaussian sensor noise and motor vibration that changes in frequency and amplitude.

I implemented and compared five filtering approaches:

- FIR low-pass filtering
- IIR low-pass filtering
- LMS adaptive motor-vibration cancellation
- NLMS adaptive motor-vibration cancellation
- Combined LMS + IIR filtering

I evaluated their accuracy using **root mean square error (RMSE)** against the simulated ground truth and compared how quickly the filters responded when the robot started turning.

**Key finding:** In this simulation, the second-order IIR low-pass filter achieved the lowest RMSE (**0.0451 rad/s**) with a measured 50% turn-response delay of **20 ms**. Combining LMS and IIR produced an RMSE of **0.0463 rad/s**, so it did not outperform IIR alone. LMS and NLMS preserved the onset of sudden turns more closely but retained more random sensor noise.

The results are specific to the simulated data and the filter settings used; the notebook does not evaluate a physical robot.

## Topics Covered

- FIR filter design using zero placement
- FIR filters with multiple notch frequencies
- IIR filter design using poles and feedback
- Effect of pole radius on frequency response
- Low-pass filter design using repeated zeros
- FFT and frequency-response analysis
- Passband error and stopband attenuation
- Filter stability and group delay
- LMS and NLMS adaptive noise cancellation
- Filtering simulated robot sensor measurements

## Repository Contents

- **[Projects](projects/)** — Jupyter notebooks covering filter design, noise cancellation, and robotics-related simulations.
- **[Assignments](Assignments/)** — Coursework and filter design assignments.

## Technologies

- Python
- NumPy
- SciPy
- Matplotlib
- Jupyter Notebook

## Project Status

This is an ongoing learning repository. Additional filter design experiments and comparisons may be added as I progress through the course.
