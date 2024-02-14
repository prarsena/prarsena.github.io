+++
title = "Data analytics with Python"
date = "2023-07-07"
description = "Guide to getting started with Python for Data analytics"
tags = [
    "Python",
    "Data Analytics"
]
series = ["Python"]
+++

# Introduction
If you have been following new recently, you may have come across various headlines like "South Asia in Chinese Debt Trap", "Economic crisis in Sri Lanka", "Failing economy of Pakistan", etc. These news articles made me curious to look into bilateral lendings between 2 countries. Using python, I developed a script to download PPG Bilateral Debt data between 2 countries using World Bank API.

My project collects data of PPG bilateral lending between India and its neighbouring countries which include Bangladesh, Bhutan, Sri Lanka, Nepal, Maldives & Myanmar. I have wrangled and analysed data from last 20 years of each country individually and visualized the data in form of excel dashboard for easy understanding of lending trend. Check out the project report

# About the dataset
Dataset includes details of PPG Bilateral debt data between India & Bangladesh/Bhutan/Sri Lanka/Maldives/Myanmar/Nepal obtained using World Bank API. Each dataset contains 4 columns: 'Year': Year of debt, 'Debtor': Debtor country code,'Debt in US$': Amount of debt in US$, 'YoY Growth %': Year on year growth percentage of bilateral debt. All 6 datasets are combined, cleaned, wrangled and analysed here Data is gathered from World Bank website and considered as primary data.

# Python Script
Here's the script:
``` python
#Import required packages
import pandas as pd
import json
import requests

#Get all data sources from World Bank website
sources = requests.get("http://api.worldbank.org/v2/sources?per_page=100&format=json")
sourcesJSON = sources.json()

#Get ID of required data source
for i in sourcesJSON[1]:
    if i["name"] == "International Debt Statistics":
        print("ID of International Debt Statistics is " + i["id"])
    else:
        pass

#Get indicator code of required data
indicators = requests.get("http://api.worldbank.org/v2/indicator?format=json&source=6&per_page=600")
indicatorsJSON = indicators.json()
for i in indicatorsJSON[1]:
    IDSindicators = (i["id"],i["name"])
    print(i['id'], i['name'])

#Getting information of selected indicator
indicator = "DT.DOD.BLAT.CD"
for dict_entity in indicatorsJSON[1]:
    if dict_entity["id"] == indicator:
        print(dict_entity["sourceNote"])
    else:
        pass

# Requesting the locations
clocations = requests.get("http://api.worldbank.org/v2/sources/6/counterpart-area?per_page=300&format=JSON")
clocationsJSON = clocations.json()

# Parse through the response to see the location IDs and names
clocations = clocationsJSON["source"][0]["concept"][0]["variable"]
listLen = int(len(clocations))

# Create dataframe with location values
df = pd.DataFrame(columns=["id", "value"])     
for i in range(0,listLen):
    code = clocations[i]["id"]
    name = clocations[i]["value"]
    df = df.append({"id":code, "value":name}, ignore_index = True)
clocationsList = df
print(clocationsList)

#Converting the gathered data into Excel file
clocationsList.to_excel('Creditor Country Code.xlsx')
print("Excel File Saved")
```
 
# Conclusion of project
Total PPG Bilateral Lending has increased from less than 500 million $ in 2000 to about 45 billion $ in 2020
1. Bhutan has been the biggest debtor country receiving almost 18 billion $ over the period of 20 years
2. Nepal has received the least bilateral lending amounting to less than 1 billion $
3. Total bilateral lending show a positive growth rate since last 20 years
4. Total bilateral lending to neighbouring countries is approx. 1.2% of overall GDP of India
5. In the event of default by any neighboring country in future, its impact on India’s financial sector will be minimal (Considering only the above data)