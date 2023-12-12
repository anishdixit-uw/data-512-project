# Goal of the Project

To summarize the project, this undertaking involves analyzing wildfires in the US, specifically around North Platte, Nebraska, and trying to estimate the impact these wildfires and the smoke produced have on the environment, society and lives of residents around. I calculated a smoke impact estimate to quantify the wildfire smoke’s effect on the city. One of my research questions involves trying to correlate my smoke estimates with the actual Air Quality Index in the region. I also found that there are lesser fires close to the city, but also that wildfires have burnt huge amounts of land around the city in recent years. I tried to forecast future trends in smoke and found that smoke in the city will increase in the coming years and the local authorities need to administer measures to ensure the residents are not affected.

I also tried to give a human centered angle to my analysis by trying to gauge if respiratory diseases such as lung cancer in the area were a by-product of the smoke in the air. I found that though the overall lung cancer cases in the area were going down of late, the fatality rates were very high and this needed fixing. Finally, I tried to forecast future lung cancer occurrences using smoke estimates as a predictor and concluded that cases could well increase in the future.

# Source Data

1. Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)
   https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81

2. Wildfire Cities Assignment
https://docs.google.com/spreadsheets/d/1cmTW5fgU3KyH6JbrRao-qWjzu2GovKk_BkA7a-poGFw/edit#gid=1247370552

3. Cancer Cases in Nebraska Report (2006)
https://dhhs.ne.gov/Reports/Cancer%20Incidence%20and%20Mortality%20in%20Nebraska%20-%202006.pdf

4. Cancer Cases in Nebraska Report (2013)
https://dhhs.ne.gov/Reports/Cancer%20Incidence%20and%20Mortality%20in%20Nebraska%202013.pdf

6. Cancer Cases in Nebraska Report (2019)
https://dhhs.ne.gov/Reports/Cancer%20Incidence%20and%20Mortality%20in%20Nebraska%202019.pdf

8. Nebraska Population Data
https://revenue.nebraska.gov/sites/revenue.nebraska.gov/files/doc/MUN_1_Cert_Pop_Summary.xlsx

# Features in Data Files

1. *USGS_Wildland_Fire_Combined_Dataset.json* - Original wildfire data file, too big to be uploaded to Github

| Features Used      | Description |
| ----------- | ----------- |
| Fire_Year      | The Year in which the wildfire occurred       |
| GIS_Acres   | Area of Land burnt (in 10^7 acres)        |
| Assigned_Fire_Type | Type of wildfire (wildfire, prescribed fire etc.) |

2. *aqi.csv* - File generated from calling AQS API
   
| Features Used      | Description |
| ----------- | ----------- |
| Year      | All Years for which AQIs are available       |
| avg_aqi   | Average yearly AQI values around North Platte        |

3. *smoke_estimate_np.json* - File generated after generating smoke estimates, too big to be uploaded to Github

| Features Used      | Description |
| ----------- | ----------- |
| Fire_Year      | The Year in which the wildfire occurred       |
| distance   | Distance of fire from North Platte        |
| smoke_estimate | Computed impact of smoke in North Platte |

4. *future_predicted_smoke_values.csv* - File generated after forecasting future smoke values

| Features Used      | Description |
| ----------- | ----------- |
| ds      | The Year for which predictions are made       |
| yhat   | Predicted smoke estimate value        |

5. *population_1990s.csv* - File containing North Platte population from 1990-2000

| Features Used      | Description |
| ----------- | ----------- |
| Year      | The Year in which the census was carried out       |
| Population   | Number of people residing in the city        |

6. *MUN_1_Cert_Pop_Summary.xlsx* - File containing North Platte 2000 onwards - organized by different sheets per year

| Features Used      | Description |
| ----------- | ----------- |
| County      | Different counties for which census was carried out       |
| Population   | Number of people residing in the area        |

7. *cancer_data.csv* - File containing cancer case occurrences data

| Features Used      | Description |
| ----------- | ----------- |
| Year      | List of years for which cancer data is present       |
| Total Cancer Cases   | Total count of all type of cancer cases in Nebraska per 100000 of population        |
| Lung Cancer Cases   | Total count of lung cancer cases in Nebraska per 100000 of population        |
| Lung Cancer Mortality   | Total count of lung cancer fatalities in Nebraska per 100000 of population        |

