# Airline Passenger Forecasting with LSTM

**Author:** MD ZIHADUL AHSAN RATUL  
**Project type:** Time-series forecasting  
**Model:** Long Short-Term Memory (LSTM) neural network  
**Environment:** Google Colab / Python

## Overview

This project explores time-series forecasting of international airline passenger numbers using an LSTM neural network. Historical monthly passenger values are converted into fixed-length sequences, used to train the model, and then used to forecast the next 10 values.

The notebook includes data loading, visualization, Min-Max scaling, sequence generation, LSTM training, prediction, RMSE evaluation and future forecasting.

## Dataset

The notebook loads a CSV file named:

`AirPassengers.csv`

The notebook reads the second column (`data.iloc[:, 1]`) as the passenger-count series. The CSV file was not included with the uploaded notebook, so it is not bundled in this repository. The notebook does not specify a direct download URL or dataset licence. See [DATASET.md](DATASET.md).

## Methodology

### 1. Data preparation

- Load `AirPassengers.csv` using pandas.
- Extract the passenger values from the second column.
- Reshape the series into a single-column array.
- Convert values to `float32`.
- Scale values to the range 0–1 using `MinMaxScaler`.
- Split the sequence chronologically: 80% training data and 20% test data.

### 2. Sequence generation

The notebook uses a time step of **12**. Each input sequence contains 12 observations, and the corresponding target is the following observation.

The sequences are reshaped into the three-dimensional input format expected by the LSTM layer.

### 3. LSTM architecture and training

The model in the notebook consists of:
- An LSTM layer with 32 units.
- A Dense output layer with 1 unit.
- Mean Squared Error loss.
- Adam optimizer.
- 50 training epochs.
- Batch size of 1.

### 4. Evaluation

The notebook calculates:
- Training RMSE.
- Test RMSE.

It also plots actual passenger values alongside training and test predictions.

### 5. Future forecasting

The notebook recursively predicts **10 future values**. Each predicted value is appended to the input sequence and used to generate the next forecast. Predictions are inverse-transformed back to passenger-count scale and plotted.

## Repository contents

```text
.
├── airline_passenger_forecasting_lstm.ipynb
├── README.md
├── DATASET.md
├── requirements.txt
├── .gitignore
└── LICENSE
```

## Run in Google Colab

1. Open Google Colab.
2. Upload `airline_passenger_forecasting_lstm.ipynb`.
3. Upload `AirPassengers.csv` when the notebook prompts for a file.
4. Run the cells sequentially.
5. Review the RMSE scores, prediction plot and 10-step forecast.

## Run locally

Use Python 3.10 or 3.11 where possible.

```bash
python -m venv .venv
```

Activate the environment, then install dependencies:

```bash
pip install -r requirements.txt
```

Launch Jupyter:

```bash
jupyter notebook
```

Place `AirPassengers.csv` in the notebook's working directory. The notebook includes `google.colab.files.upload()`, which is specific to Google Colab; for local execution, replace that upload cell with a local file-path workflow.

## Notes and limitations

- The dataset file is not included in this package.
- The notebook fits `MinMaxScaler` on the full series before splitting into training and test portions. This allows information from the test period to influence the scaling range. For a stricter time-series evaluation, fit the scaler on training data only and apply that fitted scaler to the test data.
- The notebook reshapes each 12-value sequence to `(samples, 1, time_step)`, so the LSTM receives one timestep with 12 features rather than 12 sequential timesteps. This documents the supplied implementation as written.
- The 10 future values are generated recursively, so forecast errors can accumulate across steps.
- The notebook does not include saved, verified RMSE values in its source code. Run it with the dataset to generate the metrics.
- This is an educational forecasting experiment, not an operational airline demand forecasting system. Forecast reliability depends on data quality, time coverage and model validation.
- The original notebook is preserved as supplied; this package adds documentation and does not rebuild or independently validate the experiment.
