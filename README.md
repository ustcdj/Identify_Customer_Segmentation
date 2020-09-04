# Identify Customer Segmentation

- [Table of Contents](#Table_of_Contents)
- [Introduction](#)
- [File Descriptions](#)
- [Acknowledgements](#)

## Introduction
The goal of this project is to help a mail-order sales company in Germany to identify segments of the population that form the core customer base. These segments can then be used to direct marketing campaigns towards audiences that should bring high expected returns.

The detailed code is in the **[`Identify_Customer_Segments.ipynb`](https://github.com/ustcdj/Identify_Customer_Segmentation/blob/master/Identify_Customer_Segments.ipynb)** notebook.

## Data

The data was provided by our partners at Bertelsmann Arvato Analytics.

## Installation

The code was developed using the Anaconda distribution of Python, versions 3.8. Python libraries used are `pandas`, `numpy`, `sklearn`, `matplotlib`, `seaborn`

## Summary of Analysis

### preprocessing

#### missing data
1. drop columns with more than 20% missing or unkown values
2. rows with 30 or more than 30 missing or unkown values are dropped.

#### categorical data
1. For binary categorical features with numeric values, keep them with no change
2. For binary categorical features with non-numeric values, re-encode the values as numbers.
3. For categorical features with three or more values, OneHotEncoder
special treated mixed-type Features

### Feature Transformation
sklearn requires that data not have missing values in order for its estimators to work properly. The NaN were imputed (SimpleImputer) using the most frequent value for each feature.  

After all features are converted to numeric, apply feature scaling (StandardScaler, mean of 0 and standard deviation of 1 ) so that the principal component vectors are not influenced by the natural differences in scale for features.

Use sklearn's PCA class to apply principal component analysis on the data
plot the ratio of variance explained by each principal component as well as the cumulative variance explained.
Perform Dimensionality Reduction

Interpret Principal Components
The 1st principle component can explain 7.78% variance, 2nd for 5.71%, 3rd 3.54% and so on.
To explain 90% variance, 105 principle components are needed.

<img src="images/variance_vs_n_pca.jpg" width=650>

the 1st PC is related to financial, movement pattern, and number of 1-2 family houses in the PLZ8 region.
The 2nd PC is related to personal (age, generation, personality, energy consumption etc.) and financial.
The 3rd PC is related to personal (personality and Gender).

### Apply Clustering to General Population
Use sklearn's KMeans class to perform k-means clustering on the PCA-transformed data and use scree plot to decide on 7 as the number of clusters to keep.

<img src="images/screeplot.jpg" width=500>

Apply the same feature wrangling, selection, engineering, imputing, feature scaling steps to the customer demographics data.
Then use PCA, and clustering from general population to obtain cluster assignments for all of the data in the customer demographics data.
Compare customer clusters to general population clusters,
It is clear from the table above, cluster 2 and 4 are overrepresented in the customer data compared to the general population.
cluster 0, 1, 3, and cluster 5 and 6 are underrepresented in the customer data compared to the general population.

<img src="images/population_vs_customer.jpg" width=600>

I looked into cluster 4 and 0:
To summarize, customers relatively popular with the mail-order company share some characters below,**
- financially well (Top eaners, Estimated household net income, high home ownership)
- Having Membership in environmental sustainability as part of youth

Customers relatively unpopular with the mail-order company share some characters below,
- low-income earners
- MINIMALIST with low financial interest
- Rational people
- Young people
- Non-dreamful people*


## Acknowledgements
Special thanks to Bertelsmann Arvato Analytics for providing the dataset.
