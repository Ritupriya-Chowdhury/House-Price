# House Price Analysis
Data cleaning and exploratory data analysis (EDA) of a house price dataset, done in a Jupyter notebook with pandas, NumPy, Matplotlib and Seaborn.

## Dataset

- Source: [House Prices on Kaggle](https://www.kaggle.com/datasets/tanyachawla412/house-prices)
- Size: 4548 rows and 7 columns (4545 rows and 6 columns after cleaning)

| Column | Description |
|---|---|
| `Avg. Area Income` | Average income of the area |
| `House Age` | Age of the house in years |
| `Number of Rooms` | Total number of rooms |
| `Number of Bedrooms` | Number of bedrooms |
| `Area Population` | Population of the area |
| `Price` | House price (target) |
| `Address` | House address (dropped during cleaning) |

## Project Files

- `House_price.ipynb`: notebook with the cleaning and EDA code
- `House_price.csv`: dataset (download it from the Kaggle link above)
- `Methodology.md`: step-by-step description of the cleaning and EDA

## Workflow

1. **Data cleaning**
   - Checked for duplicates and missing values (none found)
   - Converted rooms, bedrooms and house age to integers
   - Removed 2 rows where bedrooms exceeded rooms
   - Extracted `State` from `Address`, removed 1 row with no valid state
   - Dropped `Address` and `State` because they add no predictive value
2. **EDA**
   - Price distribution, price by house age, and price by state
   - Distributions of bedrooms, rooms and house age
   - Income vs population and income vs price
   - Price by rooms and bedrooms, and rooms vs bedrooms heatmap
   - Correlation heatmap
3. **Outlier Detection**

## Key Findings

- The most common house price is about 1.0 to 1.5 million.
- Location (state) has little effect on price. The highest (TX) and lowest (HI) state means differ by a ratio of only 1.175.
- Higher area income goes with higher price.
- Number of rooms affects price more than number of bedrooms.
- Newer houses are not more expensive. Average price generally rises with house age up to 9 years.
- Area income and area population show no clear relationship.

## Requirements

- Python 3
- pandas, numpy, matplotlib, seaborn
- Jupyter Notebook

```bash
pip install pandas numpy matplotlib seaborn notebook
```

## How to Run

1. Download `House_price.csv` from the Kaggle link and place it in the same folder as the notebook.
2. Start Jupyter: `jupyter notebook`
3. Open `House_price.ipynb` and run all cells.

## Next Steps

- Outlier detection and handling
- Feature scaling and train/test split
- Price prediction models and evaluation
