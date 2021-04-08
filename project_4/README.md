# **Project 4: West Nile Virus Prediction**

## **Introduction**

The West Nile virus (WNV) is a mosquito-borne illness that can cause severe neurological disease and death in humans. Originating from <a href="https://www.who.int/news-room/fact-sheets/detail/west-nile-virus">Uganda in 1937</a>,  the WNV's first recorded occurrence in the United States (US) was in New York City in 1999, and it has since spread across the entire nation to become the leading disease transmitted by mosquitoes in the US.

The disease is spread primarily by several members of the <a href="https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0227160">Culex species</a> of mosquitoes, which become infected when they feed on infected birds. These infected mosquitoes then spread the disease to humans and other animals by biting them.

Although 8 out of 10 infected people with the WNV do not develop any symptoms, about 1 in 5 of those infected develop a fever or other physical symptoms such as headaches or body aches. Fortunately, most of these people manage to recover completely.

However, 1 in 150 people develop much more severe symptoms affecting the central nervous system, including areas of the brain and the spinal cord. These result in much more severe illnesses such as high fevers, comas and even death. This is especially more pronounced in people over the age of 60 and those with pre-existing medical conditions (<a href="https://www.cdc.gov/westnile/index.html">source</a>).

## **Problem Statement** ##

With no vaccine or specific antiviral cure for the WNV, combined with an <a href ="https://www.sciencedaily.com/releases/2014/02/140210184713.htm">estimated cost of $800 million</a> in healthcare expenditures and lost productivity over a 15-year period from 1999 to 2014, it is paramount that a solution is developed to curb the spread of the WNV, with our focus placed on the city of Chicago.

Using weather, location and spray data from the Chicago Department of Public Health, we selected and trained XX classification models to determine which has the best performance in predicting whether the WNV is present in a given location. Our goal is to use our predictions to devise a strategy to deploy pesticides in WNV-hotspots to maximise pesticide effectiveness with minimal cost.


## **Executive Summary**

This project explores the <a href="https://www.kaggle.com/c/predict-west-nile-virus/">West Nile Virus Prediction Challenge</a> launched on Kaggle in a bid to predict WNV in mosquitoes across the city of Chicago. The first instances of the virus in Chicago were detected in 2002 and since 2004, the Chicago Department of Public Health has increased surveillance and control efforts in a bid to prevent transmission of this virus.

We first began with an initial cleaning of our 4 datasets - main, spray, weather and map. This was followed by an extensive exploratory data analysis where we assessed the numerical and categorical variables against the count of WNV-positive mosquitoes. The numerical weather features related to temperature, precipitation, dew point, wet bulb and average wind speed appeared to have some effect on the WNV-positive mosquito count. After conducting time series analysis on these features, these effects became more pronounced and we were able to obtain more meaningful results.

These features, as well as the weather phenomena, were then fed into our modelling process. To account for the imbalanced classes, we re-sampled the positive WNV cases using SMOTE. The models used were:

- Extra Trees
- K Nearest Neighbors
- Logistic Regression
- Random Forest
- Support Vector Machines
- XGBoost

Hyperparameter tuning was done to obtain the best training and cross-validated scores for each pipeline. We then used the best model to find the classification metrics and compared them against an AUC (Area Under The Curve) ROC (Receiver Operating Characteristics) curve to determine how much our model is capable of distinguishing between locations with and without the WNV.


## **Data dictionary**

This dictionary is not exhaustive and includes only original features from raw datasets provided. These are the final features are used to train the models.
<br>
Unlisted features with suffixes are computed from original data. For example, "rolling_14" means moving average over 14 days while "lag_7" means data is shifted by 7 days. All are of float type.

All mosquito species and weather cond(condition) features are one hot encoded from categorical data.
<br>Datasets:
1. train_weather.csv

2. test_weather.csv

