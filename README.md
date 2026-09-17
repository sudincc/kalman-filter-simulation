# Discrete-Time Kalman Filter (State Estimation)

A clean, straightforward implementation of a discrete-time linear Kalman filter built to track dynamic states from noisy sensor measurements.

I put this project together to bridge the gap between textbook linear control theory and a practical, hands-on simulation. Sensors in real-world systems (whether on a flight computer, rocket IMU, or mobile robot) are inevitably corrupted by noise. This filter demonstrates how fusing dynamic model predictions with noisy measurements yields an estimate that is substantially closer to the true state than raw sensor readings alone.

---

## 📌 What This Project Does

- **Dynamic State Tracking:** Simulates a system moving over discrete time steps while subjected to process uncertainty.
- **Sensor Noise Modeling:** Adds zero-mean Gaussian measurement noise to replicate realistic sensor readings.
- **Recursive Filtering:** Implements the classic prediction-correction loop:
  1. **Predict:** Project state and error covariance ahead using system dynamics.
  2. **Update:** Compute the optimal Kalman gain ($K$) and correct the state estimate with incoming sensor data ($z_k$).

---

## 📐 The Math Behind It

The core recursive loop follows standard discrete linear equations:

### 1. Prediction (Time Update)
- State projection:  
  $$\hat{x}_{k|k-1} = F \hat{x}_{k-1|k-1} + B u_k$$
- Covariance projection:  
  $$P_{k|k-1} = F P_{k-1|k-1} F^T + Q$$

### 2. Correction (Measurement Update)
- Kalman Gain:  
  $$K_k = P_{k|k-1} H^T (H P_{k|k-1} H^T + R)^{-1}$$
- State estimate update:  
  $$\hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k (z_k - H \hat{x}_{k|k-1})$$
- Error covariance update:  
  $$P_{k|k} = (I - K_k H) P_{k|k-1}$$

Where **$Q$** represents process noise covariance (trust in physics model) and **$R$** represents measurement noise covariance (trust in sensor data).

---

## 💡 Key Takeaway & Intuition

Tuning the ratio between $Q$ and $R$ dictates the filter's personality:
- **High $R$ / Low $Q$:** The filter relies heavily on the physical model. It smooths out aggressive spikes effectively, but reacts more sluggishly to sudden state changes.
- **Low $R$ / High $Q$:** The filter trusts incoming sensor readings quickly. It tracks rapid maneuvers well, but lets more sensor flutter pass through into the state estimate.

---

## 🚀 How to Run

1. Clone or download this repo.
2. Open the script in your preferred environment (Python or MATLAB).
3. Run the file to simulate the loop and view the comparison plot between:
   - **Ground Truth** (actual simulated dynamics)
   - **Noisy Measurements** (simulated sensor feed)
   - **Kalman Estimate** (filtered output tracking truth)

---
*Built as part of ongoing personal studies in control theory, state estimation, and dynamic systems.*