8. *future_cancer_predictions.csv* - File generated after predicting future trends in lung cancer cases

| Features Used      | Description |
| ----------- | ----------- |
| ds      | The Year for which predictions are made       |
| Cancer Cases   | Predicted count of yearly lung cancer cases in the North Platte region        |

9. *Cancer Incidence and Mortality in Nebraska (2006,2013,2019)* - Reports generated by the Nebraska Department of Public Health which keep a track of all types of cancer occurrences in the state. *cancer_data.csv* has been generated from data from these files.

# Licensing

1. Creative Commons License: https://creativecommons.org/licenses/by/4.0/

# Important Considerations for the Data

The GeoJSON dataset is massive and has around 136000 fire occurrences that need to be analyzed. It takes a long time to load the data, hence the data acquisition process needs good error handling. The features of each fire are not consistent. Some fires do not have the 'ring' parameter and instead have 'curved ring' which needs to be handled and dealt with separately. There is no data for years 2021, 2022 and 2023. 

AQI data is also messy. Because each weather station has different years of operation, the data needs to be amalgamated across 3 different stations. This also needs exception handling becasue the aqi parameter is often missing. My city locations simply had no data for gaseous pollutants, only particulate pollutants, so this case also needs to be handled separately.

We also have not considered fire season in either our wildfire or AQI data. The USA fire season runs from May to October, but because we do not have good month level data, we do not consider this, which is an oversight.

Cancer cases dataset has been manually curated and the accuracy of the public health reports, if questionable, can put the efficacy of the analysis into doubt.

# Helpful Documentation

1. Metadata for Wilfire Polygon Data: https://www.sciencebase.gov/catalog/file/get/61aa537dd34eb622f699df81?f=__disk__d0%2F63%2F53%2Fd063532049be8e1bc83d1d3047b4df1a5cb56f15&transform=1&allowOpen=true
   
2. Technical Assistance Document for the Reporting of Daily Air Quality – the Air Quality Index (AQI): https://www.airnow.gov/sites/default/files/2020-05/aqi-technical-assistance-document-sept2018.pdf
   
3. Facebook Prophet Library: https://facebook.github.io/prophet/docs/quick_start.html
   
5. Wildfire Data Reader Python Module: https://drive.google.com/file/d/1TwCkvdaw0MxJzW7NSDg6XxYQ0dvaS44I/view
   
6. Python Notebook for geidetic distance computation: https://drive.google.com/file/d/1qNI6hji8CvDeBsnLDAhJXvaqf2gcg8UV/view
    
