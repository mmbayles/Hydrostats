Hydrostats
==========

## Contents

### [Mac OS X Installation Notes](#mac-os-x)

### Metrics

+ [Mean Error](#hydrostatsme)
+ [Mean Absolute Error](#hydrostatsmae)
+ [Mean Squared Error](#hydrostatsmse)
+ [Eclidean Distance](#hydrostatsed)
+ [Normalized Eclidean Distance](#hydrostatsned)
+ [Root Mean Square Error](#hydrostatsrmse)
+ [Root Mean Squared Log Error](#hydrostatsrmsle)
+ [Mean Absolute Scaled Error](#hydrostatsmase)
+ [Coefficient of Determination (R^2)](#hydrostatsr_squared)
+ [Anomoly Correlation Coefficient](#hydrostatsacc)
+ [Mean Absolute Percentage Error](#hydrostatsmape)
+ [Mean Absolute Percentage Deviation](#hydrostatsmapd)
+ [Symmetric Mean Absolute Percentage Error (1)](#hydrostatssmap1)
+ [Symmetric Mean Absolute Percentage Error (2)](#hydrostatssmap2)
+ [Index of Agreement (d)](#hydrostatsd)
+ [Index of Agreement (d1)](#hydrostatsd1)
+ [Index of Agreement Refined (dr)](#hydrostatsdr)
+ [Relative Index of Agreement](#hydrostatsdrel)
+ [Modified Index of Agreement](#hydrostatsdmod)
+ [Watterson's M](#hydrostatswatt_m)
+ [Mielke-Berry R](#hydrostatsmb_r)
+ [Nash-Sutcliffe Efficiency](#hydrostatsnse)
+ [Modified Nash-Sutcliffe Efficiency](#hydrostatsnse_mod)
+ [Relative Nash-Sutcliffe Efficiency](#hydrostatsnse_rel)
+ [Legate-McCabe Index](#hydrostatslm_index)
+ [Spectral Angle](#hydrostatssa)
+ [Spectral Correlation](#hydrostatssc)
+ [Spectral Information Divergence](#hydrostatssid)
+ [Spectral Gradient Angle](#hydrostatssga)

### [H - Metrics](#h-metrics---methods-from-tornqvist-l-vartia-p-and-vartia-yo-1985)

+ [H1](#hydrostatsh1)
+ [H2](#hydrostatsh2)
+ [H3](#hydrostatsh3)
+ [H4](#hydrostatsh4)
+ [H5](#hydrostatsh5)
+ [H6](#hydrostatsh6)
+ [H7](#hydrostatsh7)
+ [H8](#hydrostatsh8)
+ [H10](#hydrostatsh10)

### Making Tables and Time Lag Analysis
+ [Making Tables](#hydrostatsmake_table)
+ [Time Lag Analysis](#hydrostatstime_lag)

### Data Management:
+ [Merging Data](#hydrostatsdatamerge_data)
+ [Finding Seasonal Periods](#hydrostatsdataseasonal_period)
+ [Finding Daily Averages](#hydrostatsdatadaily_average)
+ [Finding Daily Standard Error](#hydrostatsdatadaily_std_error)
+ [Finding Monthly Averages](#hydrostatsdatamonthly_average)
+ [Finding Monthly Standard Error](#hydrostatsdatamonthly_std_error)


### Visualization
+ [Time Series Plot](#hydrostatsvisualplot)
+ [Histogram](#hydrostatsvisualhist)
+ [Scatter Plot](#hydrostatsvisualscatter)
+ [Quantile-Quantile Plot](#hydrostatsvisualqqplot)

### Appendix
+ [List of Available Timezones](#available-timezones)

# Mac OS X

When installing hydrostats on Mac OSX operating system, you may get the following error when trying to run python scripts using hydrostats in an IDE such as PyCharm. 

```python
**RuntimeError**: Python is not installed as a framework. The Mac OS X backend will not be able to function correctly if Python is not installed as a framework. See the Python documentation for more information on installing Python as a framework on Mac OS X. Please either reinstall Python as a framework, or try one of the other backends.
```

If this happens, you will need to manually change the backend for use in your IDE. This can be done by running the following commands in the terminal:

```Shell Session
sudo apt install nano # If you have not already installed it

vim ~/.matplotlib/matplotlibrc # Create a file called matplotlibrc
```
Then add the following code to the file you created:
```
backend: TkAgg
```

For more information about backends, read [here](https://matplotlib.org/faq/usage_faq.html#what-is-a-backend).

# Metrics

hydrostats.me
-------------

#### class hydrostats.me(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L13 "Source Code")

#### Mean Error (ME) 

![Mean Error](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/ME.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

The ME measures the difference between the simulated data and the observed data (Fisher, 1920).  For the mean error, a smaller number indicates a better fit to the original data. Note that if the error is in the form of random noise, the mean error will be very small, which can skew the accuracy of this metric. ME is cumulative and will be small even if there are large positive and negative errors that balance.  

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.me(sim, obs)
```

hydrostats.mae
-------------

#### class hydrostats.mae(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L13 "Source Code")

#### Mean Absolute Error (MAE) 

![Mean Absolute Error](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/MAE.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

The ME measures the absolute difference between the simulated data and the observed data. For the mean abolute error, a smaller number indicates a better fit to the original data.  

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.mae(sim, obs)
```

hydrostats.mse
-------------

#### class hydrostats.mse(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L35 "Source Code")

#### Mean Squared Error (MSE) 

![Mean Squared Error](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/MSE.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

The MSE measures the squared difference between the simulated data and the observed data.  For the mean squared error, a smaller number indicates a better fit to the original data.  

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.mse(sim, obs)
```

hydrostats.ed
-------------

#### class hydrostats.ed(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L46 "Source Code")

#### Euclidean Distance (ED) 
The ED function returns the Euclidean Distance error metric.  

![Euclidean Distance](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/ED.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.ed(sim, obs)
```

hydrostats.ned
-------------

#### class hydrostats.ned(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L57 "Source Code")

#### Normalized Euclidean Distance (NED) 
The NED function returns the Normalized Euclidean Distance error metric.  

![Normalized Euclidean Distance](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/NED.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.ed(sim, obs)
```

hydrostats.rmse
-------------

#### class hydrostats.rmse(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False) 
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L70 "Source Code")

#### Root Mean Square Error (RMSE) 
The RMSE measures the difference between the simulated data and the observed data.  For the RMSE, a smaller number indicates a better fit to the original data. The RMSE is biased towards large values and outliers, and is one of the most common metric used to describe error. 

![Root Mean Square Error](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/RMSE.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.rmse(sim, obs)
```

hydrostats.rmsle
-------------

#### class hydrostats.rmsle(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)  
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L81 "Source Code")

#### Root Mean Square of Log Error (RMSLE) 
The RMSLE measures the difference between the logged simulated data and the logged observed data.  For the RMSLE, a smaller number indicates a better fit to the original data. The RMSLE removes the biases towards larger numbers by removing outliers within the log transformation of the data. 

![Root Mean Square Log Error](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/RMSLE.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.rmsle(sim, obs)
```

hydrostats.mase
-------------

#### class hydrostats.mase(simulated_array, observed_array, m=1, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)  
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L93 "Source Code")

#### Mean Absolute Scaled Error (MASE) 
Returns the mean absolute scaled error metric 

![Mean Absolute Scaled Error](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/MASE.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| m = 1            | Integer input indicating the seasonal period m. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.mase(sim, obs, m=2)
```

hydrostats.r_squared
-------------

#### class hydrostats.r_squared(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)   
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L109 "Source Code")

#### R^2 Coefficient
The R^2 Coefficient, or coefficient of determination, is used to determine the linear correlation between two datasets.  An R^2 coefficient of 1.0 signifies perfect linear correlation between the two data sets. An R^2 coefficient of 0 signifies no linear correlation. The R^2 coefficient is sensitive to timing changes between the two data sets as well as outliers. 

![Coefficient of Determination](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/r_squared.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.r_squared(sim, obs)
```

hydrostats.acc
-------------

#### class hydrostats.acc(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L122 "Source Code")

#### Anomaly Correlation Coefficient (ACC)
The ACC is used to define any correlation (positive or negative) between two data sets.  It ignores any potential biases due to large or small values.  An ACC value of 1.0 corresponds to a perfect one-to-one positive correlation, an ACC value of -1.0 corresponds to a perfect one-to-one negative correlation, and an ACC value of 0 corresponds to no correlation between the datasets. 

![Anomaly Correlation Coefficient](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/ACC.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.acc(sim, obs)
```

hydrostats.mape
-------------

#### class hydrostats.mape(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L136 "Source Code")

#### Mean Absolute Percentage Error (MAPE)
Returns the mean absolute percentage error metric value.

![Mean Absolute Percentage Error](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/MAPE.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.mape(sim, obs)
```

hydrostats.mapd
-------------

#### class hydrostats.mapd(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L147 "Source Code")

#### Mean Absolute Percentage Deviation (MAPD)
Returns the Mean Absolute Percentage Deviation.

![Mean Absolute Percentage Deviation](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/MAPD.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.mapd(sim, obs)
```

hydrostats.smap1
-------------

#### class hydrostats.smap1(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L158 "Source Code")

#### Symmetric Mean Absolute Percentage Error (1) (SMAP1)
Returns the Symmetric Mean Absolute Percentage Error (1).

![Symmetric Mean Absolute Percentage Error (1)](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/SMAP1.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.smap1(sim, obs)
```

hydrostats.smap2
-------------

#### class hydrostats.smap2(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L172 "Source Code")

#### Symmetric Mean Absolute Percentage Error (2) (SMAP2)
Returns the Symmetric Mean Absolute Percentage Error (2).

![Symmetric Mean Absolute Percentage Error (2)](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/SMAP2.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.smap2(sim, obs)
```

hydrostats.d
-------------

#### class hydrostats.d(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L185 "Source Code")

#### Index of Agreement (D)
Returns the Index of Agreement (d).

![Index of Agreement](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/D.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.d(sim, obs)
```

hydrostats.d1
-------------

#### class hydrostats.d1(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L199 "Source Code")

#### Index of Agreement (1) (D1)
Returns the Index of Agreement (d1).

![Index of Agreement (1)](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/D1.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.d1(sim, obs)
```

hydrostats.dr
-------------

#### class hydrostats.dr(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L212 "Source Code")

#### Index of Agreement (DR)
Returns the refined Index of Agreement (dr).

![Index of Agreement (DR)](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/D_r.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.dr(sim, obs)
```

hydrostats.drel
-------------

#### class hydrostats.drel(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L228 "Source Code")

#### Index of Agreement (DREL)
Returns the relative Index of Agreement.

![Index of Agreement (DREL)](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/DR.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | A 1D Numpy array of forecasted data from the time series.   |
| observed_array   | A 1D Numpy array of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.drel(sim, obs)
```

hydrostats.dmod
-------------

#### class hydrostats.dmod(simulated_array, observed_array, j=1, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)    
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L241 "Source Code")

#### Index of Agreement (DMOD)
Returns the modified Index of Agreement.

![Index of Agreement (DMOD)](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/DM.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| j = 1            | Integer input indicating the j values desired. | 
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.dmod(sim, obs)
```

hydrostats.watt_m
-------------

#### class hydrostats.watt_m(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L254 "Source Code")

#### Watterson's M (M)
Returns Watterson's M value [1]. 

![Watterson's M](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/M.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.dmod(sim, obs)
```

#### References
+ [1] Watterson IG. 1996. Non-dimensional measures of climate model performance. International Journal of Climatology 16: 379–391.

hydrostats.mb_r
-------------

#### class hydrostats.mb_r(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L268 "Source Code")

#### Mielke-Berry R (R)
Returns the Mielke-Berry R value [1]. 

![Mielke-Berry R](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/R.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.mb_r(sim, obs)
```

#### References
+ [1] Mielke PW Jr, Berry KJ. 2001. Permutation Methods: A Distance Function Approach. Springer-Verlag: New York; 352.

hydrostats.nse
-------------

#### class hydrostats.nse(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False) 
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L295 "Source Code")

#### Nash-Sutcliffe Efficiency (NSE)
The NSE [1] is used widely for hydrologic validation and calibration.  It is sensitive to outliers, and the distribution of the datapoints must be normalized (usually with a log transformation) before analysis can be done.  A NSE value of 1.0 means that there is no error in the dataset, whereas a negative value shows that the average of the observed data would serve as a better model than the predicted data. 

![Nash-Sutcliffe Efficiency](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/NSE.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.nse(sim, obs)
```

#### References
+ [1] Nash JE, Sutcliffe JV. 1970. River flow forecasting through conceptual models part I—A discussion of principles. Journal of Hydrology 10(3): 282–290.

hydrostats.nse_mod
-------------

#### class hydrostats.nse_mod(simulated_array, observed_array, j=1, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L308 "Source Code")

#### Modified Nash-Sutcliffe Efficiency (MNSE)
Returns the modified Nash-Sutcliffe Efficiency value [1, 2].

![Modified Nash-Sutcliffe Efficiency (MNSE)](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/NSE_MOD.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| j = 1            | Integer input indicating the desired j value. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.nse_mod(sim, obs)
```

#### References
+ [1] Krause, P., Boyle, D. P., and Base, F.: Comparison of different efficiency criteria for hydrological model assessment, Adv. Geosci., 5, 89-97, 2005.
+ [2] Legates, D. R., and G. J. McCabe Jr. (1999), Evaluating the Use of "Goodness-of-Fit" Measures in Hydrologic and Hydroclimatic Model Validation, Water Resour. Res., 35(1), 233-241.

hydrostats.nse_rel
-------------

#### class hydrostats.nse_rel(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L324 "Source Code")

#### Relative Nash-Sutcliffe Efficiency (RELNSE)
Returns the relative Nash-Sutcliffe Efficiency value [1, 2].

![Relative Nash-Sutcliffe Efficiency (RELNSE)](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/NSE_REL.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.nse_rel(sim, obs)
```

#### References
+ [1] Krause, P., Boyle, D. P., and Base, F.: Comparison of different efficiency criteria for hydrological model assessment, Adv. Geosci., 5, 89-97, 2005.
+ [2] Legates, D. R., and G. J. McCabe Jr. (1999), Evaluating the Use of "Goodness-of-Fit" Measures in Hydrologic and Hydroclimatic Model Validation, Water Resour. Res., 35(1), 233-241.

hydrostats.lm_index
-------------

#### class hydrostats.lm_index(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L340 "Source Code")

#### Legate-McCabe Index (LMINDX)
Returns the Legate-McCabe index [1].

![Legate-McCabe Index](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/E1.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.lm_index(sim, obs)
```

#### References
+ [1] Legates DR, McCabe GJ Jr. 1999. Evaluating the use of “goodness-of-fit” measures in hydrologic and hydroclimatic model validation. Water Resources Research 35(1): 233–241.

hydrostats.sa
-------------

#### class hydrostats.sa(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L353 "Source Code")

#### Spectral Angle Coefficient (SA)
The spectral angle coefficient [1] is used to determine the differences between the shapes of two time series.  It determines the angle of difference between the gradients between any two points.  Because it measures the shape of the time series, rather than the magnitude, it is not sensitve to changes in magnitude or timing shifts.  

![Spectral Angle Coefficient](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/SA.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.sa(sim, obs)
```

#### References
+ [1] Robila, S.A.; Gershman, A. In Spectral matching accuracy in processing hyperspectral data, Signals, Circuits and Systems, 2005. ISSCS 2005. International Symposium on, 2005; IEEE: pp 163-166.

hydrostats.sc
-------------

#### class hydrostats.sc(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L367 "Source Code")

#### Spectral Correlation (SC)
Returns the Spectral Correlation [1].

![Spectral Correlation](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/SC.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.sa(sim, obs)
```

#### References
+ [1] Robila, S.A.; Gershman, A. In Spectral matching accuracy in processing hyperspectral data, Signals, Circuits and Systems, 2005. ISSCS 2005. International Symposium on, 2005; IEEE: pp 163-166.

hydrostats.sid
-------------

#### class hydrostats.sid(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### Spectral Information Divergence (SID)
Returns the Spectral Information Divergence.

![Spectral Information Divergence](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/SID.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.sid(sim, obs)
```

hydrostats.sga
-------------

#### class hydrostats.sga(simulated_array, observed_array, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L396 "Source Code")

#### Spectral Gradient Angle (SGA)
Returns the spectral gradient angle.

![Spectral Gradient Angle](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/SGA.PNG?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.sga(sim, obs)
```

# H Metrics - Methods from Tornqvist L, Vartia P, and Vartia YO. (1985)
Tornqvist et al. (1985) argue that the log-difference or log-percent-diffence are the most appropriate measure of relative change because they are semetric and have several other properies. They present 10 different potential measures of change, 9 are included in hydrostats. They use H<sub>1</sub> through H<sub>10</sub> for an error measure. 

For a goodness-of-fit, each of these could be made into a goodness of fit metric. The three goodness of fit metrics used in the paper are shown below:

![H Types](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H_Types.png?raw=true)

hydrostats.h1
-------------

#### class hydrostats.h1(simulated_array, observed_array, h_type='mean', replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H1

![H1](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H1.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'.|
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h1(sim, obs, type='absolute')
```

hydrostats.h2
-------------

#### class hydrostats.h2(simulated_array, observed_array, h_type='mean', replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H2

![H2](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H2.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'.|
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h2(sim, obs, type='absolute')
```

hydrostats.h3
-------------

#### class hydrostats.h3(simulated_array, observed_array, h_type='mean', replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H3

![H3](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H3.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h3(sim, obs, type='absolute')
```

hydrostats.h4
-------------

#### class hydrostats.h4(simulated_array, observed_array, h_type='mean', replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H4

![H4](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H4.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h4(sim, obs, type='absolute')
```

hydrostats.h5
-------------

#### class hydrostats.h5(simulated_array, observed_array, h_type='mean', replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H5

![H5](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H5.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h5(sim, obs, type='absolute')
```

hydrostats.h6
-------------

#### class hydrostats.h6(simulated_array, observed_array, h_type='mean', k=1, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H6

![H6](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H6.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'. |
| k=1              | Integer input indicating the k value. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h6(sim, obs, type='absolute')
```

hydrostats.h7
-------------

#### class hydrostats.h7(simulated_array, observed_array, h_type='mean', replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H7

![H7](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H7.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h7(sim, obs, type='absolute')
```

hydrostats.h8
-------------

#### class hydrostats.h8(simulated_array, observed_array, h_type='mean', replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H8

![H8](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H8.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h8(sim, obs, type='absolute')
```

hydrostats.h10
-------------

#### class hydrostats.h10(simulated_array, observed_array, h_type='mean', replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False)
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L382 "Source Code")

#### H10

![H10](https://github.com/waderoberts123/Hydrostats/blob/master/docs/pictures/H10.png?raw=true)
<p align="left"><b>Where x = observed data and y = simulated data</b></p>

| Parameters       |              |
| :-------------   |:-------------|
| forecasted_array | 1D Numpy array input of forecasted data from the time series.   |
| observed_array   | 1D Numpy array input of observed data from the time series.     |
| h_type='mean'    | Text input indicating the type of metric you want to use on the H values. Possible arguments are 'mean', 'absolute', and 'rmhe'. |
| replace_nan=None | Float input indicating what value to replace NaN values with. |
| replace_inf=None | Float input indicating what value to replace Inf values with. |
| remove_neg=False | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False| Boolean input indicating whether user wants to remove zero values. |

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h10(sim, obs, type='absolute')
```

hydrostats.make_table
---------------------

#### class make_table(merged_dataframe, metrics, seasonal_periods=None, mase_m=1, dmod_j=1, nse_mod_j=1, h6_k=1, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False, to_csv=None, to_excel=None, location=None):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L803 "Source Code")

#### Make Table
Creates a table with metrics as specified by the user. Seasonal periods can also be specified in order to compare different seasons and how well the simulated data matches the observed data. Has options to save the table to either a csv or an excel workbook. Also has an option to add a column for the location of the data.

| Parameters                           |               |
| :------------------------------------|:------------- |
| merged_dataframe (required input) | A pandas dataframe input that has two columns of predicted data and observed data with a datetime index. |
| metrics (required input)          | A list type input that a list of all the metrics that the user wants to calculate. |
| seasonal_periods=None             | A list type input that specifies the seasonal periods that the user wants to analyze (e.g. [['06-01', '06-30'], ['08-12', '11-23']] would analyze the dates from June 1st to June 30th and also August 8th to November 23). Note that the entire time series is analyzed with the selected metrics by default. |
| mase_m=1                          | Parameter for the mean absolute scaled error (mase) metric. |
| dmod_j=1                          | Paremeter for the modified index of agreement (dmod) metric. |
| nse_mod_j=1                       | Parameter for the modified Nash Sutcliffe (nse_mod) metric. |
| h6_k=1                            | Parameter for the H6 (h6) metric. |
| replace_nan=None                  | Float type input indicating if the user wants to fill nan values in the simulated and observed data with another number. |
| replace_inf=None                  | Float type input indicating if the user wants to fill inf values in the simulated and observed data with another number. |
| remove_neg=False                  | Boolean type input indicating if the user wants to remove the negative numbers in the simulated and observed data. |
| remove_zero=False                 | Boolean type input indicating if the user wants to remove the zero values in the simulated and observed data. |
| to_csv=None                       | String type input input with the filepath and file name of the csv that is written (e.g. r'/path/to/output_dir/file.csv'). |
| to_excel=None                     | String type input input with the filepath and file name of the excel workbook that is written (e.g. r'/path/to/output_dir/file.xlsx'). |
| location=None                     | String type input indicating the name of the location that will be created as a column in the dataframe that is created. Useful for creating a large table with different datasets. |

#### List of Metric Names for the metrics Parameter
- Mean Error
- Mean Absolute Error
- Mean Squared Error
- Eclidean Distance
- Normalized Eclidean Distance
- Root Mean Square Error
- Root Mean Squared Log Error
- Mean Absolute Scaled Error
- R^2
- Anomoly Correlation Coefficient
- Mean Absolute Percentage Error
- Mean Absolute Percentage Deviation
- Symmetric Mean Absolute Percentage Error (1)
- Symmetric Mean Absolute Percentage Error (2)
- Index of Agreement (d)
- Index of Agreement (d1)
- Index of Agreement Refined (dr)
- Relative Index of Agreement
- Modified Index of Agreement
- Watterson's M
- Mielke-Berry R
- Nash-Sutcliffe Efficiency
- Modified Nash-Sutcliffe Efficiency
- Relative Nash-Sutcliffe Efficiency
- Legate-McCabe Index
- Spectral Angle
- Spectral Correlation
- Spectral Information Divergence
- Spectral Gradient Angle
- H1 - Mean
- H1 - Absolute
- H1 - Root
- H2 - Mean
- H2 - Absolute
- H2 - Root
- H3 - Mean
- H3 - Absolute
- H3 - Root
- H4 - Mean
- H4 - Absolute
- H4 - Root
- H5 - Mean
- H5 - Absolute
- H5 - Root
- H6 - Mean
- H6 - Absolute
- H6 - Root
- H7 - Mean
- H7 - Absolute
- H7 - Root
- H8 - Mean
- H8 - Absolute
- H8 - Root
- H10 - Mean
- H10 - Absolute
- H10 - Root
- Geometric Mean Difference
- Mean Variance

#### Example

```python
import hydrostats as hs
import numpy as np

sim = np.arange(10)
obs = np.random.rand(10)

hs.h10(sim, obs, type='absolute')
```

hydrostats.time_lag
---------------------

#### class time_lag(merged_dataframe, metric, interp_freq='6H', interp_type='pchip', shift_range=[-30, 30], mase_m=1, dmod_j=1, nse_mod_j=1, h6_k=1, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False, plot_title='Metric Values as Different Lags', ylabel='Metric Value', xlabel='Number of Lags', save_fig=None, figsize=(10, 6)):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/__init__.py#L977 "Source Code")

#### Time Lag Analysis
Runs a time lag analysis to check for potential timing errors in datasets. Returns a dataframe with all of the metric values at different time lags, the maximum and minimum metric value throughout the time lag, and the index of the maximum and minimum time lag values.

| Parameters                           |               |
| :------------------------------------|:------------- |
| merged_dataframe (required input) | A pandas dataframe input that has two columns of predicted data and observed data with a datetime index. |
| metric (required input)           | A string type input with the metric that the user wants to calculate. (See a list of the metric names below). |
| interp_freq='6H'                  | A string type input that specifies the frequency of the interpolation that the user wants.|
| interp_type='pchip'               | Specifies the interpolation method that the user wants to use. (see the documentation for the interpolater used [here](http://pandas.pydata.org/pandas-docs/version/0.16.2/generated/pandas.DataFrame.interpolate.html) for a list of the methods. |
| shift_range=[-30, 30]             | A list of two integer type inputs that specifies the range of the lag analysis, the default is [-30, 30], which will shift the 1st column array through the range of -30 to 30.
| mase_m=1                          | Parameter for the mean absolute scaled error (mase) metric. |
| dmod_j=1                          | Paremeter for the modified index of agreement (dmod) metric. |
| nse_mod_j=1                       | Parameter for the modified Nash Sutcliffe (nse_mod) metric. |
| h6_k=1                            | Parameter for the H6 (h6) metric. |
| replace_nan=None                  | Float type input indicating if the user wants to fill nan values in the simulated and observed data with another number. |
| replace_inf=None                  | Float type input indicating if the user wants to fill inf values in the simulated and observed data with another number. |
| remove_neg=False                  | Boolean type input indicating if the user wants to remove the negative numbers in the simulated and observed data. |
| remove_zero=False                 | Boolean type input indicating if the user wants to remove the zero values in the simulated and observed data. |
| plot_title='Metric Values as Different Lags' | String type input that specifies the title of the plot that is generated.|
| ylabel='Metric Value'             | String type input that specifies the y-axis label of the plot that is generated. |
| xlabel='Number of Lags'           | String type input that specifies the x-axis label of the plot that is generated. |
| save_fig=None                     | String type input indicating the path to the plot that will be saved on the users local machine (e.g. r'/path/to/output_dir/plot.png'). A list of available image types is below. |

#### Available Filetypes with savefig: 
- Postscript (.ps) 
- Encapsulated Postscript (.eps)
- Portable Document Format (.pdf)
- PGF code for LaTeX (.pgf)
- Portable Network Graphics (.png)
- Raw RGBA bitmap (.raw)
- Raw RGBA bitmap (.rgba)
- Scalable Vector Graphics (.svg) 
- Scalable Vector Graphics (.svgz)
- Joint Photographic Experts Group (.jpg, .jpeg)
- Tagged Image File Format (.tif, .tiff)

#### Metric Names for the metric Parameter
- Mean Error
- Mean Absolute Error
- Mean Squared Error
- Eclidean Distance
- Normalized Eclidean Distance
- Root Mean Square Error
- Root Mean Squared Log Error
- Mean Absolute Scaled Error
- R^2
- Anomoly Correlation Coefficient
- Mean Absolute Percentage Error
- Mean Absolute Percentage Deviation
- Symmetric Mean Absolute Percentage Error (1)
- Symmetric Mean Absolute Percentage Error (2)
- Index of Agreement (d)
- Index of Agreement (d1)
- Index of Agreement Refined (dr)
- Relative Index of Agreement
- Modified Index of Agreement
- Watterson's M
- Mielke-Berry R
- Nash-Sutcliffe Efficiency
- Modified Nash-Sutcliffe Efficiency
- Relative Nash-Sutcliffe Efficiency
- Legate-McCabe Index
- Spectral Angle
- Spectral Correlation
- Spectral Information Divergence
- Spectral Gradient Angle
- H1 - Mean
- H1 - Absolute
- H1 - Root
- H2 - Mean
- H2 - Absolute
- H2 - Root
- H3 - Mean
- H3 - Absolute
- H3 - Root
- H4 - Mean
- H4 - Absolute
- H4 - Root
- H5 - Mean
- H5 - Absolute
- H5 - Root
- H6 - Mean
- H6 - Absolute
- H6 - Root
- H7 - Mean
- H7 - Absolute
- H7 - Root
- H8 - Mean
- H8 - Absolute
- H8 - Root
- H10 - Mean
- H10 - Absolute
- H10 - Root
- Geometric Mean Difference
- Mean Variance

# Data Management

hydrostats.data.merge_data
--------------------------

#### class hydrostats.data.merge_data(sim_fpath=None, obs_fpath=None, sim_df=None, obs_df=None, interpolate=None,          column_names=['Simulated', 'Observed'], simulated_tz=None, observed_tz=None, interp_type='pchip'): 
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/data.py#L5 "Source Code")

#### Merge Data 
Takes two csv files that have been formatted with 1 row as a header with date in the first column and
streamflow values in the second column and combines them into a pandas dataframe with datetime type for the
dates and float type for the streamflow value. Please note that the only acceptable time deltas are 15min,
30min, 45min, and any number of hours in between.

There are three scenarios to consider when merging your data:

The first scenario is that the timezones and the spacing of the time series matches (eg. 1 Day). In this case,
you will want to leave the predicted_tz, recorded_tz, and interpolate arguments empty, and the function will
simply join the two csv's into a dataframe.

The second scenario is that you have two time series with matching time zones but not matching spacing. In this
case you will want to leave the predicted_tz and recorded_tz empty, and use the interpolate argument to tell the
function which time series you would like to interpolate to match the other time series.

The third scenario is that you have two time series with different time zones and possibly different spacings.
In this case you will want to fill in the predicted_tz, recorded_tz, and interpolate arguments. This will then
take timezones into account when interpolating the selected time series.

| Parameters       |               |
| :------------------------------------|:------------- |
| sim_fpath=None | A string type input that has the path to the predicted data file. |
| obs_fpath=None | A string type input that has the path to the recorded data file. |
| sim_df=None    | A pandas dataframe type input with one column of simulated data and a datetime type index. |
| obs_df=None    | A pandas dataframe type input with one column of observed data and a datetime type index. |
| interpolate (Default=None)           | A string type input that must be either 'predicted' or 'observed'. If the parameter is set to 'predicted', the predicted values will be interpolated to match up with the recorded values, and vice versa. |
| column_names (Default=['Simulated', 'Observed']) | A list of two string type inputs specifying the column names of the two columns in the dataframe created.|
| simulated_tz (Default=None) | A string type input that lists the time zone of the predicted data. Must be selected from the time zones available (see [List of Available Timezones](#available-timezones) in appendix).|
| observed_tz (Default=None) | A string type input that lists the time zone of the recorded data. Must be selected from the time zones available (see [List of Available Timezones](#available-timezones) in appendix).|

#### Example

```python
import hydrostats.data as hd
import pandas as pd
import numpy as np

sim_freq = '2H'
obs_freq = '45min'
sim_tz = 'Asia/Kathmandu'
obs_tz = 'UTC'

# Seed for reproducibility
np.random.seed(589859043)

sim_index = pd.date_range('2018-01-01', periods=100, freq=sim_freq)
obs_index = pd.date_range('2018-01-01', periods=100, freq=obs_freq)

sim = pd.DataFrame(data=np.random.rand(100), index=sim_index)
obs = pd.DataFrame(data=np.random.rand(100), index=obs_index)

print(hd.merge_data(sim_df=sim, obs_df=obs, interpolate='observed', column_names=['Simulated', 'Observed'],
      simulated_tz=sim_tz, observed_tz=obs_tz, interp_type='pchip'))
```

hydrostats.data.seasonal_period
-------------------------------

#### class hydrostats.data.seasonal_period(merged_dataframe, daily_period, time_range=None, numpy=False): 
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/data.py#L73 "Source Code")

#### Seasonal Period 
The merge data function takes a pandas dataframe with two columns of predicted data and observed data and returns a seasonal period of data based on user input. 

| Parameters                        |              |
| :---------------------------------|:-------------|
| merged_dataframe (Required Input) | A pandas dataframe input that has two columns of predicted data and observed data with a datetime index. |
| daily_period (Required Input)     | A list of strings that contains the seasonal period that the user wants to capture (e.g. ['05-01', '07-01']). |
| time_range (Default=None)         | An optional input of a list of two string type options specifying a date-range for the seasonal period. (e.g. ['1980-01-01', '1987-12-31'])|
| Numpy (Default=False)             | An optional input of boolean type. If specified as true the function will return two numpy arrays rather than a pandas dataframe.|

#### Example

```python
import hydrostats.data as hd
import pandas as pd
import numpy as np

example_df = pd.DataFrame(np.random.rand(1000, 2), index=pd.date_range('1990-01-01', periods=1000), freq='1D')

df_seasonal = hd.seasonal_period(example_df, daily_period=['05-01', '05-04'])

df_seasonal
```

hydrostats.data.daily_average
-----------------------------

#### class hydrostats.data.daily_average(merged_data): 
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/data.py#L22 "Source Code")

#### Daily Average
The daily average function takes a pandas dataframe and calculates daily averages of the time series. If the frequency of the time series is not daily, then it will still take the daily averages of all of the values that day.  

| Parameters       |               |
| :-------------   |:-------------|
| merged_data (Required Input) | A pandas dataframe input that has two columns of predicted data and observed data with a datetime index. |

#### Example

```python
import hydrostats.data as hd
import pandas as pd
import numpy as np

example_df = pd.DataFrame(np.random.rand(1000, 2), index=pd.date_range('1990-01-01', periods=1000), freq='1D')

df_daily_avg = hd.daily_average(example_df)

df_seasonal
```

hydrostats.data.daily_std_error
-------------------------------

#### class hydrostats.data.daily_std_error(merged_data):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/data.py#L240 "Source Code")

#### Daily Standard Error
The daily standard error function takes a pandas dataframe and calculates daily standard error of the time series. If the frequency of the time series is not daily, then it will still take the daily standard error of all of the values that day.  

| Parameters       |               |
| :-------------   |:-------------|
| merged_data (Required Input) | A pandas dataframe input that has two columns of predicted data and observed data with a datetime index. |

#### Example

```python
import hydrostats.data as hd
import pandas as pd
import numpy as np

# Seed for reproducibility
np.random.seed(589859043)

example_df = pd.DataFrame(np.random.rand(1000, 2), index=pd.date_range('1990-01-01', periods=1000, freq='1D'),
                          columns=['Simulated', 'Observed'])

df_standard_error = hd.daily_std_error(example_df)

print(df_standard_error)
```

hydrostats.data.monthly_average
-------------------------------

#### class hydrostats.data.monthly_average(merged_data):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/data.py#L250 "Source Code")

#### Monthly Average
The monthly average function takes a pandas dataframe and calculates monthly averages of the time series.  

| Parameters       |               |
| :-------------   |:-------------|
| merged_data (Required Input) | A pandas dataframe input that has two columns of predicted data and observed data with a datetime index. |

#### Example

```python
import hydrostats.data as hd
import pandas as pd
import numpy as np

# Seed for reproducibility
np.random.seed(589859043)

example_df = pd.DataFrame(np.random.rand(1000, 2), index=pd.date_range('1990-01-01', periods=1000, freq='1D'),
                          columns=['Simulated', 'Observed'])

df_monthly_avg = hd.monthly_average(example_df)

print(df_monthly_avg)
```

hydrostats.data.monthly_std_error
---------------------------------

#### class hydrostats.data.monthly_std_error(merged_data):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/data.py#L260 "Source Code")

#### Monthly Standard Error
The monthly standard error function takes a pandas dataframe and calculates monthly standard error of the time series.

| Parameters       |               |
| :-------------   |:-------------|
| merged_data (Required Input) | A pandas dataframe input that has two columns of predicted data and observed data with a datetime index. |

#### Example

```python
import hydrostats.data as hd
import pandas as pd
import numpy as np

# Seed for reproducibility
np.random.seed(589859043)

example_df = pd.DataFrame(np.random.rand(1000, 2), index=pd.date_range('1990-01-01', periods=1000, freq='1D'),
                          columns=['Simulated', 'Observed'])

df_monthly_std_error = hd.monthly_average(example_df)

print(df_monthly_std_error)
```

# Visualization

hydrostats.visual.plot
----------------------

#### class hydrostats.visual.plot(merged_data_df, legend=None, metrics=None, grid=False, title=None, x_season=False, labels=None, savefigure=None, linestyles=['ro', 'b^'], tight_xlim=False, fig_size=(10, 6), text_adjust=[-0.35, 0.75], plot_adjust=0.27, transparency=0.5, ebars=None, ecolor=None, markersize=2, errorevery=1, markevery=1):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/visual.py#L10 "Source Code")

#### Time Series Plot
The time series plot is a function that is available for viewing two times series plotted side by side vs. time. Goodness of fit metrics can also be viewed on the plot to compare the two time series.  

<br>

| Parameters       |               |
| :---------------------------------   |:-------------|
| merged_data_df (Required Input)      | A dataframe with a datetime type index and floating point type numbers in the two columns. The columns must be simulated Data and observed Data going from left to right. |
| legend (Default=None)                | Adds a Legend in the 'best' location determined by matplotlib. The entries must be in the form of a list. (e.g. ['Simulated Data', 'Predicted Data']|
| metrics (Default=None)               | Adds Metrics to the left side of the Plot. Any Metric from the Hydrostats Library can be added to the plot as the name of the function. The entries must be in a list. (e.g. |['ME', 'MASE'] would plot the Mean Error and the Mean Absolute Scaled Error on the left side of the plot.| 
| grid (Default=False)                 | Takes a boolean type input and adds a grid to the plot. |
| title (Default=None)                 | Takes a string type input and adds a title to the hydrograph. |
| x_season (Default=None)              | Takes a boolean type input. If True, the x-axis ticks will be staggered every 20 ticks. This is a useful feature when plotting daily averages. |
| labels (Default=None)                | Takes a list of two string type objects and adds them as x-axis labels and y-axis labels, respectively.|
| savefigure (Default=None)            | Takes a string type input and will save the plot the the specified path as a filetype specified by the user. (eg. path/to/file.png) | 
| linestyles (Default=['ro', 'b^'])    | Takes a list of two string type inputs and will change the linestyle of the predicted and recorded data, respectively (see below for a guide to linestyles). |
| tight_xlim (Default=False)           | Takes a boolean type input indicating of a tight xlim is desired. |
| fig_size=(10, 6)                     | Takes a tuple type input indicating the size of the figure created. |
| text_adjust=[-0.35, 0.75]            | Takes a list type input indicating the relative position of the text [x-coordinate, y-coordinate]. |
| plot_adjust=0.27                     | Take a float type input specifying the relative position to shift the plot the the right when adding metrics to the plot. |
| transparency=0.5                     | Float type input from 0 to 1 indicating the transparency of the two lines that are plotted and error bars if they are plotted. |
| ebars=None                           | Pandas dataframe type with a datetime index and two columns of data that specify the error of the plots. These dataframes can be created with the following hydrostats functions hydrostats.data.daily_std_error, hydrostats.data.daily_std_dev, hydrostats.data.monthly_std_error, hydrostats.data.monthly_std_dev. |
| ecolor=None                          | List of two sting type inputs specifying the colors of the errorbars (e.g. ['r', 'k'] would make red and black errorbars on the simulated and observed data, respectively. |
| markersize=2                         | Float type input indicating the size of the markers on the plot, if markers are used. |
| errorevery=1                         | Integer type input specifying how often to put error bars on the plot. |
| markevery=1                          | Integer type input specifying how often to put markers on the plot if markers are used. |

#### Available metrics to add to the left side of the plot:
- ME (Mean Error)
- MAE (Mean Absolute Error)
- MSE (Mean Squared Error)
- ED (Eclidean Distance)
- NED (Normalized Eclidean Distance)
- RMSE (Root Mean Square Error)
- RMSLE (Root Mean Squared Log Error)
- MASE (Mean Absolute Scaled Error)
- R^2 (Coefficient of Determination)
- ACC (Anomoly Correlation Coefficient)
- MAPE (Mean Absolute Percentage Error)
- MAPD (Mean Absolute Percentage Deviation)
- SMAP1 (Symmetric Mean Absolute Percentage Error (1))
- SMAP2 (Symmetric Mean Absolute Percentage Error (2))
- D (Index of Agreement (d))
- D1 (Index of Agreement (d1))
- DR (Index of Agreement Refined (dr))
- D-Rel (Relative Index of Agreement)
- D-Mod (Modified Index of Agreement)
- M (Watterson's M)
- R (Mielke-Berry R)
- E (Nash-Sutcliffe Efficiency)
- E-Mod (Modified Nash-Sutcliffe Efficiency)
- E-Rel (Relative Nash-Sutcliffe Efficiency)
- E_1 (Legate-McCabe Index)
- SA (Spectral Angle)
- SC (Spectral Correlation)
- SID (Spectral Information Divergence)
- SGA (Spectral Gradient Angle)

#### Available linestyle options in matplotlib documentation (can be combined e.g. 'r-' is a red solid line, 'r^' is red triangle up markers)
- [Colors](https://matplotlib.org/2.0.2/api/colors_api.html#colors)
- [Linestyles](https://matplotlib.org/gallery/lines_bars_and_markers/line_styles_reference.html#line-style-reference)
- [Marker Styles](https://matplotlib.org/api/markers_api.html#markers)

#### Available Filetypes with savefig: 
- Postscript (.ps) 
- Encapsulated Postscript (.eps)
- Portable Document Format (.pdf)
- PGF code for LaTeX (.pgf)
- Portable Network Graphics (.png)
- Raw RGBA bitmap (.raw)
- Raw RGBA bitmap (.rgba)
- Scalable Vector Graphics (.svg) 
- Scalable Vector Graphics (.svgz)
- Joint Photographic Experts Group (.jpg, .jpeg)
- Tagged Image File Format (.tif, .tiff)

#### Example

```python
import hydrostats.visual as hv
import hydrostats.data as hd
import numpy as np
import pandas as pd

# Seed for reproducibility
np.random.seed(7850493)

random_noise = (np.random.rand(10000) - 0.5) / 10 + 1

# Creting synthetic simulated and observed data
sim = np.sin(np.linspace(0, 5*np.pi, 10000)) * random_noise + 20
obs = np.sin(np.linspace(0, 5*np.pi, 10000)) + 20

time_index = pd.date_range('1980-01-01', periods=10000)
df = pd.DataFrame(np.column_stack((sim, obs)), index=time_index, columns=['Synthetic Simulated Data', 'Synthetic Observed Data'])

# Plotting a ~28 yr time series
hv.plot(df, linestyles=['k-', 'r--'], title='28 Year Timeseries of Sin Curves', labels=['Datetime', 'Sin Values'],
        legend=['Synthetic Simulated Data', 'Synthetic Observed Data'], metrics=['ME', 'R^2', 'NSE'], text_adjust=[-0.3, 0.80])

# Now I can find daily averages and plot them, notice the x_seasonal argument was used to avoid cramped x ticks
df = hd.daily_average(df)

hv.plot(df, linestyles=['k-', 'r--'], title='Daily Averages of Sin Curves', labels=['Datetime', 'Sin Values'],
        legend=['Synthetic Simulated Data', 'Synthetic Observed Data'], metrics=['ME', 'R^2', 'NSE'], text_adjust=[-0.3, 0.80], x_season=True)

# Now I can save the plot I like (Daily Averages) with savefig argument
hv.plot(df, linestyles=['k-', 'r--'], title='Daily Averages of Sin Curves', labels=['Datetime', 'Sin Values'],
        legend=['Synthetic Simulated Data', 'Synthetic Observed Data'], metrics=['ME', 'R^2', 'NSE'], text_adjust=[-0.3, 0.80], x_season=True, savefigure='Daily_Averages.png')
```

hydrostats.visual.hist
----------------------

#### class hydrostats.visual.hist(merged_data_df=None, sim_array=None, obs_array=None, num_bins=100, z_norm=False, legend=None, grid=False, title=None, labels=None, savefigure=None, prob_dens=False, figsize=(12, 6)):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/visual.py#L112 "Source Code")

#### Histogram Plot
The histogram plot is a function that is available for comparing the histogram of two time series. Data can be Z-score normalized as well as fit in a probability density function.  

<br>

| Parameters       |               |
| :---------------------------------   |:-------------|
| merged_data_df=None                  | A dataframe with a datetime type index and floating point type numbers in the two columns. The columns must be simulated Data and observed Data going from left to right. |
| sim_array=None                       | An numpy 1D array of simulated data. If this argument is selected then the obs_array parameter must also be provided. |
| obs_array=None                       | An numpy 1D array of observed data. If this argument is selected then the sim_array parameter must also be provided. |
| num_bins (Required Input)            | An interger type input specifying the number of bins in the histogram. |
| z_norm=False                         | A boolean type input specifying if the user wants to Z-score normalize the data. |
| legend (Default=None)                | Adds a Legend in the 'best' location determined by matplotlib. The entries must be in the form of a list. (e.g. ['Simulated Data', 'Predicted Data']|
| grid (Default=False)                 | Takes a boolean type input and adds a grid to the plot. |
| title (Default=None)                 | Takes a string type input and adds a title to the hydrograph. |
| labels (Default=None)                | Takes a list of two string type objects and adds them as x-axis labels and y-axis labels, respectively.|
| savefigure (Default=None)            | Takes a string type input and will save the plot the the specified path as a filetype specified by the user. (eg. path/to/file.png) | 
| prob_dens=False                      | Takes a boolean type input. If True, the first element of the return tuple will be the counts normalized to form a probability density, i.e., the area (or integral) under the histogram will sum to 1. |
| figsize=(12, 6)                      | A list of tuples specifying the size of the figure in inches. |

#### Available Filetypes with savefig: 
- Postscript (.ps) 
- Encapsulated Postscript (.eps)
- Portable Document Format (.pdf)
- PGF code for LaTeX (.pgf)
- Portable Network Graphics (.png)
- Raw RGBA bitmap (.raw)
- Raw RGBA bitmap (.rgba)
- Scalable Vector Graphics (.svg) 
- Scalable Vector Graphics (.svgz)
- Joint Photographic Experts Group (.jpg, .jpeg)
- Tagged Image File Format (.tif, .tiff)

#### Example

```python
import hydrostats.visual as hv
import numpy as np
import pandas as pd

# Seed for reproducibility
np.random.seed(7850493)

random_noise = (np.random.rand(10000) - 0.5) / 10 + 1

# Creting synthetic simulated and observed data
sim = np.sin(np.linspace(0, 5*np.pi, 10000)) * random_noise + 20
obs = np.sin(np.linspace(0, 5*np.pi, 10000)) + 20

time_index = pd.date_range('1980-01-01', periods=10000)
df = pd.DataFrame(np.column_stack((sim, obs)), index=time_index, columns=['Synthetic Simulated Data', 'Synthetic Observed Data'])

# Plotting histograms for the ~28 yr time series
hv.hist(df, num_bins=100, title='28 Year Histograms of Sin Curves', labels=['Bins', 'Frequency'],
        legend=['Synthetic Simulated Data', 'Synthetic Observed Data'])

# Now I can check for outliers by normalizing the data into Z-scores
hv.hist(df, num_bins=100, title='28 Year Histograms of Sin Curves (Z-Score Normalized)', labels=['Bins', 'Frequency'],
        legend=['Synthetic Simulated Data', 'Synthetic Observed Data'], z_norm=True)

# Now I can save the first plot with the savefig argument
hv.hist(df, num_bins=100, title='28 Year Histograms of Sin Curves (Z-Score Normalized)', labels=['Bins', 'Frequency'],
        legend=['Synthetic Simulated Data', 'Synthetic Observed Data'], savefigure='Histogram.png')
```

hydrostats.visual.scatter
----------------------

#### class hydrostats.visual.scatter(merged_data_df=None, sim_array=None, obs_array=None, grid=False, title=None, labels=None, best_fit=False, savefigure=None, marker_style='ko', metrics=None, log_scale=False, line45=False, figsize=(12, 8)):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/visual.py#L202 "Source Code")

#### Scatter Plot
The scatter plot is a function that is available for comparing the correlation of two datasets. Metrics can be added to the plot, as well as the use of a Log-Log scale for large time-series.  

<br>

| Parameters       |               |
| :---------------------------------   |:-------------|
| merged_data_df=None                  | A dataframe with a datetime type index and floating point type numbers in the two columns. The columns must be simulated Data and observed Data going from left to right. |
| sim_array=None                       | An numpy 1D array of simulated data. If this argument is selected then the obs_array parameter must also be provided. |
| obs_array=None                       | An numpy 1D array of observed data. If this argument is selected then the sim_array parameter must also be provided. |
| grid (Default=False)                 | Takes a boolean type input and adds a grid to the plot. |
| title (Default=None)                 | Takes a string type input and adds a title to the hydrograph. |
| labels (Default=None)                | Takes a list of two string type objects and adds them as x-axis labels and y-axis labels, respectively.|
| best_fit=False                       | Boolean type input indicating if the user wants a best linear regression line on the graph with the equation for the line in the legend. |
| savefigure (Default=None)            | Takes a string type input and will save the plot the the specified path as a filetype specified by the user. (eg. path/to/file.png) | 
| marker_style='ko'                    | Takes a string type input and will change the markerstyle of the points on the scatter plot. |
| metrics (Default=None)               | Adds Metrics to the left side of the Plot. Any Metric from the Hydrostats Library can be added to the plot as the name of the function. The entries must be in a list. (e.g. ['ME', 'MASE'] would plot the Mean Error and the Mean Absolute Scaled Error on the left side of the plot.| 
| log_scale=False                      | Boolean type input indicating whether or not to use a log-log scale on the scatter plot. | 
| line45=False                         | Boolean type input indicating whether or not to add a line with a slope of 1 to the plot. |
| figsize=(12, 8)                      | List of tuples specifying the size of the plot in inches. | 

#### Available metrics to add to the left side of the plot:
- ME (Mean Error)
- MAE (Mean Absolute Error)
- MSE (Mean Squared Error)
- ED (Eclidean Distance)
- NED (Normalized Eclidean Distance)
- RMSE (Root Mean Square Error)
- RMSLE (Root Mean Squared Log Error)
- MASE (Mean Absolute Scaled Error)
- R^2 (Coefficient of Determination)
- ACC (Anomoly Correlation Coefficient)
- MAPE (Mean Absolute Percentage Error)
- MAPD (Mean Absolute Percentage Deviation)
- SMAP1 (Symmetric Mean Absolute Percentage Error (1))
- SMAP2 (Symmetric Mean Absolute Percentage Error (2))
- D (Index of Agreement (d))
- D1 (Index of Agreement (d1))
- DR (Index of Agreement Refined (dr))
- D-Rel (Relative Index of Agreement)
- D-Mod (Modified Index of Agreement)
- M (Watterson's M)
- R (Mielke-Berry R)
- E (Nash-Sutcliffe Efficiency)
- E-Mod (Modified Nash-Sutcliffe Efficiency)
- E-Rel (Relative Nash-Sutcliffe Efficiency)
- E_1 (Legate-McCabe Index)
- SA (Spectral Angle)
- SC (Spectral Correlation)
- SID (Spectral Information Divergence)
- SGA (Spectral Gradient Angle)

#### Available Filetypes with savefig: 
- Postscript (.ps) 
- Encapsulated Postscript (.eps)
- Portable Document Format (.pdf)
- PGF code for LaTeX (.pgf)
- Portable Network Graphics (.png)
- Raw RGBA bitmap (.raw)
- Raw RGBA bitmap (.rgba)
- Scalable Vector Graphics (.svg) 
- Scalable Vector Graphics (.svgz)
- Joint Photographic Experts Group (.jpg, .jpeg)
- Tagged Image File Format (.tif, .tiff)

#### Example

```python
import hydrostats.visual as hv
import numpy as np
import pandas as pd

# Seed for reproducibility
np.random.seed(7850493)

random_noise = (np.random.rand(10000) - 0.5) / 10 + 1

# Creting synthetic simulated and observed data
sim = np.sin(np.linspace(0, 5*np.pi, 10000)) * random_noise + 1
obs = np.sin(np.linspace(0, 5*np.pi, 10000)) + 1

time_index = pd.date_range('1980-01-01', periods=10000)
df = pd.DataFrame(np.column_stack((sim, obs)), index=time_index, columns=['Synthetic Simulated Data', 'Synthetic Observed Data'])

# Plotting a scatter plot for the ~28 yr time series
hv.scatter(df, title='Scatter Plot for the Synthetic Data',
           labels=['Synthetic Simulated Data', 'Synthetic Observed Data'], marker_style='bP',
           metrics=['R^2'], line45=True)

# Plotting with a log-log scale
hv.scatter(df, title='Scatter Plot for the Synthetic Data (Log-Log Scale)',
           labels=['Synthetic Simulated Data', 'Synthetic Observed Data'], marker_style='bP',
           metrics=['R^2'], log_scale=True)

# Now I can save the second plot with the savefig argument
hv.scatter(df, title='Scatter Plot for the Synthetic Data (Log-Log Scale)',
           labels=['Synthetic Simulated Data', 'Synthetic Observed Data'], marker_style='bP',
           metrics=['R^2'], log_scale=True, savefigure='Scatter.png')
```

hydrostats.visual.qqplot
----------------------

#### class hydrostats.visual.qqplot(merged_data_df=None, sim_array=None, obs_array=None, interpolate='linear', title=None, xlabel='Simulated Data Quantiles', ylabel='Observed Data Quantiles', legend=False, replace_nan=None, replace_inf=None, remove_neg=False, remove_zero=False, figsize=(12, 8), savefigure=None):
[source](https://github.com/waderoberts123/Hydrostats/blob/master/hydrostats/visual.py#L202 "Source Code")

#### QQ (Quantile Quantile Plot)
The QQ plot is a function that is available for comparing the distribution of two datasets. When data falls along a linear regression line, it indicates that the data comes from the same distribution. The function will plot the quantiles along a line that is linear to the ends of the interquartile range of the two plots (Q1 and Q3).

<br>

| Parameters       |                   |
| :---------------------------------   |:-------------|
| merged_data_df=None                  | A dataframe with a datetime type index and floating point type numbers in the two columns. The columns must be simulated Data and observed Data going from left to right. |
| sim_array=None                       | An numpy 1D array of simulated data. If this argument is selected then the obs_array parameter must also be provided. |
| obs_array=None                       | An numpy 1D array of observed data. If this argument is selected then the sim_array parameter must also be provided. |
| interpolate='linear'                 | A string type input specifying the interpolation type when computing quantiles. The default is linear. |
| title=None                           | A string type input that specifies the title of the QQ Plot. |
| xlabel='Simulated Data Quantiles'    | The label for the x axis that holds the simulated data quantiles. |
| ylabel='Observed Data Quantiles'     | The label for the y axis that holds the observed data quantiles. |
| legend=False                         | Boolean type input specifying whether the user wants to add a legend to explain the elements on the chart. | 
| replace_nan=None                     | Float input indicating what value to replace NaN values with. |
| replace_inf=None                     | Float input indicating what value to replace Inf values with. |
| remove_neg=False                     | Boolean input indicating whether user wants to remove negative numbers. |
| remove_zero=False                    | Boolean input indicating whether user wants to remove zero values. |
| figsize=(12, 8)                      | Takes a list of 2 tuples specifying the size of the figure in inches. |
| savefigure=None                      | Takes a string type input and will save the plot the the specified path as a filetype specified by the user. (eg. path/to/file.png) | 

#### Available Filetypes with savefig: 
- Postscript (.ps) 
- Encapsulated Postscript (.eps)
- Portable Document Format (.pdf)
- PGF code for LaTeX (.pgf)
- Portable Network Graphics (.png)
- Raw RGBA bitmap (.raw)
- Raw RGBA bitmap (.rgba)
- Scalable Vector Graphics (.svg) 
- Scalable Vector Graphics (.svgz)
- Joint Photographic Experts Group (.jpg, .jpeg)
- Tagged Image File Format (.tif, .tiff)

#### Example

```python
import hydrostats.visual as hv
import numpy as np
import pandas as pd

# Seed for reproducibility
np.random.seed(7850493)

random_noise = (np.random.rand(100) - 0.5) / 5 + 1

# Creting synthetic simulated and observed data
sim = np.sin(np.linspace(0, 5*np.pi, 100)) * random_noise + 20
obs = np.sin(np.linspace(0, 5*np.pi, 100)) + 20

time_index = pd.date_range('1980-01-01', periods=100)
df = pd.DataFrame(np.column_stack((sim, obs)), index=time_index, columns=['Synthetic Simulated Data', 'Synthetic Observed Data'])

# Plotting a QQ Plot for the time series
hv.qqplot(df, legend=True, title='QQ Plot', interpolate='midpoint')

# Saving the figure with savefig argument
hv.qqplot(df, legend=True, title='QQ Plot', interpolate='midpoint', savefig='QQ_Plot.png')
```

# Appendix

## Available Timezones

+ Africa/Abidjan (+00:00)
+ Africa/Accra (+00:00)
+ Africa/Addis_Ababa (+03:00)
+ Africa/Algiers (+01:00)
+ Africa/Asmara (+03:00)
+ Africa/Asmera (+03:00)
+ Africa/Bamako (+00:00)
+ Africa/Bangui (+01:00)
+ Africa/Banjul (+00:00)
+ Africa/Bissau (+00:00)
+ Africa/Blantyre (+02:00)
+ Africa/Brazzaville (+01:00)
+ Africa/Bujumbura (+02:00)
+ Africa/Cairo (+02:00)
+ Africa/Casablanca (+00:00)
+ Africa/Ceuta (+01:00)
+ Africa/Conakry (+00:00)
+ Africa/Dakar (+00:00)
+ Africa/Dar_es_Salaam (+03:00)
+ Africa/Djibouti (+03:00)
+ Africa/Douala (+01:00)
+ Africa/El_Aaiun (+00:00)
+ Africa/Freetown (+00:00)
+ Africa/Gaborone (+02:00)
+ Africa/Harare (+02:00)
+ Africa/Johannesburg (+02:00)
+ Africa/Juba (+03:00)
+ Africa/Kampala (+03:00)
+ Africa/Khartoum (+02:00)
+ Africa/Kigali (+02:00)
+ Africa/Kinshasa (+01:00)
+ Africa/Lagos (+01:00)
+ Africa/Libreville (+01:00)
+ Africa/Lome (+00:00)
+ Africa/Luanda (+01:00)
+ Africa/Lubumbashi (+02:00)
+ Africa/Lusaka (+02:00)
+ Africa/Malabo (+01:00)
+ Africa/Maputo (+02:00)
+ Africa/Maseru (+02:00)
+ Africa/Mbabane (+02:00)
+ Africa/Mogadishu (+03:00)
+ Africa/Monrovia (+00:00)
+ Africa/Nairobi (+03:00)
+ Africa/Ndjamena (+01:00)
+ Africa/Niamey (+01:00)
+ Africa/Nouakchott (+00:00)
+ Africa/Ouagadougou (+00:00)
+ Africa/Porto-Novo (+01:00)
+ Africa/Sao_Tome (+00:00)
+ Africa/Timbuktu (+00:00)
+ Africa/Tripoli (+02:00)
+ Africa/Tunis (+01:00)
+ Africa/Windhoek (+02:00)
+ America/Adak (-10:00)
+ America/Anchorage (-09:00)
+ America/Anguilla (-04:00)
+ America/Antigua (-04:00)
+ America/Araguaina (-03:00)
+ America/Argentina/Buenos_Aires (-03:00)
+ America/Argentina/Catamarca (-03:00)
+ America/Argentina/ComodRivadavia (-03:00)
+ America/Argentina/Cordoba (-03:00)
+ America/Argentina/Jujuy (-03:00)
+ America/Argentina/La_Rioja (-03:00)
+ America/Argentina/Mendoza (-03:00)
+ America/Argentina/Rio_Gallegos (-03:00)
+ America/Argentina/Salta (-03:00)
+ America/Argentina/San_Juan (-03:00)
+ America/Argentina/San_Luis (-03:00)
+ America/Argentina/Tucuman (-03:00)
+ America/Argentina/Ushuaia (-03:00)
+ America/Aruba (-04:00)
+ America/Asuncion (-03:00)
+ America/Atikokan (-05:00)
+ America/Atka (-10:00)
+ America/Bahia (-03:00)
+ America/Bahia_Banderas (-06:00)
+ America/Barbados (-04:00)
+ America/Belem (-03:00)
+ America/Belize (-06:00)
+ America/Blanc-Sablon (-04:00)
+ America/Boa_Vista (-04:00)
+ America/Bogota (-05:00)
+ America/Boise (-07:00)
+ America/Buenos_Aires (-03:00)
+ America/Cambridge_Bay (-07:00)
+ America/Campo_Grande (-03:00)
+ America/Cancun (-05:00)
+ America/Caracas (-04:00)
+ America/Catamarca (-03:00)
+ America/Cayenne (-03:00)
+ America/Cayman (-05:00)
+ America/Chicago (-06:00)
+ America/Chihuahua (-07:00)
+ America/Coral_Harbour (-05:00)
+ America/Cordoba (-03:00)
+ America/Costa_Rica (-06:00)
+ America/Creston (-07:00)
+ America/Cuiaba (-03:00)
+ America/Curacao (-04:00)
+ America/Danmarkshavn (+00:00)
+ America/Dawson (-08:00)
+ America/Dawson_Creek (-07:00)
+ America/Denver (-07:00)
+ America/Detroit (-05:00)
+ America/Dominica (-04:00)
+ America/Edmonton (-07:00)
+ America/Eirunepe (-05:00)
+ America/El_Salvador (-06:00)
+ America/Ensenada (-08:00)
+ America/Fort_Nelson (-07:00)
+ America/Fort_Wayne (-05:00)
+ America/Fortaleza (-03:00)
+ America/Glace_Bay (-04:00)
+ America/Godthab (-03:00)
+ America/Goose_Bay (-04:00)
+ America/Grand_Turk (-04:00)
+ America/Grenada (-04:00)
+ America/Guadeloupe (-04:00)
+ America/Guatemala (-06:00)
+ America/Guayaquil (-05:00)
+ America/Guyana (-04:00)
+ America/Halifax (-04:00)
+ America/Havana (-05:00)
+ America/Hermosillo (-07:00)
+ America/Indiana/Indianapolis (-05:00)
+ America/Indiana/Knox (-06:00)
+ America/Indiana/Marengo (-05:00)
+ America/Indiana/Petersburg (-05:00)
+ America/Indiana/Tell_City (-06:00)
+ America/Indiana/Vevay (-05:00)
+ America/Indiana/Vincennes (-05:00)
+ America/Indiana/Winamac (-05:00)
+ America/Indianapolis (-05:00)
+ America/Inuvik (-07:00)
+ America/Iqaluit (-05:00)
+ America/Jamaica (-05:00)
+ America/Jujuy (-03:00)
+ America/Juneau (-09:00)
+ America/Kentucky/Louisville (-05:00)
+ America/Kentucky/Monticello (-05:00)
+ America/Knox_IN (-06:00)
+ America/Kralendijk (-04:00)
+ America/La_Paz (-04:00)
+ America/Lima (-05:00)
+ America/Los_Angeles (-08:00)
+ America/Louisville (-05:00)
+ America/Lower_Princes (-04:00)
+ America/Maceio (-03:00)
+ America/Managua (-06:00)
+ America/Manaus (-04:00)
+ America/Marigot (-04:00)
+ America/Martinique (-04:00)
+ America/Matamoros (-06:00)
+ America/Mazatlan (-07:00)
+ America/Mendoza (-03:00)
+ America/Menominee (-06:00)
+ America/Merida (-06:00)
+ America/Metlakatla (-09:00)
+ America/Mexico_City (-06:00)
+ America/Miquelon (-03:00)
+ America/Moncton (-04:00)
+ America/Monterrey (-06:00)
+ America/Montevideo (-03:00)
+ America/Montreal (-05:00)
+ America/Montserrat (-04:00)
+ America/Nassau (-05:00)
+ America/New_York (-05:00)
+ America/Nipigon (-05:00)
+ America/Nome (-09:00)
+ America/Noronha (-02:00)
+ America/North_Dakota/Beulah (-06:00)
+ America/North_Dakota/Center (-06:00)
+ America/North_Dakota/New_Salem (-06:00)
+ America/Ojinaga (-07:00)
+ America/Panama (-05:00)
+ America/Pangnirtung (-05:00)
+ America/Paramaribo (-03:00)
+ America/Phoenix (-07:00)
+ America/Port-au-Prince (-05:00)
+ America/Port_of_Spain (-04:00)
+ America/Porto_Acre (-05:00)
+ America/Porto_Velho (-04:00)
+ America/Puerto_Rico (-04:00)
+ America/Punta_Arenas (-03:00)
+ America/Rainy_River (-06:00)
+ America/Rankin_Inlet (-06:00)
+ America/Recife (-03:00)
+ America/Regina (-06:00)
+ America/Resolute (-06:00)
+ America/Rio_Branco (-05:00)
+ America/Rosario (-03:00)
+ America/Santa_Isabel (-08:00)
+ America/Santarem (-03:00)
+ America/Santiago (-03:00)
+ America/Santo_Domingo (-04:00)
+ America/Sao_Paulo (-02:00)
+ America/Scoresbysund (-01:00)
+ America/Shiprock (-07:00)
+ America/Sitka (-09:00)
+ America/St_Barthelemy (-04:00)
+ America/St_Johns (-03:30)
+ America/St_Kitts (-04:00)
+ America/St_Lucia (-04:00)
+ America/St_Thomas (-04:00)
+ America/St_Vincent (-04:00)
+ America/Swift_Current (-06:00)
+ America/Tegucigalpa (-06:00)
+ America/Thule (-04:00)
+ America/Thunder_Bay (-05:00)
+ America/Tijuana (-08:00)
+ America/Toronto (-05:00)
+ America/Tortola (-04:00)
+ America/Vancouver (-08:00)
+ America/Virgin (-04:00)
+ America/Whitehorse (-08:00)
+ America/Winnipeg (-06:00)
+ America/Yakutat (-09:00)
+ America/Yellowknife (-07:00)
+ Antarctica/Casey (+11:00)
+ Antarctica/Davis (+07:00)
+ Antarctica/DumontDUrville (+10:00)
+ Antarctica/Macquarie (+11:00)
+ Antarctica/Mawson (+05:00)
+ Antarctica/McMurdo (+13:00)
+ Antarctica/Palmer (-03:00)
+ Antarctica/Rothera (-03:00)
+ Antarctica/South_Pole (+13:00)
+ Antarctica/Syowa (+03:00)
+ Antarctica/Troll (+00:00)
+ Antarctica/Vostok (+06:00)
+ Arctic/Longyearbyen (+01:00)
+ Asia/Aden (+03:00)
+ Asia/Almaty (+06:00)
+ Asia/Amman (+02:00)
+ Asia/Anadyr (+12:00)
+ Asia/Aqtau (+05:00)
+ Asia/Aqtobe (+05:00)
+ Asia/Ashgabat (+05:00)
+ Asia/Ashkhabad (+05:00)
+ Asia/Atyrau (+05:00)
+ Asia/Baghdad (+03:00)
+ Asia/Bahrain (+03:00)
+ Asia/Baku (+04:00)
+ Asia/Bangkok (+07:00)
+ Asia/Barnaul (+07:00)
+ Asia/Beirut (+02:00)
+ Asia/Bishkek (+06:00)
+ Asia/Brunei (+08:00)
+ Asia/Calcutta (+05:30)
+ Asia/Chita (+09:00)
+ Asia/Choibalsan (+08:00)
+ Asia/Chongqing (+08:00)
+ Asia/Chungking (+08:00)
+ Asia/Colombo (+05:30)
+ Asia/Dacca (+06:00)
+ Asia/Damascus (+02:00)
+ Asia/Dhaka (+06:00)
+ Asia/Dili (+09:00)
+ Asia/Dubai (+04:00)
+ Asia/Dushanbe (+05:00)
+ Asia/Famagusta (+02:00)
+ Asia/Gaza (+02:00)
+ Asia/Harbin (+08:00)
+ Asia/Hebron (+02:00)
+ Asia/Ho_Chi_Minh (+07:00)
+ Asia/Hong_Kong (+08:00)
+ Asia/Hovd (+07:00)
+ Asia/Irkutsk (+08:00)
+ Asia/Istanbul (+03:00)
+ Asia/Jakarta (+07:00)
+ Asia/Jayapura (+09:00)
+ Asia/Jerusalem (+02:00)
+ Asia/Kabul (+04:30)
+ Asia/Kamchatka (+12:00)
+ Asia/Karachi (+05:00)
+ Asia/Kashgar (+06:00)
+ Asia/Kathmandu (+05:45)
+ Asia/Katmandu (+05:45)
+ Asia/Khandyga (+09:00)
+ Asia/Kolkata (+05:30)
+ Asia/Krasnoyarsk (+07:00)
+ Asia/Kuala_Lumpur (+08:00)
+ Asia/Kuching (+08:00)
+ Asia/Kuwait (+03:00)
+ Asia/Macao (+08:00)
+ Asia/Macau (+08:00)
+ Asia/Magadan (+11:00)
+ Asia/Makassar (+08:00)
+ Asia/Manila (+08:00)
+ Asia/Muscat (+04:00)
+ Asia/Nicosia (+02:00)
+ Asia/Novokuznetsk (+07:00)
+ Asia/Novosibirsk (+07:00)
+ Asia/Omsk (+06:00)
+ Asia/Oral (+05:00)
+ Asia/Phnom_Penh (+07:00)
+ Asia/Pontianak (+07:00)
+ Asia/Pyongyang (+08:30)
+ Asia/Qatar (+03:00)
+ Asia/Qyzylorda (+06:00)
+ Asia/Rangoon (+06:30)
+ Asia/Riyadh (+03:00)
+ Asia/Saigon (+07:00)
+ Asia/Sakhalin (+11:00)
+ Asia/Samarkand (+05:00)
+ Asia/Seoul (+09:00)
+ Asia/Shanghai (+08:00)
+ Asia/Singapore (+08:00)
+ Asia/Srednekolymsk (+11:00)
+ Asia/Taipei (+08:00)
+ Asia/Tashkent (+05:00)
+ Asia/Tbilisi (+04:00)
+ Asia/Tehran (+03:30)
+ Asia/Tel_Aviv (+02:00)
+ Asia/Thimbu (+06:00)
+ Asia/Thimphu (+06:00)
+ Asia/Tokyo (+09:00)
+ Asia/Tomsk (+07:00)
+ Asia/Ujung_Pandang (+08:00)
+ Asia/Ulaanbaatar (+08:00)
+ Asia/Ulan_Bator (+08:00)
+ Asia/Urumqi (+06:00)
+ Asia/Ust-Nera (+10:00)
+ Asia/Vientiane (+07:00)
+ Asia/Vladivostok (+10:00)
+ Asia/Yakutsk (+09:00)
+ Asia/Yangon (+06:30)
+ Asia/Yekaterinburg (+05:00)
+ Asia/Yerevan (+04:00)
+ Atlantic/Azores (-01:00)
+ Atlantic/Bermuda (-04:00)
+ Atlantic/Canary (+00:00)
+ Atlantic/Cape_Verde (-01:00)
+ Atlantic/Faeroe (+00:00)
+ Atlantic/Faroe (+00:00)
+ Atlantic/Jan_Mayen (+01:00)
+ Atlantic/Madeira (+00:00)
+ Atlantic/Reykjavik (+00:00)
+ Atlantic/South_Georgia (-02:00)
+ Atlantic/St_Helena (+00:00)
+ Atlantic/Stanley (-03:00)
+ Australia/ACT (+11:00)
+ Australia/Adelaide (+10:30)
+ Australia/Brisbane (+10:00)
+ Australia/Broken_Hill (+10:30)
+ Australia/Canberra (+11:00)
+ Australia/Currie (+11:00)
+ Australia/Darwin (+09:30)
+ Australia/Eucla (+08:45)
+ Australia/Hobart (+11:00)
+ Australia/LHI (+11:00)
+ Australia/Lindeman (+10:00)
+ Australia/Lord_Howe (+11:00)
+ Australia/Melbourne (+11:00)
+ Australia/NSW (+11:00)
+ Australia/North (+09:30)
+ Australia/Perth (+08:00)
+ Australia/Queensland (+10:00)
+ Australia/South (+10:30)
+ Australia/Sydney (+11:00)
+ Australia/Tasmania (+11:00)
+ Australia/Victoria (+11:00)
+ Australia/West (+08:00)
+ Australia/Yancowinna (+10:30)
+ Brazil/Acre (-05:00)
+ Brazil/DeNoronha (-02:00)
+ Brazil/East (-02:00)
+ Brazil/West (-04:00)
+ CET (+01:00)
+ CST6CDT (-06:00)
+ Canada/Atlantic (-04:00)
+ Canada/Central (-06:00)
+ Canada/Eastern (-05:00)
+ Canada/Mountain (-07:00)
+ Canada/Newfoundland (-03:30)
+ Canada/Pacific (-08:00)
+ Canada/Saskatchewan (-06:00)
+ Canada/Yukon (-08:00)
+ Chile/Continental (-03:00)
+ Chile/EasterIsland (-05:00)
+ Cuba (-05:00)
+ EET (+02:00)
+ EST (-05:00)
+ EST5EDT (-05:00)
+ Egypt (+02:00)
+ Eire (+00:00)
+ Etc/GMT (+00:00)
+ Etc/GMT+0 (+00:00)
+ Etc/GMT+1 (-01:00)
+ Etc/GMT+10 (-10:00)
+ Etc/GMT+11 (-11:00)
+ Etc/GMT+12 (-12:00)
+ Etc/GMT+2 (-02:00)
+ Etc/GMT+3 (-03:00)
+ Etc/GMT+4 (-04:00)
+ Etc/GMT+5 (-05:00)
+ Etc/GMT+6 (-06:00)
+ Etc/GMT+7 (-07:00)
+ Etc/GMT+8 (-08:00)
+ Etc/GMT+9 (-09:00)
+ Etc/GMT-0 (+00:00)
+ Etc/GMT-1 (+01:00)
+ Etc/GMT-10 (+10:00)
+ Etc/GMT-11 (+11:00)
+ Etc/GMT-12 (+12:00)
+ Etc/GMT-13 (+13:00)
+ Etc/GMT-14 (+14:00)
+ Etc/GMT-2 (+02:00)
+ Etc/GMT-3 (+03:00)
+ Etc/GMT-4 (+04:00)
+ Etc/GMT-5 (+05:00)
+ Etc/GMT-6 (+06:00)
+ Etc/GMT-7 (+07:00)
+ Etc/GMT-8 (+08:00)
+ Etc/GMT-9 (+09:00)
+ Etc/GMT0 (+00:00)
+ Etc/Greenwich (+00:00)
+ Etc/UCT (+00:00)
+ Etc/UTC (+00:00)
+ Etc/Universal (+00:00)
+ Etc/Zulu (+00:00)
+ Europe/Amsterdam (+01:00)
+ Europe/Andorra (+01:00)
+ Europe/Astrakhan (+04:00)
+ Europe/Athens (+02:00)
+ Europe/Belfast (+00:00)
+ Europe/Belgrade (+01:00)
+ Europe/Berlin (+01:00)
+ Europe/Bratislava (+01:00)
+ Europe/Brussels (+01:00)
+ Europe/Bucharest (+02:00)
+ Europe/Budapest (+01:00)
+ Europe/Busingen (+01:00)
+ Europe/Chisinau (+02:00)
+ Europe/Copenhagen (+01:00)
+ Europe/Dublin (+00:00)
+ Europe/Gibraltar (+01:00)
+ Europe/Guernsey (+00:00)
+ Europe/Helsinki (+02:00)
+ Europe/Isle_of_Man (+00:00)
+ Europe/Istanbul (+03:00)
+ Europe/Jersey (+00:00)
+ Europe/Kaliningrad (+02:00)
+ Europe/Kiev (+02:00)
+ Europe/Kirov (+03:00)
+ Europe/Lisbon (+00:00)
+ Europe/Ljubljana (+01:00)
+ Europe/London (+00:00)
+ Europe/Luxembourg (+01:00)
+ Europe/Madrid (+01:00)
+ Europe/Malta (+01:00)
+ Europe/Mariehamn (+02:00)
+ Europe/Minsk (+03:00)
+ Europe/Monaco (+01:00)
+ Europe/Moscow (+03:00)
+ Europe/Nicosia (+02:00)
+ Europe/Oslo (+01:00)
+ Europe/Paris (+01:00)
+ Europe/Podgorica (+01:00)
+ Europe/Prague (+01:00)
+ Europe/Riga (+02:00)
+ Europe/Rome (+01:00)
+ Europe/Samara (+04:00)
+ Europe/San_Marino (+01:00)
+ Europe/Sarajevo (+01:00)
+ Europe/Saratov (+04:00)
+ Europe/Simferopol (+03:00)
+ Europe/Skopje (+01:00)
+ Europe/Sofia (+02:00)
+ Europe/Stockholm (+01:00)
+ Europe/Tallinn (+02:00)
+ Europe/Tirane (+01:00)
+ Europe/Tiraspol (+02:00)
+ Europe/Ulyanovsk (+04:00)
+ Europe/Uzhgorod (+02:00)
+ Europe/Vaduz (+01:00)
+ Europe/Vatican (+01:00)
+ Europe/Vienna (+01:00)
+ Europe/Vilnius (+02:00)
+ Europe/Volgograd (+03:00)
+ Europe/Warsaw (+01:00)
+ Europe/Zagreb (+01:00)
+ Europe/Zaporozhye (+02:00)
+ Europe/Zurich (+01:00)
+ GB (+00:00)
+ GB-Eire (+00:00)
+ GMT (+00:00)
+ GMT+0 (+00:00)
+ GMT-0 (+00:00)
+ GMT0 (+00:00)
+ Greenwich (+00:00)
+ HST (-10:00)
+ Hongkong (+08:00)
+ Iceland (+00:00)
+ Indian/Antananarivo (+03:00)
+ Indian/Chagos (+06:00)
+ Indian/Christmas (+07:00)
+ Indian/Cocos (+06:30)
+ Indian/Comoro (+03:00)
+ Indian/Kerguelen (+05:00)
+ Indian/Mahe (+04:00)
+ Indian/Maldives (+05:00)
+ Indian/Mauritius (+04:00)
+ Indian/Mayotte (+03:00)
+ Indian/Reunion (+04:00)
+ Iran (+03:30)
+ Israel (+02:00)
+ Jamaica (-05:00)
+ Japan (+09:00)
+ Kwajalein (+12:00)
+ Libya (+02:00)
+ MET (+01:00)
+ MST (-07:00)
+ MST7MDT (-07:00)
+ Mexico/BajaNorte (-08:00)
+ Mexico/BajaSur (-07:00)
+ Mexico/General (-06:00)
+ NZ (+13:00)
+ NZ-CHAT (+13:45)
+ Navajo (-07:00)
+ PRC (+08:00)
+ PST8PDT (-08:00)
+ Pacific/Apia (+14:00)
+ Pacific/Auckland (+13:00)
+ Pacific/Bougainville (+11:00)
+ Pacific/Chatham (+13:45)
+ Pacific/Chuuk (+10:00)
+ Pacific/Easter (-05:00)
+ Pacific/Efate (+11:00)
+ Pacific/Enderbury (+13:00)
+ Pacific/Fakaofo (+13:00)
+ Pacific/Fiji (+13:00)
+ Pacific/Funafuti (+12:00)
+ Pacific/Galapagos (-06:00)
+ Pacific/Gambier (-09:00)
+ Pacific/Guadalcanal (+11:00)
+ Pacific/Guam (+10:00)
+ Pacific/Honolulu (-10:00)
+ Pacific/Johnston (-10:00)
+ Pacific/Kiritimati (+14:00)
+ Pacific/Kosrae (+11:00)
+ Pacific/Kwajalein (+12:00)
+ Pacific/Majuro (+12:00)
+ Pacific/Marquesas (-09:30)
+ Pacific/Midway (-11:00)
+ Pacific/Nauru (+12:00)
+ Pacific/Niue (-11:00)
+ Pacific/Norfolk (+11:00)
+ Pacific/Noumea (+11:00)
+ Pacific/Pago_Pago (-11:00)
+ Pacific/Palau (+09:00)
+ Pacific/Pitcairn (-08:00)
+ Pacific/Pohnpei (+11:00)
+ Pacific/Ponape (+11:00)
+ Pacific/Port_Moresby (+10:00)
+ Pacific/Rarotonga (-10:00)
+ Pacific/Saipan (+10:00)
+ Pacific/Samoa (-11:00)
+ Pacific/Tahiti (-10:00)
+ Pacific/Tarawa (+12:00)
+ Pacific/Tongatapu (+13:00)
+ Pacific/Truk (+10:00)
+ Pacific/Wake (+12:00)
+ Pacific/Wallis (+12:00)
+ Pacific/Yap (+10:00)
+ Poland (+01:00)
+ Portugal (+00:00)
+ ROC (+08:00)
+ ROK (+09:00)
+ Singapore (+08:00)
+ Turkey (+03:00)
+ UCT (+00:00)
+ US/Alaska (-09:00)
+ US/Aleutian (-10:00)
+ US/Arizona (-07:00)
+ US/Central (-06:00)
+ US/East-Indiana (-05:00)
+ US/Eastern (-05:00)
+ US/Hawaii (-10:00)
+ US/Indiana-Starke (-06:00)
+ US/Michigan (-05:00)
+ US/Mountain (-07:00)
+ US/Pacific (-08:00)
+ US/Samoa (-11:00)
+ UTC (+00:00)
+ Universal (+00:00)
+ W-SU (+03:00)
+ WET (+00:00)
+ Zulu (+00:00)
