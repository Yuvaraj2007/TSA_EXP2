# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
# NAME : YUVARAJ M
# REG NO : 212224040377
# Date: 22/04/2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### TOOLS REQUIRED:
```
Google colab 
Data set name : Stock market Data set
```
### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv('/content/1a1dde51-8d29-46db-92b7-0b677236ab7d.csv')

data['Date'] = pd.to_datetime(data['Date'])
data = data.drop_duplicates(subset='Date')
data = data.sort_values('Date')
data.set_index('Date', inplace=True)

col = 'High'

data['diff'] = data[col].diff()

result = seasonal_decompose(data[col].dropna(), model='additive', period=30)
data['sea_diff'] = np.nan
data.loc[result.resid.index, 'sea_diff'] = result.resid

data['log'] = np.log(data[col])
data['log_diff'] = data['log'].diff()

result = seasonal_decompose(data['log_diff'].dropna(), model='additive', period=30)
data['log_sea_diff'] = np.nan
data.loc[result.resid.index, 'log_sea_diff'] = result.resid

plt.figure(figsize=(16,16))

plt.subplot(6,1,1)
plt.plot(data[col])
plt.title('Original High')

plt.subplot(6,1,2)
plt.plot(data['diff'])
plt.title('Differencing')

plt.subplot(6,1,3)
plt.plot(data['sea_diff'])
plt.title('Seasonal Adjusted')

plt.subplot(6,1,4)
plt.plot(data['log'])
plt.title('Log')

plt.subplot(6,1,5)
plt.plot(data['log_diff'])
plt.title('Log + Diff')

plt.subplot(6,1,6)
plt.plot(data['log_sea_diff'])
plt.title('Log + Diff + Seasonal')

plt.tight_layout()
plt.show()
```

### OUTPUT
REGULAR DIFFERENCING:
<img width="747" height="249" alt="image" src="https://github.com/user-attachments/assets/a3dc2cea-4839-4f2e-8b4f-31264d55af5f" />
SEASONAL ADJUSTMENT:
<img width="741" height="124" alt="image" src="https://github.com/user-attachments/assets/266f2f59-ec59-4212-91f2-3e94d820c40f" />
LOG TRANSFORMATION:
<img width="747" height="374" alt="image" src="https://github.com/user-attachments/assets/4e1704b8-d02f-489d-9229-3db4a7090999" />



### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