7. Python Notebook to call EPI Air Quality History Data: [https://drive.google.com/file/d/17C9xsmR9U3lJeD52UTbAedlHDetwYsxs/view?usp=sharing](https://drive.google.com/file/d/1bxl9qrb_52RocKNGfbZ5znHVqFDMkUzf/view)
   
8. Nebraska Public Health Reports: [https://dhhs.ne.gov/Pages/Public-Health-Reports.aspx]
   
9. Nebraska Revenue Department Statistics: [https://revenue.nebraska.gov/research/statistics/local-government-data]
    
10. EPA Research Study on Wildfire Effects on Health: [https://www.epa.gov/air-research/wildland-fire-research-health-effects-research]


# Methodology

*1. Wildfire Data Acquisition*

In the Python Notebook Wildfire_Data_Acquistion.ipynb, we first read in wildfire data from the JSON file of Combined wildfires, USGS_Wildland_Fire_Combined_Dataset.json, which is obtained from the US Geological Survey. This is a massive data file of 2.8GB. Professor McDonald’s GeoJSON reader library and helpful code, which we are licensed to use, helped me undertake these processing steps.
I then filter the data to only include those fires which are after 1963 and within 1250 miles of North Platte, Nebraska. I calculate a smoke estimate based on distance, area of fire and fire intensity as well. Smoke should be inversely proportional to distance (more the distance, lesser the smoke spread), directly to area burnt and also to fire intensity (wildfires should be weighted more than prescribed fires, I have chosen 2x). The intensity parameter is weighted as follows:

```
fire_intensity['Wildfire'] = 2

fire_intensity['Likely Wildfire'] = 1.75

fire_intensity['Unknown - Likely Wildfire'] = 1.5

fire_intensity['Prescribed Fire'] = 1.25

fire_intensity['Unknown - Likely Prescribed Fire'] = 1
```

Smoke estimate formula is:

```
Smoke_Estimate = (Fire_Intensity*Area_Burnt)/Fire_Distance
```
A massive intermediate JSON is generated named smoke_estimate_NP.json, which has wildfire features, distance from city and smoke estimate value. The JSON data has data from 1963-2020.


*2. AQI Data Acquisition*

In the Ipython Notebook ,AQI_Data_Acquisition.ipynb, I get Air Quality index data from the US AQS (Air Quality System) API implemented by the EPA. Professor McDonald’s helper notebook, licensed freely to use, helps in this process. I set up an account with EPA, created an API key and then repetitively called the API to get air quality indices around North Platte. Now, this city does not have any weather stations close by, so we create a bounding box for 50,100,150,200,250 miles around the city and get data from weather stations around there. Yearly API calls are made and AQI values are averaged out. Finally aqi.csv is generated with yearly data from (1985-2022) and AQI values for each year.

*3. Wildfire Data Analysis*

In the Python Notebook Wildlife Data Analysis.ipynb, we read in smoke_estimate_NP.json and create visualizations, corresponding to different kinds of impact of the fires. The first graph is a histogram of the number of fires occurring every 50 miles from North Platte. The second graph charts out the area of land burnt by wildfires per year. The third chart tries to correlate air quality index with calculated smoke estimate and finds similarities in the two. We also create predictions for smoke estimates 25 years into the future, using the Prophet library by Facebook for Time Series Forecasting. The predicted smoke estimate values and corresponding years are saved in future_predicted_smoke_estimate.csv.

*4.  Extension Plan*

I planned to extend this work by trying to apply it to certain socio-economic factors, giving it a human centered angle, which can actually impact the community of North Platte as well. The focus area I am choosing to base my analysis on is Healthcare. I chose this domain because I believe the smoke estimate calculated in the common analysis would have the maximum impact and correlation with the health of the residents of North Platte. As mentioned in the motivation, standalone wildfires can affect the health and well being of the individuals residing in the city, and can have detrimental effects on the long term fitness as well. Of course, wildfires are not the only contributors to this wane of health, it is a much larger systemic problem, but it can still serve as one indicator.  I intend to study occurrences of bronchial cancer and tuberculosis in the North Platte area across years, try to map and correlate it to the yearly smoke estimate in part 1, and predict how feature frequency of cancer cases/mortality rates would look. 

I decided to expand upon these diseases specifically as these are respiratory illnesses. They can be directly brought about, cause or if inherently present, intensified by excessive smoke in the region, which my previous work can help with. A future prediction can help medical services be prepared for sudden spikes in cases in a cyclic manner if any seasonality exists, or if there is simply a generic upward trend in the number of cases found. This work could help the health services in the North Platte city and Lincoln county better understand how wildfire occurrences could be a potential harbinger of respiratory diseases and how the population is being affected by the same. Efforts can be made to better handle these humanitarian problems.

*5. Modeling Smoke Impact on Respiratory Illnesses*

In the Python Notebook Smoke Impact + Respiratory Illness Modeling.ipynb, we read in population data from the MUN_1_Cert_Pop_Summary.xlsx and population_1990s.csv and merge it. We also read in cancer cases data from cancer_data.csv. I then have a look at a comparison of total detected lung cancer cases and fatalities by plotting a bar chart. I also read the smoke estimates calculated in smoke_estimates_np.json. I plot Correlations between cancer occurrences and smoke estimates and find good positive correlations. Finally, I try to predict future trends in lung cancer cases by using a Linear Regression model with smoke estimate as a predictor and obtain interesting trends. These values are stored into lung_cancer_predictions.csv with yearly values.
