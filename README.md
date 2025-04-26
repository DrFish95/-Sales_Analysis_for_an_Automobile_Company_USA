# -Sales_Analysis_for_an_Automobile_Company_USA
A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.
### PROBLEM STATEMENT:
## What are the Top Most-Profitable 5 States for a Bike business in the United States ?
## DATA PRE-PROCESSING
#### DATA LOADING
## importing all the necessary python packages 
```python
# solution 

import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt

print('the package has been successfully imported')

```
```python
bikes_df = pd.read_csv("C:/Users/office/Documents/_EXCLUSIVE DATA SCIENCE BOOT CAMP_STUDENT FOLDER/_DATASET/bikes.csv")

bikes_df.head()

![projec1 screen 2](https://github.com/user-attachments/assets/a219860c-6131-4cd9-8b6a-032d42785b67)


```
# DATA MODIFICATION
```python
# (1). Adding the following 3 extra columns to pansdas Dataframe:  bikes_df







# TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 





# SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 



# Profit : To be obtained by (SalesRevenue - TotalCostPrice)



bikes_df["Profit"] = bikes_df["SalesRevenue"] - bikes_df["TotalCostPrice"]


bikes_df.head()

![Data modification](https://github.com/user-attachments/assets/d33461a1-7ece-477f-b56a-c9d99f0129be)


```
## DATA ANALYSIS
#### DATA FILTERING
 # Filtering out only the data relevant to solving the problem statement
 ```python
is_usa = bikes_df["CustomerCountry"] == "United States"

is_bike = bikes_df["ProductCategory"] == "Bikes" 

bikes_in_the_us = bikes_df[(is_usa) & (is_bike)]

bikes_in_the_us.head()


![Data analysis screenshot](https://github.com/user-attachments/assets/8a05b0e0-d513-4989-892b-2a9ccdd655fb)



```
#### DATA AGREGATION
```python
# agregating the total profit by states in the united states for bike sales

total_profit_by_states = bikes_in_the_us.pivot_table(values = "Profit", index = "CustomerState",aggfunc = np.sum)
 
total_profit_by_states

![Data agregation screenshot](https://github.com/user-attachments/assets/6b1fa50b-83c6-4f62-bd55-11014c6ee414)


```
## DATA SORTING
```python
# sorting the agregated data,

# in order according to the top most profitable states


total_profit_by_states.sort_values("Profit", ascending = False)

![Data Sorting screenshot](https://github.com/user-attachments/assets/968817f2-0a64-41be-af9c-20c7b4518d4a)

![Data sorting screenshot2](https://github.com/user-attachments/assets/64faa008-0f37-4c86-bcd4-5a901e9ee97c)


```
## RESULTS
```python
 #Top_Most-Profitable 5 States for a Bike business in the United State ?
top_5_most_profitable_state_USA_bike =total_profit_by_states.sort_values("Profit", ascending = False).head()
top_5_most_profitable_state_USA_bike

```
## DATA VISUALIZATION
```python
# visualizing the result

top_5_most_profitable_state_USA_bike.plot(kind = "bar")

# adding a little and label to the plot 

plt.title("The top 5 most profitable states for Bike product in the Us")

plt.ylabel("Total profit in Million Dolars")
plt.xlabel("States")

# showing the plot

plt.show()

```


![project_1 picture](https://github.com/user-attachments/assets/3b4e2801-456d-4c4f-9be2-30fa122c31bf)


