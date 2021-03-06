# Exploring the Drivers of the Error in the Zestimate

## Introduction
- For this 2-days project you will continue working with the zillow dataset. Continue to use the 2017 properties and predictions data for single unit / single family homes.
- In addition to continuing work on your previous project, you should incorporate clustering methodologies on this project.
- Your audience for this project is a data science team. The presentation will consist of a notebook demo of the discoveries you made and work you have done related to uncovering what the drivers of the error in the zestimate is.

## Goals
To uncover what the drivers of the error in the zestimate by three steps.<br>
    - Stage 1: Explore the Target Variable: Logerror.<br>
    - Stage 2: Clustering Logerror.<br>
    - Stage 3: Modeling and Evalution.<br>

## Key Findings and Takeaways

![clustering zillow dataset](https://github.com/Yongliang-Shi/clustering-project/blob/main/cluster_zillow.png)

- The biggest driver of the logerror is taxvlauedollarcnt.
- The zillow dataset can be clustered into 6 distinct groups based on logerror and property value.
- Medium/high nagetive logerror has an obvious cluster in LA country.
- No specific clusters of medium/high positve logerror are found based on location. 
- The top model is the LinearRegression with rfe features and it beats the baseline by redcuing 50% of te RMSE. 
- A new created categorical feature 'error_type' plays an crucial role in improving the model performance and keep the model from being overfit.

## Documents in the Repo
- README.md:
    - Overview of the zillow clustering project 
- .gitignore:
    - files to be ignored. 
- Jupyter notebooks:
    - clustering_project_zillow_walkthrough.ipynb
        - Present the most important discoveries that have been made related to the project goals.
    - explore_zillow.ipynb: 
        - Explore the interactions between independent variables and the target varibales using visualization and statistical testing.
    - cluster_zillow.ipynb: 
        - Clustering is used to explore the data and 4 combination of features have been tried. 
        - A conclusion is drawn on whether or not the clusters are helpful/useful. 
    - model_zillow.ipynb: 
        - Six different models are created and their performance is compared. 
- src:
    - acquire.py: 
        - functions to collect the zillow dataset from the codeup cloud database with approariate query. 
    - summarize.py:
        - functions used to summarize the zillow dataset.
    - prepare.py:
        - functions used to address duplicates, missing values and outliers in the zillow dataset.
        - functions used to encode, split and scale the zillow dataset.
    - wrangle_zillow.py:
        - functions to produce train, validate and test dataset ready for either exploration or modeling. 
    - features.py:
        - functions to return top k selected features based on SelectKBest and RFE classes.
    - model.py:
        - functions to group a dataset into k clusters based on K-Means
        - functions to plot residual plots. 

## Data Dictionary

| Column | Description |
| --- | ---|
| id | Autoincremented unique index id for each property |
| bathroomcnt | Number of Bathrooms; Includes halfbaths as 0.5 |
| bedroomcnt | Number of Bedrooms |
| calculatedbathnbr | Precise meaning unknown, but appears to be redundant with bathroomcnt and bedroomcnt |
| calculatedfinishedsquarefeet | Total square feet of home; doesn't include property square feet |
| finishedsquarefeet12| Unknown, but appears to be redundant with calculatedfinishedsquarefeet | 
| fips | Federal Information Processing System codes used to identify unique geographical areas | 
| fullbathcnt | Number of full bathrooms |
| latitude | The latitude of the property
| longitude | The longitude of the property |
| lotsizesquarefeet| The size of the total property lot |
| propertycountylandusecode | Unknown, but represents categorical government code |
| propertylandusetypeid |  Categorical variable describing the general type of property |
| rawcensustractandblock | Government id for each property linked to geographic location |
| regionidcity | Categorical variable identifying geographic location |
| regionidcounty | Categorical variable identifying geographic location |
| roomcnt | Number of rooms |
| yearbuilt | The year the house was built |
| structuretaxvaluedollarcnt | The tax assessed value of only the property structure in USD | 
| assessmentyear | Year that the tax value was assessed |
| landtaxvaluedollarcnt | The tax assessed value of only the land lot for the property |
| taxamount | The amount paid in taxes by the landowner in USD |
| taxvaluedollarcnt | The tax accessed value of the property in USD |
| censustractandblock | Redundant with rarcensustractandblock |
| logerror |  |
| transactiondate | Four digit year, two digit month, two digit date | 
| taxrate | Rounded derived value by dividing the taxamount by the taxvaluedollarcnt and multiplying by 100 |
| County | County the property is located in | 

## Future Work
1. Turn the clusters into Labels and further explore the each individual class.
2. Since only one cluster is modeled,  I will model the rest of the 5 clusters seprately. 
3. Turn the clusters into Features while reducing the features with high correlationship. 