# MTA-EDA-Metis

# Using MTA Turnstile Data to Determine Covid-19 Clinic Locations

## Abstract
This project used MTA Turnstile Data as a proxy for foot traffic to look at which five City University of New York (CUNY) campuses would be the best sites for new Covid-19 clinics. By pairing latitude and longitude data with turnstile count data, I was able to limit my focus to only stations located less than 0.5 miles from a CUNY campus, and only CUNY campuses located less than 0.5 miles from a MTA subway station. I calculated the average subway ridership for each station on a given day during the Fall 2021 semester, and summed the averages for all the stations near each CUNY campus to estimate the daily foot traffic for that campus. The five campuses with the highest estimated foot traffic were: Guttman Community College, The School of Journalism, The Graduate Center, The School of Professional Studies, and The School of Labor and Urban Studies. These schools are all located less than 0.5 miles from 8 or more subway stations, contributing to their high foot traffic estimates. After completing this analysis, I recommend the locations of the new clinics be balanced for both geographic spread and proximity to MTA subway stations.

## Design
In this scenario, The City University of New York (CUNY) and the New York City Department of Health and Mental Hygiene (NYC DOHMH) are partnering to create five COVID-19 clinics aimed at serving CUNY students, faculty, and staff, as well as members of the surrounding community, during the Spring 2022 semester. These clinics will be located at five CUNY campuses and provide Covid-19 testing and vaccinations.

Rather than locating the clinics at a flagship campus in each Borough (Brooklyn College in Brooklyn, Queens College in Queens, the College of Staten Island on Staten Island, City College in Manhattan, and Lehman College in the Bronx), this project looks at subway ridership as a way of determining where to locate the new clinics. By using counts of entrances and exits recorded at nearby subway station turnstiles, we are able to estimate the foot traffic around each campus, and thus see which locations would make the new clinics the most acessible to the most people.

## Data
The Data used for this analysis came from three sources:
1. MTA Turnstile data (http://web.mta.info/developers/turnstile.html) Lists counts of entrances and exits at each turnstile at each subway station
2. NYC Transit Subway Entrance and Exit data (https://data.ny.gov/Transportation/NYC-Transit-Subway-Entrance-And-Exit-Data/i9wp-a4ja) Lists latitudes and longitudes for each subway station
3. CUNY Campus Locations data (https://data.ny.gov/Education/City-University-of-New-York-CUNY-University-Campus/irqs-74ez/data) Lists latitudes and longitudes for 25 CUNY campuses

The MTA Turnstile data was limited to the months spanning the Fall 2021 Semester, August through December, as a way of predicting traffic patterns during the spring semester. The most recent semester was chosen (rather than the Spring 2021 semester) because it is likely that Covid-19 protocols affecting traffic flow were the most similar in the most recent past. Compiling the data for five months created an initial database of 4,409,348 rows.

## Methodology
1. Used Metis-provided Python script used to download 5 months of data and format it as a SQLite database
2. Explored the database in DB Browswer for SQLite and realized I would not be able to have the time granularity I had hoped
3. Loaded all three data sets into Pandas and cleaned them
4. Calculated Haversine distance from latitude and longitude dataframes for stations and campuses
5. Used new distance dataframe to limit station location dataframe and campus location dataframe to only stations and campuses < 0.5 miles from each other
7. Calculated Levenshtein distances between station names in the turnstile dataframe and the station names in the station location dataframe and added the station location name that best matched to each row of the turnstile dataframe (this was very computationally taxing and if I were to do this again I would do this differently, but it took so long to run that I just worked with the output it generated!)
8. Inner joined the limited station location dataframe with the turnstile dataframe using the Levenshtein distance calculations (and then manually corrected for mismatched stations) to limit the turnstile data to only stations near CUNY campuses
9. Found the sum of all turnstiles at each station on each date at each time
10. Found the number of exits tallied each day for each station by subtracting the min from the max of the summed station exit data for that day (necessary because the counts don't reset each date or time period but are cumulative; I considered subtracting the earliest count on each day from the latest count, but figured finding the range was functionally equivalent for my purposes)
11. Found the number of entrances tallied each day for each station by subtracting the min from the max of the summed station entrance data for that day
12. Summed the entrance and exit data for each station for each day, giving an estimate of total foot traffic in that station for an entire day
13. Took the average of the total daily foot traffic for each station for all five months
14. Pooled the average daily foot traffic for all the stations near each CUNY campus, and used that as an estimate of total daily foot traffic for that campus
15. Sorted the data to find the 5 CUNY campuses with the most average daily foot traffic
16. Plotted and mapped the data for presenting

## Tools
1. DB Browser for SQLite -- Explore MTA turnstile data
2. Pandas -- Exploring, manipulating, aggregating, and merging dataframes
3. Numpy and Scikit-learn -- Calculating Haversine distance between campuses and subway stations using latitude and longitude data 
4. Geopandas -- Plotting latitude and longitude data on a map of the 5 Boroughs
5. Matplotlib -- Plotting turnstile averages
6. Fuzzywuzzy -- Calculating Levenshtein distances between strings to match station names following different naming conventions across the datasets

## Communication
[Metis_EDA_Presentation.pdf](https://github.com/dr-dronkos/MTA-EDA-Metis/files/7938715/Metis_EDA_Presentation.pdf)

