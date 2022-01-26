# MTA-EDA-Metis

# Using MTA Turnstile Data to Measure Foot Traffic Near CUNY Campuses

## Abstract
This project used MTA Turnstile Data as a proxy for foot traffic to look at which five City University of New York (CUNY) campuses would be the best sites for new Covid-19 clinics. I first paired latitude and longitude data for MTA subway stations and CUNY campuses to focus on the subset of stations and campuses within half a mile of each other. I used this subset of MTA stations to limit 5 months of MTA Turnstile Data to only the relevant stations, using Levenshtein distances to match the inconsistent station names in each list. After calcuating the entrance and exit counts for each turnstile for each each date in the data set, I summed the entrance and exit data for each station as a way of measuring total passersby for the station on each date. I found the mean of the total for each station, as a way of estimating the average number of passersby on a given day for that station, and then pooled the averages of nearby stations to find an estimate of the average foot traffic near each CUNY campus. The five campuses with the most foot traffic were: Guttman Community College, The School of Journalism, The Graduate Center, The School of Professional Studies, and The School of Labor and Urban Studies. These schools are all located less than 0.5 miles from 8 or more subway stations, contributing to their high foot traffic measures. After completing this analysis, I recommend the locations of the new clinics be balanced for both geographic spread and proximity to MTA subway stations.

## Design
In this scenario, The City University of New York (CUNY) and the New York City Department of Health and Mental Hygiene (NYC DOHMH) are partnering to create five COVID-19 clinics aimed at serving CUNY students, faculty, and staff, as well as members of the surrounding community, during the Spring 2022 semester. These clinics will be located at five CUNY campuses and provide Covid-19 testing and vaccinations.

Rather than locating the clinics at a flagship campus in each Borough (Brooklyn College in Brooklyn, Queens College in Queens, the College of Staten Island on Staten Island, City College in Manhattan, and Lehman College in the Bronx), this project looks at subway ridership as a way of determining where to locate the new clinics. By using counts of entrances and exits recorded at nearby subway station turnstiles, we are able to estimate the foot traffic around each campus, and thus see which locations would make the new clinics the most acessible to the most people.

## Data
The Data used for this analysis came from three sources:
1. MTA Turnstile data (http://web.mta.info/developers/turnstile.html) Lists counts of entrances and exits at each turnstile at each subway station
2. NYC Transit Subway Entrance and Exit data (https://data.ny.gov/Transportation/NYC-Transit-Subway-Entrance-And-Exit-Data/i9wp-a4ja) Lists latitudes and longitudes for each subway station
3. CUNY Campus Locations (https://data.ny.gov/Education/City-University-of-New-York-CUNY-University-Campus/irqs-74ez/data) Lists latitudes and longitudes for 25 CUNY campuses

The MTA Turnstile data was limited to the months spanning the Fall 2021 Semester, August through December, as a way of predicting traffic patterns during the spring semester. The most recent semester was chosen (rather than the Spring 2021 semester) because it is likely that Covid-19 protocols affecting traffic flow were the most similar in the most recent past. Compiling the data for five months created an initial database of 4,409,348 rows.

## Algorithms/Methodology
1. Used Metis-provided Python script used to download 5 months of data and format it as a SQLite database
2. Explored the database in DB Browswer for SQLite and realized I would not be able to have the time granularity I had hoped
3. Loaded all three data sets into Pandas
4. Calculated Haversine distance from latitude and longitude dataframes for stations and campuses
5. Used new distance dataframe to limit station location dataframe and campus location dataframe to only stations and campuses < 0.5 miles from each other
7. Calculated Levenshtein distances between station names in the turnstile dataframe and the station names in the limited station location dataframe and added the station location name that best matched to each row of the turnstile datagrame (this was very computationally taxing and if I were to do this again I would do this differently, but it took so long to run that I just worked with the output it generated!)
8. Inner joined the limited station location dataframe with the turnstile dataframe using the Levenshtein distances calculations (and then manually corrected for mismatched stations) to limit the data to only stations near CUNY campuses
9. Grouped the 


## Tools
1. DB Browser for SQLite -- Explore MTA turnstile data
2. Pandas -- Exploring, manipulating, aggregating, and merging dataframes
3. Numpy and Scikit-learn -- Calculating Haversine distance between campuses and subway stations using latitude and longitude data 
4. Geopandas -- Plotting latitude and longitude data on a map of the 5 Boroughs
5. Matplotlib -- Plotting turnstile averages
6. Fuzzywuzzy -- Calculating Levenshtein distances between strings to match station names following different naming conventions across the datasets

## Communication
