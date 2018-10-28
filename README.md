# problem_set3
comp tools for research assignment

problem 1

import csv #import the cvs library
with open('CO-OPS__8729108__wl.csv') as f:
    reader = csv.reader(f)
    next(reader) # skip header
    data = [] #get the date as a sting
    dct = {} #get the value in a dictionnary

    for column in reader: #use of for loop to read through the each line of the data frame
        date_time = column[0] # select first column of the data frame
        w_level= column[1] # select the second column of the data frame
        dct[date_time]=w_level
        dct[w_level]=date_time

print(max(dct)) #print the water level max
print(max(dct,key=dct.get)) # print the date when water level max was observed


#Problem 2
import pandas as pd

df=pd.read_csv("CO-OPS__8729108__wl.csv")

highest=df[" Water Level"].idxmax()

print(df.loc[highest, "Date Time" : " Water Level"])

#Problem 3

import pandas as pd

df=pd.read_csv("C:/Users/moeinraja/Desktop/CO-OPS__8729108__wl.csv")

df['difference'] = df[" Water Level"].diff()

highest=df['difference'].idxmax()

print(df.iloc[highest,[0, 1, 8]])


import matplotlib.pyplot as plt

import pandas as pd

df=pd.read_csv("CO-OPS__8729108__wl.csv")

x, y=df['Date Time'], df[' Water Level']

fig=plt.figure()

plt.plot(x, y)

plt.xlabel("Time")


#Extra credit. Download was done on Oct. 24 2018

import requests #importpython request library
from bs4 import BeautifulSoup #import BeautifulSoup
#define a variable containing the URL
url = "https://tidesandcurrents.noaa.gov/waterlevels.html?id=8729108&units=standard&bdate=20181011&edate=20181012&timezone=GMT&datum=MLLW&interval=6&action=data"

response = requests.get(url) #pass the URL to the we defined to the request.get fucntion that will visit the Panama pacific webpage and fetch the html
html = response.text #

soup = BeautifulSoup(html, "html.parser") #we use beautiful soup to parse its representation of a webpage
links = soup.findAll("a") #find links in the html pages
