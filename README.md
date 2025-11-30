# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 19/08/2025
### Name: Visalan H
### Register Number: 212223240183

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("C:\DL\dataSets\GoldPrice(2013-2023).csv")

data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

data['Price'] = data['Price'].astype(str).str.replace(',', '').astype(float)
data['price_diff'] = data['Price'] - data['Price'].shift(1)

result = seasonal_decompose(data['Price'], model='additive', period=12)
data['price_sea_diff'] = result.resid

data['price_log'] = np.log(data['Price'])
data['price_log_diff'] = data['price_log'] - data['price_log'].shift(1)

result = seasonal_decompose(data['price_log_diff'].dropna(), model='additive', period=12)
data['price_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Price'], label='Original')
plt.legend(loc='best')
plt.title('Original Gold Price Data')
plt.xlabel('Year')
plt.ylabel('Price')
plt.show()

plt.subplot(6, 1, 2)
plt.plot(data['price_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Price')

plt.subplot(6, 1, 3)
plt.plot(data['price_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Residual')

plt.subplot(6, 1, 4)
plt.plot(data['price_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log')

plt.subplot(6, 1, 5)
plt.plot(data['price_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Log Difference')

plt.subplot(6, 1, 6)
plt.plot(data['price_log_seasonal_diff'], label='Log Transformation + Differencing + Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Log Transformation + Differencing + Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Residual')

plt.tight_layout()
plt.show()

data.plot(kind='line', figsize=(12, 6))
plt.title("Gold Price Transformations")
plt.show()
```

### OUTPUT:


REGULAR DIFFERENCING:

<img width="733" height="171" alt="image" src="https://github.com/user-attachments/assets/5537071a-7277-4d8f-86ad-4b7b1c6107a0" />


SEASONAL ADJUSTMENT:

<img width="733" height="172" alt="image" src="https://github.com/user-attachments/assets/0a7f9389-2cac-4fdf-961b-a9cc45a83dcc" />


LOG TRANSFORMATION:

<img width="715" height="171" alt="image" src="https://github.com/user-attachments/assets/b40bc2d6-fd9e-4ed8-87f4-64badf83782c" />

GOLD PRICE TRANSFORMATIONS

<img width="1241" height="628" alt="image" src="https://github.com/user-attachments/assets/af572fb5-5dfd-42e8-8307-5210193a0e0f" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