|Feature|Type|Description|
|---|---|:---:|
wetbulb|int|average wet bulb|
dewpoint|int|average dew point|       
tmin|int|minimum temperature|
tavg|int|average temperature|
tmax|int|maximum temperature|
species_PIPIENS|int|mosquito species|
species_PIPIENS/RESTUANS|int|mosquito species|
species_RESTUANS|int|mosquito species|
species_SALINARIUS|int|mosquito species|
species_ERRATICUS|int|mosquito species|
species_TARSALIS|int|mosquito species|
species_TERRITANS|int|mosquito species|
ts|int|weather cond: thunderstorm|
tsra|int|weather cond: thunderstorm and rain|
vcts|int|weather cond: vicinity thunderstorm|
ra|int|weather cond: rain|
br|int|weather cond: mist|
hz|int|weather cond: haze|
preciptotal|float|24 hour precipitation in inches|
avgspeed|float|average wind speed in mile per hour|
lat|float|latitude|
long|float|longitude|
cool|int|cooling, season begins with January|
heat|int|heating, season begins with July|
wnv|int|west nile virus: 1 for present, 0 for absent|  


## **Cost-Benefit Analysis**

As part of our cost-benefit analysis, we studied research papers which highlighted that an estimated \\$778 million was incurred in both short-term and long-term, direct and indirect medical costs associated with the WNV disease, over a 15-year period from 1999 to 2014 across the US.

<a href="https://wwwnc.cdc.gov/eid/article/16/3/09-0667_article">Louisiana state data</a> showed that total epidemic costs were around \\$20 million for 329 cases, which averages to about \\$61,000 per infected case. We also explored a 2005 California economic cost analysis of the virus where the total economic impact was $2.98 million for 163 cases. This averaged the economic impact to around \\$18,282 per case, whereas vector control cost was \\$701,790. Their analysis also revealed that only <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3322011/">15 cases</a> of WNV would need to be prevented to justify the cost of the pesticide spraying.

However, their analysis is not backed up by our EDA process. Spatial data showing the spray locations did not show any noticeable reductions in the WNV-positive mosquito hot spot, thus we would recommend alternative measures to use in conjunction with the spraying.

To increase the cost-effectiveness of pesticide spraying, we advise against spraying when average wind speeds are high (i.e below 10 mph) to reduce the occurrence of <a href="https://crops.extension.iastate.edu/cropnews/2017/01/wind-speed-and-herbicide-application#:~:text=specify%2010%20MPH%20as%20the,spray%20pressure%2C%20etc.).">spray drift</a>. Also, more mosquitoes tend to be caught in traps when wind speeds are lower. Spraying should be avoided above 86°F as the higher temperatures would cause pesticide droplets to <a href="https://grdc.com.au/__data/assets/pdf_file/0024/248181/GRDC-Weather-Essentials-for-Pesticide-Application-2017.pdf">evaporate faster</a> than in cooler air. Results from the EDA showed that the virus is only prevalent during the months of July to September, and thus any efforts to reduce the mosquito population should be focused on this time period.

We recommend that The Department of Public Health consider cost-friendly measures such as eliminating mosquito breeding grounds by covering up areas where water tends to collect and remain stagnant, e.g still ponds, flower pots, rainwater barrels, etc. preventing excessive breeding after periods of heavy rainfall. This is backed up by our EDA which shows an increase in WNV counts after a spike in the precipitation total. In addition, mosquito bites can also be reduced by using mosquito repellent, and wearing long pants and long-sleeves.

Overall, our findings show that the benefits of increasing pesticide spraying may not outweigh the costs incurred. Therefore, we propose a combination of proactive (eg. spraying of pesticides)and reactive (eg. cover up mosquito breeding grounds) measures to combat the spread of the WNV in a more cost-efficient manner.


## **Conclusions and Recommendations**

Our best performing model is SVM with a test accuracy score of 85.5%. Although accuracy provides an overview of the model's performance, we need to consider the other metrics to gain more meaningful insights to guide the decisions of the Chicago Department of Public Health.

Other key metrics include the AUC, which shows that our model is 79.6% capable of distinguishing between WNV-positive and WNV-negative classes. We also note the recall rate which indicates that 80.7% of the actual WNV-positive cases were correctly classified.

Based on these 3 metrics, we conclude that our model has performed relatively well in its classification of WNV-positive mosquitoes. This, in conjunction with the findings from the EDA and cost-benefit analysis, would help the Department of Public Health in making better decisions on when and where to spray pesticides to combat the spread of the WNV-virus.
