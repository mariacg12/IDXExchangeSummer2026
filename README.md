# IDXExchangeSummer2026

Data source:
The dataset was obtained from the California Regional Multiple Listing Service (CRMLS). 
We explored listing from May 2025-May 2026 and June 2025-June 2026. 

We also used the California School District Areas 25-26 geojson dataset. 

We restricted the dataset to:
Property Type: Residential
Property Subtype: Single Family Residence

Target Variable: ClosePrice

Since housing prices are highly right-skewed the target variable was log-transformed

Data Processing:

The files required a lot of data processing, including:
Combining all the monthly datasets into one.
Filtering property type and subtype
Converting variables to correct data types.
Handling missing and duplicate values
Encoding categorical variables
Scaling numeric variables
Log transformation 
Train test split(Chronologically)

Featuring Engineering:
Feature Engineering was done in order to improve our model.

HouseAge: Difference between the year of sale and the year the property was built
BathroomPerBedroom: Relationship between the number of bathroom and bedroom
LivingAreaPerBedroom: Shows us the relationship of available space per bedroom.
LotToLivingAreaRatio: property’s lot relative to the size of the home.
HasParking: 1 and 0. 1 yes there is parking, 0 there is no parking.
HasGarage: 1 and 0. 1 yes there is a garage, 0 there is no garage.

Also transformed some skewed values like to reduce the influence of extreme values and make the distributions less skewed:
LotSizeAcres
LotSizeArea
LivingArea
LotSizeSquareFeet
AssociationFee
ParkingTotal
GarageSpaces

Outliers:
Naked Negative values in ParkingTotal and GarageSpaces were replace with missing values.

For some property values upper extreme levels were capped at 99th percentile:
LotSizeAcres
LotSizeArea
LivingArea
LotSizeSquareFeet
ParkingTotal
GarageSpaces

Features that were removed: 
CloseDate
ListingContractDate
ContractStatusChangeDate
LotSizeDimensions
BuilderName
SubdivisionName
Removing these variables reduced unnecessary dimension and avoided the model retaining very specific information.


Geographic Features:
Latitude and Longitude info was incoaprted to help represent geographic variation in property

Models:
Linear Regression
Decision Tree
Random Forest
Gradient Boosting Regressor
XGBoost
LightGBM

The first three models were used as a baseline to see our performance. Other models were used to capture more complex relationships within our data. Did some tuning in lightGBM to improve performance.

Evaluation: 
Used these metrics to evaluate the models:
R^2: variation in house prices explained by the model
RMSE: Magnitude of prediction error
MAE(For Price bands): Average abs difference between predicted and actual sale prices
MAPE: Average prediction percentage error 
MdAPE: Median Percentage prediction error
Results: 



Model
Train R2
Train RMSE
Test R2
Test RMSE
Test MAPE
Test MdAPE

0
LightGBM (Tuned)
0.911748
0.201214
0.911295
0.205190
27.366445
13.425909

1
Random Forest
0.985040
0.082845
0.906848
0.210271
31.668817
16.015618

2
Gradient Boosting
0.879763
0.234864
0.883528
0.235123
21.568911
8.417956

3
XGBoost
0.874159
0.240275
0.880872
0.237788
23.524803
11.551966

4
Linear Regression
0.821357
0.286279
0.833686
0.280962
23.497043
11.399795

5
Decision Tree
0.773220
0.322551
0.763657
0.334931
21.064567
9.460870


Best Model:

Tuned LightGBM

This model explained 91 percent of the variation in unseen housing prices. Looking at the R2 there is little evidence of overfitting.

Performance by Price Range:
The model performed the best with properties between 500k-750k, with the lowest MAPE being 10.8 percent.

Performance remained strong for home between 750k-1M, with the lowest MAPE being 11.5%

There was also high MAPE for prices below 250k, due to unexpected low prices.

Reproducing the Code:
*Note: Used Google Colab so I did not need to install the libraries*
Can download notebooks or clone my IDXExchangeSummer2026 repository
Progress in these repositories was made weekly, so can reference based on the weekly folders.
Obtain CRMLS dataset and the California School District Areas
Run preprocessing pipeline
Run Feature Engineering
Chronological training and testing datasets
Train regression models
Run Evaluations
Generate Predictions
