# Dataset Information

## Required file

The notebook expects a CSV file named:

`AirPassengers.csv`

It reads the passenger-count series from the second column:

```python
dataset = data.iloc[:, 1].values
```

## Dataset availability

The CSV was not included with the uploaded notebook. The notebook does not provide a dataset download URL, publisher citation or licence statement. This repository therefore does not include or claim a source for the data.

Before publishing a dataset file, verify its original source and redistribution terms.

## Expected structure

The CSV must contain at least two columns:
- A first column that may contain the time/month label.
- A second column containing numeric passenger counts.

The notebook uses the second column as the time series.

## Setup

### Google Colab

Upload `AirPassengers.csv` when the notebook's upload cell runs. The filename must match exactly.

### Local Jupyter

Place `AirPassengers.csv` in the notebook's working directory and replace the Google Colab upload cell with a local file path if needed.
