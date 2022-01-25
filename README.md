# MTA-EDA-Metis

# Using MTA Turnstile Data to Measure Foot Traffic Near CUNY Campuses

## Abstract
This project used MTA Turnstile Data as a proxy for foot traffic to look at which five City University of New York (CUNY) campuses would be the best sites for new Covid-19 clinics.

## Design
In this scenario, The City University of New York (CUNY) and the New York City Department of Health and Mental Hygiene (NYC DOHMH) are partnering to create five COVID-19 clinics aimed at serving CUNY students, faculty, and staff, as well as members of the surrounding community, during the Spring 2022 semester. These clinics will be located at five CUNY campuses and provide Covid-19 testing and vaccinations.

Rather than locating the clinics at a flagship campus in each Borough (Brooklyn College in Brooklyn, Queens College in Queens, the College of Staten Island on Staten Island, City College in Manhattan, and Lehman College in the Bronx), this project looks at subway ridership as a way of determining where to locate the new clinics. By using counts of entrances and exits recorded at nearby subway station turnstiles, we are able to estimate the foot traffic around each campus, and thus see which locations would make the new clinics the most acessible to the most people.

## Data
The Data used for this analysis came from three sources:
1. MTA Turnstile data (http://web.mta.info/developers/turnstile.html) Lists counts of entrances and exits at each turnstile at each subway station
2. NYC Transit Subway Entrance and Exit data (https://data.ny.gov/Transportation/NYC-Transit-Subway-Entrance-And-Exit-Data/i9wp-a4ja
) Lists latitudes and longitudes for each subway station
3. CUNY Campus Locations (https://data.ny.gov/Education/City-University-of-New-York-CUNY-University-Campus/irqs-74ez/data) Lists latitudes and longitudes for 25 CUNY campuses

MTA Turnstile data was limited to the months spanning the Fall 2021 Semester, August through December, as a way of predicting traffic patterns during the spring semester. The most recent semester was chosen (rather than the Spring 2021 semester) because it is likely that Covid-19 protocols affecting traffic flow were the most similar in the most recent past. Compiling the data for five months created an initial database of 4,409,348 rows




## Algorithms

## Tools

## Ccommunication
