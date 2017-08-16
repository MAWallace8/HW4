# HW4
Matplotlib Homework

#import potential dependencies

import pandas as pd
import json
import numpy
import matplotlib.pyplot as plt
import csv
import seaborn

#identify relevent .csv files as variables

cityData = "city_data.csv"
rideData = "ride_data.csv"

#importing cities information with pandas and csv packages, display first 5 rows

city_pd = pd.read_csv(cityData)
city_pd.head()

#importing ride information with pandas and csv packages, display first 5 rows

ride_pd = pd.read_csv(rideData)
ride_pd.head()

#merge both csvs to link fares to types, cities, etc., display first 5 rows

pyBer_df = pd.merge(city_pd, ride_pd, on='city', how='outer')
pyBer_df.head()

#create new dataframe with needed information for fare % by region

typeFare = pyBer_df.groupby('type')["fare"].sum().reset_index()
typeFare


#create pie chart for fares by city type

fig1, ax1 = plt.subplots()
ax1.pie(typeFare["fare"], labels = typeFare["type"], shadow = True, explode = (0,0,0.1), 
        startangle=90, autopct = "%1.1f%%")
ax1.axis('equal')
plt.title('Fares by City Type', fontsize = 14).axes.get_yaxis().set_visible(False)
plt.show()

#create dataframe of sum of drivers by city type

typeDriver = pyBer_df.groupby('type')["driver_count"].sum().reset_index()
typeDriver

#plot drivers by region type 

fig1, ax1 = plt.subplots()
ax1.pie(typeDriver["driver_count"], labels = typeDriver["type"], shadow = True, explode = (0,0,0.1), 
        startangle=90, autopct = "%1.1f%%")
ax1.axis('equal')
plt.title('Drivers by City Type', fontsize = 14).axes.get_yaxis().set_visible(False)
plt.show()

#create data frame for rides counting dates on record by city type

typeRides = pyBer_df.groupby('type')["date"].count().reset_index()
typeRides

#plot chart of rides by city type

fig1, ax1 = plt.subplots()
ax1.pie(typeRides["date"], labels = typeRides["type"], shadow = True, explode = (0,0,0.1), 
        startangle=90, autopct = "%1.1f%%")
ax1.axis('equal')
plt.title('Ride by City Type', fontsize = 14).axes.get_yaxis().set_visible(False)
plt.show()

