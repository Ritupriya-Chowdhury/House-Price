# House Price
## EDA
### 1.1 Dataset
1. Dataset Link: [House Prices](https://www.kaggle.com/datasets/tanyachawla412/house-prices)
2. Dataset Size: rows -> 4548, columns -> 7
3. Columns: `Avg. Area Income`, `House Age`, `Number of Rooms`, `Number of Bedrooms`, `Area Population`, `Price`, `Address`

### 1.2 Data Cleaning
1. **Load the data**: Read `House_price.csv` into a pandas DataFrame and check its shape (4548 rows, 7 columns).
2. **Inspect the structure**: Use `df.info()` to check column data types and non-null counts. Six columns are `float64` and `Address` is a string.
3. **Check for duplicates**: `df.duplicated().sum()` returned 0, so no duplicate rows were found.
4. **Check for missing values**: `df.isnull().sum()` returned 0 for every column, so no imputation was needed.
5. **Summary statistics**: Use `df.describe()` to check the range, mean and spread of each numeric column.
6. **Fix data types**:
   - `Number of Rooms` and `Number of Bedrooms` were converted from float to integer (`astype(int)`), because these are counts.
   - `House Age` was rounded to the nearest whole year and converted to integer.
7. **Remove invalid records**: Rows where `Number of Bedrooms` was greater than `Number of Rooms` are logically impossible. 2 such rows were found and dropped, and the index was reset (4548 -> 4546 rows).
8. **Check the Address column**:
   - `Address` has 4546 unique values, so every row is different. It works like an ID and gives no pattern a model can learn.
   - Sample addresses were checked and a regex was used to extract a new `State` column from the two-letter code before the ZIP code.
   - One row (`55454 M`) had no valid state, so it was dropped (4546 -> 4545 rows).
   - The result has 62 unique state codes. These include military and territory codes such as AP, AA, AE, PW, GU and VI.
9. **Drop unnecessary columns**: `Address` and `State` were removed.
   - `Address` is unique for every row and so carries no predictive value.
   - `State` was only extracted to test whether location affects price. The state-wise mean price ranges from about 1.14M (HI) to about 1.35M (TX), a max/min ratio of 1.175. With only about 70 houses per state, this gap is expected from random variation.
10. **Final cleaned dataset**: 4545 rows and 6 columns (`Avg. Area Income`, `House Age`, `Number of Rooms`, `Number of Bedrooms`, `Area Population`, `Price`).

### 1.3 Exploratory Data Analysis (EDA)
1. **Top 10 states by average price** (bar plot): Compared average house price across states before `State` was dropped. The differences between states were small.
2. **Number of houses per state** (bar plot): Checked how many houses each state has. Counts were roughly even except for the military codes (AP, AA, AE), which have more.
3. **Max/min state mean ratio**: Calculated the highest (TX) and lowest (HI) state mean price to confirm that location has little effect on price.
4. **Price distribution** (histogram with KDE and box plot): Showed the shape and spread of `Price`.
   - The most common price range is about 1.0 to 1.5 million.
5. **Average price by house age** (bar chart):
   - Newer houses are not more expensive. Average price generally increases with age, from about 0.85 million at 3 years to a peak of about 1.75 million at 9 years, then falls slightly at 10 years.
6. **Distributions of bedrooms, rooms and house age** (count plots):
   - Most houses have 3 to 4 bedrooms.
   - Most houses have 6 to 7 rooms.
   - The typical house age is 5 to 7 years.
7. **Income vs population** (scatter plot): There is no clear relationship between `Avg. Area Income` and `Area Population`. High-income areas are not necessarily larger in population.
8. **Income vs price** (regression plot): There is a clear positive trend. Higher area income goes with higher price, though the spread of points shows income is not the only factor.
9. **Price by rooms and bedrooms** (box plots):
   - Median price rises steadily with the number of rooms, from about 1.0 million at 4 rooms to about 2.0 million at 10 rooms.
   - The number of bedrooms has only a weak effect, because the price distributions overlap heavily.
10. **Rooms vs bedrooms** (crosstab heatmap): The two are positively but loosely related. 5 and 6 bedrooms only occur in houses with 7 or more rooms, but each room count includes several bedroom counts.
11. **Outlier check (started)**: Numeric columns were selected (`select_dtypes`) to find outliers in the next step.
