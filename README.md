# 06-python-api-challenge
Week 06 Challenge APIs




# WeatherPy

Analyze weather data of random cities within a specified Latitude/Longitude range and create plots that show the correlation between temperature and latitude position in relation to the equator.

## Dependencies
 - matplotlib
 - pandas
 - numpy
 - requests
 - time
 - linregress from scipy.stats
 - citipy
 - openweather api key

## Generate the Cities List by Using the `citipy` Library
Created empty lists for holding latitude and longitude combinations as well as an empty list for city names.
Defined the latitude and longitude ranges then created a set of random latitude and longitude combinations based off of those ranges.
Using a for loop, identified the nearest city for each latitude/longitude combination and, given the cities were unique, added them to the cities list.

## Creating the Plots That Will Show the Relationship Between Weather Variables and Latitude
#### Openweather API used to retrieve weather data for the previously generated cities
Set the base url (https://api.openweathermap.org/data/2.5/weather?") concatinated with the weather api key.
An empty list is defined to store each citie's data and create counters that will be used in a for loop.
Print indicating the data retrieval has begun

Using a for loop, loop through the cities from the cities list to fetch weather data:
Cities grouped into sets of 50 for logging, define endpoint URL for each city, and the url, record and set numbers.
record count updated (+1) for the preceeding loop(s).

Run API request for each city using try-except.
JSONify the endpoint URL and parse out the latitude, longitude, max temperature, humidity, cloudiness, wind speed, country and date and append the data to the city data list and skip any city producing an error.
Print indicating the data loading has been completed.

The city data is converted into a pandas data frame and the record count is shown using .count(), data frame sample is displayed using .head(), dataframe is exported into a csv.

## Creating the Scatter Plots using `matplotlib`
#### Latitude Vs. temperature
Build scatter plot by defining latitude values and temperatures from the city data dataframe's respective columns and define marker formating.

x axis label, y axis label and chart title defined, chart saved to output folder as .png and displayed.

![Alt text](https://github.com/joey-october85/06-python-api-challenge/blob/main/WeatherPy/output_data/Fig1.png?raw=true "Fig1")

#### Latitude Vs. Humidity
The same steps used to create the previous chart now using 'Humidity' data for the y axis
![Alt text](https://github.com/joey-october85/06-python-api-challenge/blob/main/WeatherPy/output_data/Fig2.png?raw=true "Fig2")

#### Latitude Vs. Cloudiness 
The same steps used to create the previous chart now using 'Humidity' data for the y axis
![Alt text](https://github.com/joey-october85/06-python-api-challenge/blob/main/WeatherPy/output_data/Fig3.png?raw=true "Fig2")

#### Latitude vs. Wind Speed Plot
The same steps used to create the previous charts now using 'Wind Speed' data for the y axis
 ![Alt text](https://github.com/joey-october85/06-python-api-challenge/blob/main/WeatherPy/output_data/Fig4.png?raw=true "Fig2")


## Compute Linear Regression for Each Relationship
Defined funcition to create linear regression plots.
within the funcition, used linregress and temporary variables for slope, intercept, r value, p value and standard error.
Defined variable to calculate the regression line (x * slope + intercept)
Define variable that will store string of regression line formula.
Scatter function defined using x and y variables and regression line defined using x variable, regression variable and formatting for the line.
define annotation for the line dsiplay, the corrdinates where it will be displayed on the chart and the formatting.
print statment added to display r value.

#### Defining the Hemisphere dataframes
Created a dataframes for Northern Hemisphere and Southern Hemisphere using .loc to find latitude greater than or equal to zero (for the northern hemisphere) and < zero (for the southern hemisphere)

### Regression Plots
For all regression plots, the x axis was difined using latitude data from the respective northern/southern hemisphere dataframes, and the y axis was defined using the requested data again from the respective northern/southern hemisphere dataframes.
x and y labels defined and the linear regression function called using these variables.

The annotation coordinates were defined for each chart for optimal positioning.

#### Temperature vs. Latitude Linerar Regression Plot 
Discussion about the linear relationship:

The data shows there is a correleation between temperature and latitude
 - Northern Hemisphere: As cities' latitude go up further away from zero(0), the max temperatures decrease.
 - Southern Hemisphere: As cities' latitude get closer to zero (0), the max temperatures increase.


#### Humidity vs. Latitude Linerar Regression Plot
Discussion about the linear relationship:

The data shows no correlation between Humidity and Latitude

#### Cloudiness vs. Latitude Linerar Regression Plot
Discussion about the linear relationship:
The data shows no correlation between Cloudinessand Latitude

#### Wind Speed vs. Latitude Linerar Regression Plot
Discussion about the linear relationship:
The data shows no correlation between Wind Speed and Latitude






# VacationPy 
Using the weather and city data from `WeatherPy`, we use geoapify to locate vacation hotels in cities with ideal weather conditions.

## Dependencies
 - hvplot.pandas
 - pandas
 - requests
 - geoapify api key

 ### Import Libraries and Load the Weather and Coordinates Data and create a Map
 The csv file from the `WeatherPy` program is loded into as a dataframe and define a map plot using latitue and longitude data from the dataframe. Additionally formatting and other parameters are defined, such as frame widht/height, size, marker color and opacity.
 The map is displayed.

 ### City Data DataFrame is narrowed down to find ideal weather conditions
 The original dataframe is copied into a new clean dataframe, the new values are defined for minimum and maximum temperatures, wind speed and cloudiness and all null values are dropped.

 From the clean dataframe, we create a new dataframe with an empty column for hotels.

 ### Retreiving hotels
 Set the parameters to search for hotels.
 print a message to display the start of the hotel search.

 A for loop is used to iterate through the hotel dataframe.
 The latitude and longitude data is retrieved for each row and then a filter and bias parameters are added with the current city's latitude and longitude to the params dictionary.

The base URL is defined, an API request made using the params dictionary, and then converted the API respons to JSON format.

Try-Except used to pull the first hotel from the results and store the name in the hotel dataframe.
If no hotel is found, the hotel name is set to "No Hotel Found" and the results are logged.

An updated map plot is configued with additional functionality to add the hotel name and country as additional information for each city in the map and display the map. 

Extra data frame and map created to exclude cities where "No Hotel Found" value was identified in the "Hotel Name" column.