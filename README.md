# MBTS Wildfire Analysis

## Introduction

This is the process by which I attempted to generate a Multiple Linear Regression model to predict the size of wildfires across the country. The various models generated were done using geographical and climate data for each wildfire, though in the end none of the models were successful. Instead, I ended up performing some statistical testing on the data.

#### Datasets Used
1. Monitoring Trends in Burn Severity (MTBS) Fire Occurrence Dataset
2. National Oceanic and Atmospheric Administration’s (NOAA) Global Historical Climatology Network
3. Ecoregion Spatial data from the Environmental Protection Agency (EPA)

#### Notebooks in the repository
1. 01_Wildfire Data Exploration - The first notebook created to clean, explore, and analyze the data. Started a few rounds of modeling.
2. 02_Spacial Join - A notebook created to spatially join: the weather data with the monitoring location data, the monitoring data with the ecoregion data, and both the ecoregion and weather data with the fire dataset
3. 03_Climate Data - A notebook used to collect and clean the climate data, and then transform the cliamte data into a usable format for further analysis (converted to CSVs).
4. 04_Wildfire Modeling - A notebook created to generate various linear regression models on the data, using different predictor variables or subsets of the data.
5. 05_Statistical Testing and Visualizations - The final notebook created to perform statistical testing on the data, as well as generate some additional visualizations for the blog post, presentation, and ReadMe file.

## EDA Results
After cleaning and joining the various datasets together, I conducted some exploratory data analysis, just to get a feel for what I was dealing with.
1. The number of fires have been increasing since since 1984
2. Surprisingly, Florida had the most number of fires, but when looking closer at this, a majority of the fires in Florida were prescribed, not wild.
3. The average prescribed fire burned about **2,000 acres**, while the average wildfire burned closer to **9,000 acres**.
4. Most fires occur in the summer months and are usually out west in states like Oregon, California, and Idaho. There are a large number of fires that also occur in spring months (mainly March and April), but these are pretty confined to Florida and Kansas. The fires out west also tend to be four to five times larger than fires in Florida.
5. As far as climate trends are concerned, even though the trends were not as clear as I expected, there were a few takeaways. First, in some ecoregions, especially where there are on average larger fires, the acres burned tends to increase as the average minimum and maximum 3-month temperatures increase. Second, though rainfall doesn't have as much an affect on the size of the fire, we can see that the more rainfall over a three-month period, the less likely a chance of fire.

## Modeling
With these insights in mind, I went on to generate a predictive model for the dataset. The goal was to create a multiple-linear regression model that would predict the size of a fire based on a variety of geographic and climate data.

Unfortunately, this didn’t pan out so well. I went through every iteration of predictor variables and data subsets I could think of that might prove fruitful, but to no avail. Almost all the models I generated didn’t have an R-squared value above 0.1, and those that did, were trained on either older portions of the whole dataset (1990-2000) or on fires with burn areas that were considered outliers (above 50K in size). Considering this, I had to give up on generating a model that would predict fire size.

After further investigative research, there are a handful of other factors at play that I not only didn’t consider, but didn’t have the data for either. These factors include topography, fire-weather conditions (not conditions prior to the ignition, but the weather conditions during the fire), human-response to fire, and fuel-type, to name a few. The only one of these factors I may have been able to add to my model dataset was the fire-weather conditions, but the MTBS dataset didn’t include a fire containment date, so I couldn’t accurately grab fire-weather conditions for each fire.

## Statistical Testing
However, so as not to walk away from this project completely empty handed, I choose to conduct a few rounds of statistical testing.

#### My first question: Do some ecoregions and/or states experience larger 'Wildfires' than others?
I used a Tukey’s Range test to determine that yes, some states and ecoregions experience larger wildfires than others.
1. As far as states go, Idaho, Oregon, and Nevada seem to be the three states with the largest average wildfires (between 12,000 and 14,000 acres) and Florida has the smallest average wildfires (just over 2,000 acres).
2. When looking at ecoregions, the Northern Basin and Range and the Idaho Batholith experience the largest average wildfire, at around 15,000 acres, while the Central Appalachians and the Southern Coastal Plain experience the smallest average wildfire, at around 2,500 acres. The other 6 ecoregions fall somewhere in the middle.

#### My second question: Are wildfires getting bigger?
Using a Welch’s T-test, and comparing three year averages from 1986-1988 and 2016-2018, I was again able to reject the null hypothesis.
Fires are getting larger. The average fire between 2016 and 2018 was 6,000 acres bigger than the average fire between 1986 and 1988.

#### And finally, where are wildfires getting bigger and becoming more frequent.
Using a series of Welch’s T-tests, I learned which states and regions have shown a statistically significant increase (or decrease) in wildfire size, as well as which have exhibited an increase in wildfire frequency.
1. For states: Nevada, California, Oregon, Colorado, Utah, New Mexico, Arizona, and Florida all show a statistically significant increase in wildfire size compared to historical wildfire data, the largest being in Nevada, with an average increase of 14,382 acres. Both West Virginia and Minnesota have experienced a negative trend in wildfire size.
2. For regions: Mediterranean California, Cold Deserts, Western Cordillera, Everglades, Upper Gila Mountains, and the Western Sierra Madres Piedmont regions of the U.S. have experienced a statistically significant increase in wildfire size compared to historical wildfire data, the largest being in the Mediterranean California region, with an average increase of 11,075 acres. The Mixed Wood Shield region experienced a negative trend in wildfire size.

Though I didn't conduct statistical testing on the number of fires experienced, it worth noting the following states and regions that are experiencing (on average) more wildfires per year than they were 30 years ago:
1. Nevada: 23 more fires per year
2. Colorado: 10.7
3. New Mexico: 15.4
4. Arizona: 23.4
5. Cold Deserts: 49.4
6. Western Cordillera: 28
7. Upper Gila Mountains: 21

## Conclusion
Even though my predictive models didn’t turn out as well as I’d hoped, I was still able to come away from this dataset with some valuable insights. With the effects of climate change starting to be felt by more and more of the population, it’s important to determine which areas in the country are experiencing more frequent and larger wildfires than they were in the past. By knowing which regions are at higher risk of wildfires, governments can better allocate funds to deal with wildfires in those regions and individuals living in high risk states and regions can decide for themselves if it would be better to move to other parts of the country with less risk of wildfire.
