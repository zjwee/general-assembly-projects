# Project 2: Ames Housing Prices

## Problem Statement

**Scenario:**  
Prospective Ames home buyers/sellers need an estimate of house prices given the features of the house.

Home buyers will want to know if the house on sale is cheaper than other houses on the market with similar features.

Home sellers will want to know what features of their house can be improved upon to raise its selling price.

**Task:**  
Create a Linear Regression model to accurately predict house prices, given Ames housing [data](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).

Select 25-30 features out of 80, and refine model using cross validation and regularization.

Test the final Linear Regression model against unseen test data on [Kaggle](https://www.kaggle.com/c/dsi-us-6-project-2-regression-challenge/overview) based on Root Mean Squared Error (RMSE) between predicted and actual sale prices.

## Executive Summary

Out of the original 80 features, 30 categorical and numeric features were selected based on exploratory data analysis and iterative model generation/evaluation. Interaction features were then created based on these top 30 features.

Out of all the interaction features generated above, the top 30 were selected for the final model. They include combinations of the following individual features:

**Nominal:**<br>
Bldg Type, Foundation, Neighborhood, Exterior 1st, Condition 1, Sale Type

**Ordinal:**<br>
Overall Qual, Overall Cond, Bsmt Exposure, BsmtFin Type 1, Kitchen Qual, Bsmt Qual, Fireplace Qu

**Discrete:**<br>
Year Built

**Continuous:**<br>
Gr Liv Area, Total Bsmt SF

The final model is a Ridge Regression model optimized with cross validation, and it acheived RMSE of 29167 (Private Score) and 24979 (Public Score) on Kaggle.

Prospective Ames home buyers/sellers should pay attention to Gr Liv Area, Total Bsmt SF, Overall Qual and Overall Cond as these features are highly correlated with Sale Price. Home buyers/sellers should expect house prices to be higher if these features' values are higher.

Conversely, Condition 1: Artery (adjacency to an arterial street), BsmtFin Type 1: Unf (unfinished basement), and Fireplace Qu: NA (no fireplace) are negatively correlated with Sale Price. Sellers who wish to maximise their selling prices should be aware of these negative qualities of their house.

## Methodology

1. Clean and explore data to select first set of features for modelling
2. Split original training data into sub train / test (holdout) sets
3. Scale and binarize features as necessary
4. Create Linear Regression model using first feature set
5. Regularize Linear Regression model using Ridge, Lasso and Elastic Net regression
6. Score Linear Regression based on RMSE of cross validation and prediction of holdout test dataset
7. Analyse top coefficients of regression models to fine-tune feature engineering and create new feature sets
8. Repeat steps 4-7 on subsequent feature sets
9. Select best performer for submission

## Data Dictionary

Full details are available on this [link](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).

|Feature        |Type       |Description                |
|---------------|-----------|---------------------------|
|MS SubClass    |Nominal    |Identifies the type of dwelling involved in the sale|
|MS Zoning      |Nominal    |Identifies the general zoning classification of the sale|
|Street         |Nominal    |Type of road access to property|
|Alley          |Nominal    |Type of alley access to property|
|Land Contour   |Nominal    |Flatness of the property|
|Lot Config     |Nominal    |Lot configuration|
|Neighborhood   |Nominal    |Physical locations within Ames city limits|
|Condition 1    |Nominal    |Proximity to various conditions|
|Condition 2    |Nominal    |Proximity to various conditions (if more than one is present)|
|Bldg Type      |Nominal    |Type of dwelling|
|House Style    |Nominal    |Style of dwelling|
|Roof Style     |Nominal    |Type of roof|
|Roof Matl      |Nominal    |Roof material|
|Exterior 1st   |Nominal    |Exterior covering on house|
|Exterior 2nd   |Nominal    |Exterior covering on house (if more than one material)|
|Mas Vnr Type   |Nominal    |Masonry veneer type|
|Foundation     |Nominal    |Type of foundation|
|Heating        |Nominal    |Type of heating|
|Central Air    |Nominal    |Central air conditioning|
|Garage Type    |Nominal    |Garage location|
|Misc Feature   |Nominal    |Miscellaneous feature not covered in other categories|
|Sale Type      |Nominal    |Type of sale|
|Lot Shape      |Ordinal    |General shape of property|
|Utilities      |Ordinal    |Type of utilities available|
|Land Slope     |Ordinal    |Slope of property|
|Overall Qual   |Ordinal    |Rates the overall material and finish of the house|
|Overall Cond   |Ordinal    |Rates the overall condition of the house|
|Exter Qual     |Ordinal    |Evaluates the quality of the material on the exterior|
|Exter Cond     |Ordinal    |Evaluates the present condition of the material on the exterior|
|Bsmt Qual      |Ordinal    |Evaluates the height of the basement|
|Bsmt Cond      |Ordinal    |Evaluates the general condition of the basement|
|Bsmt Exposure  |Ordinal    |Refers to walkout or garden level walls|
|BsmtFin Type 1 |Ordinal    |Rating of basement finished area|
|BsmtFin Type 2 |Ordinal    |Rating of basement finished area (if multiple types)|
|Heating QC     |Ordinal    |Heating quality and condition|
|Electrical     |Ordinal    |Electrical system|
|Kitchen Qual   |Ordinal    |Kitchen quality|
|Functional     |Ordinal    |Home functionality (Assume typical unless deductions are warranted)|
|Fireplace Qu   |Ordinal    |Fireplace quality|
|Garage Finish  |Ordinal    |Interior finish of the garage|
|Garage Qual    |Ordinal    |Garage quality|
|Garage Cond    |Ordinal    |Garage condition|
|Paved Drive    |Ordinal    |Paved driveway|
|Pool QC        |Ordinal    |Pool quality|
|Fence          |Ordinal    |Fence quality|
|Year Built     |Discrete   |Original construction date|
|Year Remod/Add |Discrete   |Remodel date (same as construction date if no remodeling or additions)|
|Bsmt Full Bath |Discrete   |Basement full bathrooms|
|Bsmt Half Bath |Discrete   |Basement half bathrooms|
|Full Bath      |Discrete   |Full bathrooms above grade|
|Half Bath      |Discrete   |Half baths above grade|
|Bedroom AbvGr  |Discrete   |Bedrooms above grade (does NOT include basement bedrooms)|
|Kitchen AbvGr  |Discrete   |Kitchens above grade|
|TotRms AbvGrd  |Discrete   |Total rooms above grade (does not include bathrooms)|
|Fireplaces     |Discrete   |Number of fireplaces|
|Garage Yr Blt  |Discrete   |Year garage was built|
|Garage Cars    |Discrete   |Size of garage in car capacity|
|Mo Sold        |Discrete   |Month Sold (MM)|
|Yr Sold        |Discrete   |Year Sold (YYYY)|
|Lot Frontage   |Continuous |Linear feet of street connected to property|
|Lot Area       |Continuous |Lot size in square feet|
|Mas Vnr Area   |Continuous |Masonry veneer area in square feet|
|BsmtFin SF 1   |Continuous |Type 1 finished square feet|
|BsmtFin SF 2   |Continuous |Type 2 finished square feet|
|Bsmt Unf SF    |Continuous |Unfinished square feet of basement area|
|Total Bsmt SF  |Continuous |Total square feet of basement area|
|1st Flr SF     |Continuous |First Floor square feet|
|2nd Flr SF     |Continuous |Second floor square feet|
|Low Qual Fin SF|Continuous |Low quality finished square feet (all floors)|
|Gr Liv Area    |Continuous |Above grade (ground) living area square feet|
|Garage Area    |Continuous |Size of garage in square feet|
|Wood Deck SF   |Continuous |Wood deck area in square feet|
|Open Porch SF  |Continuous |Open porch area in square feet|
|Enclosed Porch |Continuous |Open porch area in square feet|
|3Ssn Porch     |Continuous |Three season porch area in square feet|
|Screen Porch   |Continuous |Screen porch area in square feet|
|Pool Area      |Continuous |Pool area in square feet|
|Misc Val       |Continuous |$Value of miscellaneous feature|
|SalePrice      |Continuous |Sale price $$|



