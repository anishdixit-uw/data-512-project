# Goal of the Project

In this project, I analyze wildfire impacts on a specific city in the US. The end goal is to be able to inform policy makers, city managers, city councils, or other civic institutions, to make an informed plan for how they could or whether they should make plans to mitigate future impacts from wildfires. I try to acquire data relating to wildfires aronud the US, and also some air quality historical data. We create a smoke estimate for the city of North Platte, Nebraska, and gauge how close it is to the actual AQI. We aclso visualize some parameters of the fire and gain insishgts into the frequency of fire occurrences, area burnt by fires and such. Finally, we create a forecasting model to predict smoke estimates for the next 25 years using time series analysis.
# Source Data

1. Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)
   https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81

2. Wildfire Cities Assignment
https://docs.google.com/spreadsheets/d/1cmTW5fgU3KyH6JbrRao-qWjzu2GovKk_BkA7a-poGFw/edit#gid=1247370552

# Licensing

1. Creative Commons License: https://creativecommons.org/licenses/by/4.0/

# Important Considerations for the Data

The GeoJSON dataset is massive and has around 136000 fire occurrences that need to be analyzed. It takes a long time to load the data, hence the data acquisition process needs good error handling. The features of each fire are not consistent. Some fires do not have the 'ring' parameter and instead have 'curved ring' which needs to be handled and dealt with separately. There is no data for years 2021, 2022 and 2023. 

AQI data is also messy. Because each weather station has different years of operation, the data needs to be amalgamated across 3 different stations. This also needs exception handling becasue the aqi parameter is often missing. My city locations simply had no data for gaseous pollutants, only particulate pollutants, so this case also needs to be handled separately.

# Helpful Documentation

1. Metadata for Wilfire Polygon Data: https://www.sciencebase.gov/catalog/file/get/61aa537dd34eb622f699df81?f=__disk__d0%2F63%2F53%2Fd063532049be8e1bc83d1d3047b4df1a5cb56f15&transform=1&allowOpen=true
   
2. Technical Assistance Document for the Reporting of Daily Air Quality – the Air Quality Index (AQI): https://www.airnow.gov/sites/default/files/2020-05/aqi-technical-assistance-document-sept2018.pdf
   
3. Facebook Prophet Library: https://facebook.github.io/prophet/docs/quick_start.html
   
5. Wildfire Data Reader Python Module: https://drive.google.com/file/d/1TwCkvdaw0MxJzW7NSDg6XxYQ0dvaS44I/view
   
6. Python Notebook for geidetic distance computation: https://drive.google.com/file/d/1qNI6hji8CvDeBsnLDAhJXvaqf2gcg8UV/view
    
7. Python Notebook to call EPI Air Quality History Data: [https://drive.google.com/file/d/17C9xsmR9U3lJeD52UTbAedlHDetwYsxs/view?usp=sharing](https://drive.google.com/file/d/1bxl9qrb_52RocKNGfbZ5znHVqFDMkUzf/view)

# Coding Process

1. In the Python Notebook **Wildfire Data Acquisition.ipynb**, we first read in data from **USGS_Wildland_Fire_Combined_Dataset.json**. This is a massive data file of 2.8GB and cannot be uploaded to Github. We then read in the GeoJSON data and all the wildfire occurrences. I then filter the data to only include those fires which are after 1963 and within 1250 miles of North Platte, Nebraska. I calculate a smoke estimate based on distance, area of fire and fire intensity as well. This is a time consuming process and a massive intermediate JSON is generated **smoke_estimate_NP.json**, which is also too big to upload to Github. The JSON data has data from 1963-2020.

2. In the Python Notebook **AQI Data Acquisition.ipynb**, we get Air Quality index data. We setup an account with EPA, create an API key and then repetitively call the API to get air quality indices around North Platte. Now, this city does not have any weather stations, so we create a bounding box for 50,100,150,200,250 miles around the city and get data from weather stations around there. Yearly API calls are made and AQI values are averaged out. Finally **aqi.csv** is generated with data from (1985-2022) and AQI values for each year.
   
3. In the Python Notebook **Wildlife Data Analysis.ipynb**, we read in **smoke_estimate_NP.json** and create visualizations, the process of which is explained in the **Reflections.pdf**. We also create predictions for smoke estimates 25 years into the future, using the Prophet library by facebook for Time Series Forecasting.
