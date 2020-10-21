# Exploring the Drivers of the Error in the Zestimate

## Description

For this project you will continue working with the zillow dataset. Continue to use the 2017 properties and predictions data for single unit / single family homes.<br>
In addition to continuing work on your previous project, you should incorporate clustering methodologies on this project.<br>
Your audience for this project is a data science team. The presentation will consist of a notebook demo of the discoveries you made and work you have done related to uncovering what the drivers of the error in the zestimate is.


## Goals
- To uncover what the drivers of the error in the zestimate.
    - Step 1: Explore the Target Variable: Logerror
    - Step 2: Clustering Logerror
    - Step 3: Modeling and Evalution

### Specification
- You are expected to deliver a github repository with the following contents:
- A clearly named final notebook. This notebook will be what you present and should contain plenty of markdown documentation and cleaned up code.
- A README that explains what the project is, how to reproduce your work, and your notes from project planning.
- A Python module or modules that automate the data acquisition and preparation process. These modules should be imported and used in your final notebook.


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
| logerror | Unknown |
| transactiondate | Four digit year, two digit month, two digit date | 
| taxrate | Rounded derived value by dividing the taxamount by the taxvaluedollarcnt and multiplying by 100 |
| County | County the property is located in | 

Additional columns were present in the zillow database but had greater than 20% null values and were dropped during initial consideration. 

## Data Validation
The following considerations were taken with the data:
1. Initial SQL query produced 20,364 records that met the following requirements:
    * Transaction Date between 2017-05-01 and 2017-06-30
    * Property classified as one of the following Types:
        * Single Family Residential
        * Rural Residence
        * Mobile Home
        * Townhouse
        * Condominium
        * Row House
        * Bungalow
        * Manufactured, Modular, Prefabricated Homes
        * Patio Home
        * Inferred Single Family Residence
2. Records containing 0 bathrooms, 0 bedrooms, or null square footage were dropped
3. Duplicate records were dropped. These entries may represent "back-to-back" closings on the same day between three parties.

## Key Findings and Takeaways
 - The logerror is tends to increase as the property value drops.
- The logerror can be clustered into 6 groups based on the property value and error range.¶
- No specific clusters of medium/high positve logerror are found based on longitude and latitude.
- Medium/high nagetive logerror has a obvious cluster in LA country.

## How to Reproduce

### First clone this repo

### acquire.py 
* Must include `env.py` file in directory.
    * Contact [Codeup](https://codeup.com/contact/) to request access to the MySQL Server that the data is stored on.
    * `env.py` should include the following variables
        * `user` - should be your username
        * `password` - your password
        * `host` - the host address for the MySQL Server

### prepare.py
### features.py
* The functions in prepare.py and features.py can be imported to another file. Each function is specific to the task developed during the data science pipeline of this project and may need to be altered to suit different purposes. 
### model.ipynb
* There are several specific functions embedded in the model.ipynb. They will need to be copied to a .py file in order to be used elsewhere.