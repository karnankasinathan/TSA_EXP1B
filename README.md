### Developed by:Karnan K
### Reg no:212222230062
### Date:
# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
3. Perform the Augmented Dickey-Fuller test on the original series.
4. Resample the data monthly, difference it again, and decompose it into seasonal components.
5. Remove the seasonal component and plot the seasonally adjusted series.
6. Apply a log transformation to the seasonally adjusted data and plot it.
### PROGRAM:


```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
from statsmodels.tsa.stattools import adfuller
df = pd.read_csv('/content/baggagecomplaints.csv')
df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)
df.plot(figsize=(12,6))
plt.plot(df['Baggage'])
plt.title('Original Time Series')
plt.show()
result = adfuller(df['Baggage'])
df_diff1 = df['Baggage'].diff().dropna()
plt.figure(figsize=(10,6))
plt.plot(df_diff1)
plt.title('First Differenced Time Series')
plt.show()
result = adfuller(df_diff1)
df_monthly = df.resample('M').sum()
df_diff1 = df_monthly['Baggage'].diff().dropna()
df_diff1.index.freq = 'M'
decomposition = seasonal_decompose(df_diff1, model='additive')
plt.figure(figsize=(10,6))
plt.subplot(413)
plt.plot(decomposition.seasonal,label='Seasonality')
plt.legend(loc='best')
plt.tight_layout()
plt.show()
df_sa = df_diff1 - decomposition.seasonal
plt.figure(figsize=(10,6))
plt.plot(df_sa)
plt.title('Seasonally Adjusted Data')
plt.show()
result = adfuller(df_sa)
df_log = np.log(df_sa)
plt.figure(figsize=(10,6))
plt.plot(df_log)
plt.title('Log-Transformed Data ')
plt.show()
```
### OUTPUT:
![Screenshot 2024-08-25 013021](https://github.com/user-attachments/assets/56f6e3c7-8000-4e05-8842-b8db6f3ee390)


REGULAR DIFFERENCING:

![Screenshot 2024-08-25 013030](https://github.com/user-attachments/assets/f2f6d8db-6b0c-4a4a-b37f-25a53e6cdfc2)

SEASONAL ADJUSTMENT:
![Screenshot 2024-08-25 013039](https://github.com/user-attachments/assets/244b4b69-6557-46fe-a49e-978ef984fde6)


LOG TRANSFORMATION:

![Screenshot 2024-08-25 013047](https://github.com/user-attachments/assets/81388ced-4040-4f84-ab26-78ca53f5781f)

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
