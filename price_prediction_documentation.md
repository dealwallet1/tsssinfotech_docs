# Electronics Price Prediction — Documentation

## What this project does
It predicts the price of an electronics product using its brand, category, past prices, and the date — using a machine learning model called XGBoost.

## Data used
A CSV file of electronics products and their prices (`DatafinitiElectronicsProductsPricingData.csv`). It includes product name, brand, category, and price info collected on different dates.

## Step 1: Cleaning the data
Unnecessary columns (like URLs, IDs, shipping info) are removed since they don't help predict price. Only useful columns are kept.

## Step 2: Preparing text columns
Brand, category, and product name are text values, so they are converted into numbers using Label Encoding, since the model can only understand numbers.

## Step 3: Working with dates
Each product can have multiple prices recorded on different dates. These dates are split apart so each price has its own row, then converted into a proper date format.

## Step 4: Creating new features
From the date, new columns are created: Year, Month, Day, Day of Week, Quarter, Week of Year. This helps the model understand time-based patterns.

## Step 5: Adding price history
For each product, the previous 1st, 2nd, and 3rd prices are added as new columns (Lag_1, Lag_2, Lag_3). This helps the model use past prices to predict the next price.

## Step 6: Splitting data
The data is divided into training data (80%) and testing data (20%). The model learns from the training data and is tested on the testing data.

## Step 7: Training the model
An XGBoost Regressor model is trained using the training data to learn the relationship between the features and the price.

## Step 8: Checking accuracy
The model's predictions are compared with actual prices using three accuracy measures:
- MAE – average error amount
- RMSE – average error, but penalizes bigger mistakes more
- R² Score – how well the model explains price changes (closer to 1 is better)

A graph is also created comparing actual vs predicted prices.

## Step 9: Saving the model
Once trained, the model and everything it needs (encoders, feature list, price history) is saved to Google Drive so it can be reused later without retraining.

## Step 10: Using the saved model
The saved model can be loaded again later, and just by entering a product name, it will predict the price for today's date using the saved history for that product.

## Known issues
- Earlier version of the code reused one encoder for all three columns, which caused wrong encoding. This is fixed in the saving section by using a separate encoder per column.
- If a product name isn't found in the saved history, the tool shows a few example names instead of predicting.
- The saving/loading part is built for Google Colab and needs adjustment to run elsewhere.
