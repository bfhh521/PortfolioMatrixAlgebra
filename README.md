# PortfolioMatrixAlgebra

This is a simple calculation of Markowitz Portfolio method to find efficient portfolios,global minimum portfolios, tangency portfolios.
A testing function has also being provided to report the proposed return with differenct portfolios.

# Start with:

import pylab as pl
import numpy as np
import PortfolioMatrixAlgebra
import DataProcessing

# using np.loadtxt to load data from CSV and create 1D array e.g. [1,2,3 ......] format

BTC = np.loadtxt("BTC-USD.csv", delimiter = ",",skiprows = 1,usecols = (5))  
ETC = np.loadtxt("ETC-USD.csv", delimiter = ",",skiprows = 1,usecols = (5))  
LTC = np.loadtxt("LTC-USD.csv", delimiter = ",",skiprows = 1,usecols = (5))  
BTC2 = np.loadtxt("BTC-USD2.csv", delimiter = ",",skiprows = 1,usecols = (5))  

# using compute_ln_return function from DataProcessing file to transfer data into ln return

Ln_return_BTC = DataProcessing.compute_ln_return (BTC  )
Ln_return_ETC = DataProcessing.compute_ln_return (ETC )
Ln_return_LTC = DataProcessing.compute_ln_return (LTC )
Ln_return_BTC2 = DataProcessing.compute_ln_return (BTC2  )

# Create an array with different risky asset, not able to copy two same asset since inverse of covariance matrix would return error.
Ln_return_input = [Ln_return_BTC,Ln_return_ETC,Ln_return_LTC,Ln_return_BTC2  ]

# Initialise  PortfolioMatrixAlgebra class, with input of Ln_return_input and value of risk free asset (0.001)
port = PortfolioMatrixAlgebra.PortfolioMatrixAlgebra (Ln_return_input, 0.001) 

# Print report of efficient frontier graph, efficient portfolios,global minimum portfolios, tangency portfolios.
port.report()
![image](https://user-images.githubusercontent.com/42155686/44324785-ca495800-a4aa-11e8-9ea3-ec5c78603cbf.png)
![image](https://user-images.githubusercontent.com/42155686/44325152-0b8e3780-a4ac-11e8-8c6f-a8aa3684b099.png)
# Print profit and loss graph with proposed asset portfolio e.g.:

x = port.tangency_portfolio()[2]

DataProcessing.investment_report (x ,1000,inputData)   

![image](https://user-images.githubusercontent.com/42155686/44328619-1c43ab00-a4b6-11e8-8042-ccec13a2c596.png)
