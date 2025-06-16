# ⚡ Household Power Consumption Analysis

This project explores energy usage trends from the [Household Power Consumption Dataset](https://archive.ics.uci.edu/ml/datasets/individual+household+electric+power+consumption). It involves cleaning the data, engineering features, building predictive models, and visualizing insights — all using Python.

---

## 📂 Dataset

- **File**: `household_power_consumption.txt`
- **Source**: UCI Machine Learning Repository
- **Frequency**: 1-minute interval measurements
- **Key Columns**:
  - `Date`, `Time`
  - `Global_active_power`, `Global_reactive_power`
  - `Voltage`, `Sub_metering_1/2/3`

---

## 🧼 Data Cleaning

Performed with **pandas**:
- Merged `Date` and `Time` into a `datetime` index
- Replaced `'?'` with `NaN` and converted types to numeric
- Dropped rows with invalid or missing datetime entries
- Resampled data to daily energy consumption (in kWh)
  - `kWh = sum(kW per minute readings) / 60`
- Removed days with missing or zero values

---

## 🔁 Feature Engineering

- Created lag features to represent previous 7 days of energy usage:
  - `lag_1` = yesterday’s energy, `lag_2` = two days ago, ...
- Target variable (`y`) = today's energy usage
- Final dataset format:

  | y     | lag_1 | lag_2 | ... | lag_7 |
  |-------|--------|--------|-----|--------|
  | 20.3 | 22.1   | 19.8   | ... | 24.0   |

---

## 🤖 Modeling

### Models Used:
- **Linear Regression**
- **Random Forest Regressor**

### Workflow:
- 80/20 **chronological split** (train/test)
- Trained using `scikit-learn`
- Evaluated with:
  - **RMSE** (Root Mean Squared Error)
  - **R² Score** (Coefficient of Determination)

---

## 📊 Visualizations

Using **Matplotlib** and **Seaborn**:
- Heatmap showing correlation between lag features and energy
- Actual vs Predicted plots for test set
- Daily energy usage over time

---

## 📈 Results

| Model             | RMSE (kWh) | R² Score |
|------------------|------------|----------|
| Linear Regression | ~2.5       | ~0.60    |
| Random Forest     | ~1.8       | ~0.75    |

> (Results will vary depending on final preprocessing and data range)

---

## 📦 Requirements

Install dependencies with:

```bash
pip install -r requirements.txt
