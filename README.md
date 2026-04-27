# Kalman Filter Prediction Tool

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Multi-Model State Estimation with Confidence Intervals**

A desktop application that reads a time series from a CSV file and uses Kalman filtering to predict the next 10 values with 95% confidence intervals. Supports multiple filter types and motion models, with real-time visualization of predictions against historical data.

## Features

| Feature | Description |
|---------|-------------|
| **Multiple Filter Types** | Standard Kalman Filter, Extended Kalman Filter (EKF), Unscented Kalman Filter (UKF) |
| **Motion Models** | Constant Velocity, Constant Acceleration — selectable per analysis |
| **Confidence Intervals** | 95% CI computed from predicted state covariance matrices |
| **Noise Tuning** | Adjustable process noise parameter for filter sensitivity control |
| **Visualization** | Matplotlib-based plots of historical data, predictions, and confidence bands |
| **GUI** | Tkinter desktop interface — load CSV, configure filter, run prediction, view results |

## How It Works

1. **Load** a single-column CSV of numeric values (any time series — prices, sensor readings, measurements)
2. **Select** a filter type (Standard / EKF / UKF) and motion model (Constant Velocity / Constant Acceleration)
3. **Run** — the tool normalizes the data, constructs state-space matrices, runs the Kalman filter forward pass, then propagates the final state and covariance 10 steps ahead
4. **Output** — predicted values with confidence intervals displayed in a table and plotted graphically

## Technical Details

- **State-space formulation**: Constructs F (transition), H (observation), Q (process noise), and R (measurement noise) matrices based on selected motion model
- **Normalization**: Input data is z-score normalized before filtering, predictions are denormalized for display
- **Covariance propagation**: `P_next = F @ P @ F.T + Q` at each prediction step; CI = `1.96 * sqrt(P[0,0])`
- **Implementation**: ~725 lines of Python using `pykalman`, `filterpy`, `numpy`, `pandas`, `matplotlib`

## Dependencies

```
numpy
pandas
pykalman
filterpy
matplotlib
```

## Usage

```bash
pip install numpy pandas pykalman filterpy matplotlib
python predictive_software.py
```

Or build a standalone executable:

```bash
pip install pyinstaller
pyinstaller --onefile --windowed predictive_software.py
```

## Example

Input: A CSV with 830 daily gold prices (Feb 2022 – Apr 2025)
Output: 10-day price forecast with confidence bands

## Author

**Dr. Mosab Hawarey**
PhD, Geodetic & Photogrammetric Engineering (ITU) | MSc, Geomatics (Purdue) | MBA (Wales) | BSc, MSc (METU)

- GitHub: https://github.com/mhawarey
- Personal: https://hawarey.org/mosab
- ORCID: https://orcid.org/0000-0001-7846-951X

## License

MIT License
