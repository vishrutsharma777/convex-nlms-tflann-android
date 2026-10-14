# Real-Time Convex Combination of Adaptive Filters on Android

Advanced Signal Processing (IIT Gandhinagar), Assignment 3 — April 2026.
Authors: **Vishrut Sharma** and **Vikash Kumar Sinha**.

A real-time adaptive filtering system built in Simulink and deployed to two Android phones.

- **Phone A** captures live microphone audio and sends it over TCP/IP.
- **Phone B** receives the signal and runs two adaptive filters in parallel:
  - **NLMS** (normalised least mean squares) — fast convergence, linear model;
  - **TFLANN** (trigonometric functional link artificial neural network) — nonlinear model.
- The two outputs are mixed by a **convex combination** with an adaptive mixing parameter:

  y(n) = λ(n) y₁(n) + (1 − λ(n)) y₂(n),  λ(n) = 1 / (1 + e^(−α(n)))

  α(n+1) = α(n) + μ_λ · e(n) · (y₁(n) − y₂(n)) · λ(n)(1 − λ(n))

  so the combination follows whichever filter is doing better at each moment.
- The error e(n) = d(n) − y(n) and its MSE in dB are computed on the phone.

## Files

| File | What |
| --- | --- |
| `A3.slx` | Simulink model (Android Audio Capture, TCP/IP Send/Receive, NLMS, TFLANN, convex combination, MSE) |
| `ASPA3.pdf` | Report: model, equations, setup and results |

## Requirements

MATLAB/Simulink with the DSP System Toolbox and the **Simulink Support Package for Android
Devices** (needed to deploy to the phones and for the Audio Capture and TCP/IP blocks).
