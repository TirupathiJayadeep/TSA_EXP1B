# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 25-07-2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from statsmodels.tsa.seasonal import seasonal_decompose
data=pd.read_csv("Month_Value_1.csv")

data['Period'] = pd.to_datetime(data['Period'], format='%d.%m.%Y')
data['Revenue'] = pd.to_numeric(data['Revenue'], errors='coerce')
data.set_index('Period', inplace=True)
data = data.dropna(subset=['Revenue'])
data['revenue_diff'] = data['Revenue'].diff()
result = seasonal_decompose(
    data['Revenue'].dropna(),
    model='additive',
    period=12
)
data['revenue_sea_diff'] = result.resid

data['revenue_log'] = np.log(data['Revenue'])
data['revenue_log_diff'] = (
    data['revenue_log'] -
    data['revenue_log'].shift(1)
)
result = seasonal_decompose(
    data['revenue_log_diff'].dropna(),
    model='additive',
    period=12
)
data['revenue_log_seasonal_diff'] = result.resid
plt.figure(figsize=(16,16))
plt.subplot(6,1,1)
plt.plot(data['Revenue'], label='Original')
plt.legend(loc='best')
plt.title('Original Revenue')
plt.xlabel('Year')
plt.ylabel('Revenue')

# Regular Difference
plt.subplot(6,1,2)
plt.plot(data['revenue_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Revenue')

# Seasonal Adjustment
plt.subplot(6,1,3)
plt.plot(data['revenue_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Revenue')

# Log Transformation
plt.subplot(6,1,4)
plt.plot(data['revenue_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Revenue)')

# Log + Difference
plt.subplot(6,1,5)
plt.plot(data['revenue_log_diff'], label='Log + Difference')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Difference')
plt.xlabel('Year')
plt.ylabel('Diff(Log(Revenue))')

# Log + Seasonal Difference
plt.subplot(6,1,6)
plt.plot(data['revenue_log_seasonal_diff'],
         label='Log + Regular + Seasonal Difference')
plt.legend(loc='best')
plt.title('Log + Regular + Seasonal Difference')
plt.xlabel('Year')
plt.ylabel('Seasonally Differenced Log(Revenue)')

plt.tight_layout()
plt.show()

# Plot all columns
data.plot(figsize=(12,6))
plt.show()
```
### OUTPUT:
ORIGINAL:
<img width="1247" height="211" alt="image" src="https://github.com/user-attachments/assets/ef09b32c-3666-4477-ac9e-b9419e46cac2" />

REGULAR DIFFERENCING:
<img width="1241" height="201" alt="image" src="https://github.com/user-attachments/assets/48460f4b-5f9b-4536-b14d-7565ffda9313" />

SEASONAL ADJUSTMENT:
<img width="1241" height="202" alt="image" src="https://github.com/user-attachments/assets/89ee2c17-1372-4bbf-b264-8c84b0643f1a" />

LOG TRANSFORMATION:
<img width="1247" height="206" alt="image" src="https://github.com/user-attachments/assets/5c302782-9889-4608-a63d-6146ac7d2583" />

LOG TRANSFORMATION + REGULAR DIFFERENCE & LOG + REGULAR + SEASONAL DIFFERENCE:
<img width="1243" height="426" alt="image" src="https://github.com/user-attachments/assets/fb7d0d7b-20e9-4562-892c-d26c6d6fb5a3" />



### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
