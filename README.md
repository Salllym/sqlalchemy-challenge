# SQLAlchemy - Surfs Up!
Python and SQLAlchemy to do basic climate analysis and data exploration of the climate database. Using SQLAlchemy ORM queries, Pandas, and Matplotlib.

![surfs-up.png](Images/surfs-up.png)

Congratulations! You've decided to treat yourself to a long holiday vacation in Honolulu, Hawaii! To help with your trip planning, you need to do some climate analysis on the area. The following outlines the tasks that must be completed to accomplish this task.

## Step 1 - Climate Analysis and Exploration


* Use the provided [starter notebook](climate_starter.ipynb) and [hawaii.sqlite](Resources/hawaii.sqlite) files to complete your climate analysis and data exploration.

* Use SQLAlchemy `create_engine` to connect to your SQLite database.

* Use SQLAlchemy `automap_base()` to reflect your tables into classes and save a reference to those classes called `Station` and `Measurement`.

* Link Python to the database by creating a SQLAlchemy session. 

* **Important:** Don't forget to close out your session at the end of your notebook.

### Precipitation Analysis

* Find the most recent data in the dataset. 

* Design a query to retrieve the last 12 months of precipitation data.

* Select only the `date` and `prcp` values.

* Load the query results into a Pandas DataFrame and set the index to the date column.

* Sort the DataFrame values by `date`.

* Plot the results using the DataFrame `plot` method.

 ![precipitation](Images/precipitation.png)

* Use Pandas to print the summary statistics for the precipitation data.

### Station Analysis

* Design a query to calculate the total number of stations.

* Design a query to find the most active stations (stations with the most rows).

  * List the stations and observation counts in descending order.

  * Which station has the highest number of observations?

  * Using the most active station id, calculate the lowest, highest, and average temperatures.

  * Hint: You may need to use functions such as `func.min`, `func.max`, `func.avg`, and `func.count` in your queries.

* Design a query to retrieve the last 12 months of temperature observation data (TOBS).

  * Filter by the station with the highest number of observations.

  * Query the previous 12 months of temperature observation data for this station.

  * Plot the results as a histogram with `bins=12`.

    ![station-histogram](Images/station-histogram.png)

- - -

## Step 2 - Climate App

Now that you have completed your initial analysis, design a Flask API based on the queries that you have just developed.

* Use Flask to create your routes.

### Routes

* `/`

  * Home page.

  * List all available routes.

* `/api/v1.0/precipitation`

  * Convert the query results to a dictionary using `date` as the key and `prcp` as the value.

  * Return the JSON representation of your dictionary.

* `/api/v1.0/stations`

  * Return a JSON list of stations from the dataset.

* `/api/v1.0/tobs`
  * Query the dates and temperature observations of the most active station for the last year of data.
  
  * Return a JSON list of temperature observations (TOBS) for the previous year.

* `/api/v1.0/<start>` and `/api/v1.0/<start>/<end>`

  * Return a JSON list of the minimum temperature, the average temperature, and the max temperature for a given start or start-end range.

  * When given the start only, calculate `TMIN`, `TAVG`, and `TMAX` for all dates greater than and equal to the start date.

  * When given the start and the end date, calculate the `TMIN`, `TAVG`, and `TMAX` for dates between the start and end date inclusive.


## Bonus: Other Recommended Analyses

* The following are optional challenge queries. These are highly recommended to attempt, but not required for the homework.

### Temperature Analysis 1

* Hawaii is reputed to enjoy mild weather all year. Is there a meaningful difference between the temperature in, for example, June and December?

* Use Pandas to perform the following steps:

    * Convert the date column format from `string` to `datetime`.

    * Set the date column as the DataFrame index.

    * Drop the date column.

* Identify the average temperature in June at all stations across all available years in the dataset. Do the same for December temperature.

* Use the t-test to determine whether the difference in the means, if any, is statistically significant. Will you use a paired t-test, or an unpaired t-test? Why?

### Temperature Analysis 2

You want to take a trip from August 1 to August 7 of this year, but you are worried that the weather will be less than ideal. Using historical data in the dataset, find out what the temperature has previously been for this timeframe.

**Note:** The starter notebook contains a function called `calc_temps` that will accept a start date and end date in the format `%Y-%m-%d`. The function will return the minimum, average, and maximum temperatures for that range of dates.

* Use the `calc_temps` function to calculate the minimum, average, and maximum temperatures for your trip using the matching dates from a previous year (for example, use "2017-08-01").

* Plot the minimum, average, and maximum temperature from your previous query as a bar chart, as captured in the following steps and image:

    * Use "Trip Avg Temp" as the title.

    * Use the average temperature as the bar height (_y_ value).

    * Use the peak-to-peak (TMAX-TMIN) value as the _y_ error bar (YERR).

    ![temperature](Images/temperature.png)

### Daily Rainfall Average

* Calculate the rainfall per weather station using the previous year's matching dates.

    * Sort this in descending order by precipitation amount, and list the station, name, latitude, longitude, and elevation.

### Daily Temperature Normals

Calculate the daily normals for the duration of your trip. Normals are the averages for the minimum, average, and maximum temperatures.

You are provided with a function called `daily_normals` that will calculate the daily normals for a specific date. This date string will be in the format `%m-%d`. Be sure to use all historic TOBS that match that date string.

Complete the following steps:

* Set the start and end date of the trip.

* Use the date to create a range of dates.

* Strip off the year, and save a list of strings in the format `%m-%d`.

* Use the `daily_normals` function to calculate the normals for each date string, and append the results to a list called `normals`.

* Load the list of daily normals into a Pandas DataFrame, and set the index equal to the date.

* Use Pandas to plot an area plot (`stacked=False`) for the daily normals, as shown in the following image:

  ![daily-normals](Images/daily-normals.png)