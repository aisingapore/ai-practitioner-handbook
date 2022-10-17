# What are the basic core structure for performing EDA?

Contributor: Er YuYang

The purpose of this guide is to have a more systematic approach for performing EDA and some guideline or tips when performing EDA. The guide is designed for a generic EDA purpose and primarly focus on tabular data, however do note that certain parts of the workflow is still applicable for unstructured data types.

# Overview
The organization for most EDA should contain these blocks in the notebook
1. Structure investigation

    This section should investigate the data size and type. It should also examine if the data contains any private data or sensitive data.

2. Quality investigation

    This section should cover the quality of the data such as duplicate, missing and erroneous values hence identifying the potential data to drop, repair or impute.

3. Content investigation

    This section should cover the more in-depth analyses such as relationship between features. The main aim is to find if there are any trends or patterns in the data.

# Structure investigation

General guideline:

This section should be short (about less than 5 cells), it only aims to gain some insights on the size and datatype of the data. 

Sample Python command (for reference):

    a) df.shape
    b) df.info() or df.dtypes or pd.value_counts(df.dtypes)
    c) df.describe()
    d) df.head() or df.tail()

Expected ouput: 

- raw version of data
- gain some insight of the size and datatype of the data

a.) Tips for large data:

In the scenario if the data is too huge, explore using reading by sampling or chunking. Parallel processing like Dask or Ray can also help. For saving big data to disk, other file format (like Pickle, Feather, Parquest and HDF5) can help to compress to reduce the storage size.

# Quality investigation

General guideline:

This section should cover mostly on data cleaning, imputing and feature engineering/feature importance. In the scenario if there are too few features in the data, feature engineering should be explored. Conversely if there are too many features, feature importance should be explored and then dropping less important features. If there are too many missing values consider dropping the column. However if dropping is not an option, a more sophisticated method for imputing the missing value is to use the other avaiable features to predict the value of that particular column. 

Expected ouput:
- cleaned version of data ready for plotting charts

a.) Tips on handling missing values:

Non-ML techniques
- try to obtain the missing data from source
- try to estimate the missing data from the other data (based on similarity)
- do nothing (let the model handle it)

ML techniques
- impute using mean or median
- impute using most frequent or constant (eg. zero) values
- use machine learning model to impute

The choice of approach for handling missing data is also influence by the type of "missingness". There are three kinds of missing data.

- missing completely at random (MCAR)
  
  There is no relationship between the missingness of the data and any values observed or missing. There is nothing systemic going on that makes some data more likely to be missing than others.

- missing at random (MAR)

  An observation is missing has nothing to do with the missing values, but it does have to do with the values of the an individual's observed variable(s). Eg. Men are more likely to tell you their weight than women, hence weight feature is considered as MAR.

- missing not at random (MNAR)
  
  There is relationship between the inclination or natural tendency of the value to be missing and its values. Eg. Individual with the lowest eduation may have their missing value on the education feature.

b.) Tips on cleaning categorial features:

Perform a check for unique values to see if there are similar category due to spelling mistake or variations. Determine if the categorial features should be later mapped as ordinal or nominal.

Sample Python command (for reference):

    a) df.nunique()
    b) for column_name in df.columns:    
        print(df[column_name].unique())

c.) Tips on currency features:

If multiple currencies are involved as a feature, make sure to convert them into the same currency, otherwise the scale of the different currency will confuse the model or EDA findings.

# Content investigation

General guideline:

The analysis should cover the following
- distribution of the features
- feature patterns (trend)
- feature relationships (correlation)

If there are district groups in the data, try grouping them and perform individual analysis for each group, in additional to the entire data analysis. Try to use looping to cover the entire possible combinations when plotting charts that compare two features instead of selecting particular features combination that you preceive is useful. Investigate further if certain combination of features have interesting results. Highlight the findings on the notebook, regardless of whether they are useful or not, this allows the reader to understand the purpose of the charts.

Expected ouput:
- Conclusion of the findings of EDA investigation

a.) Tips on the type of plot to use:
- histogram chart (great for viewing distribution of features, and comparing between different group of data)
- stacked chart (avoid using if possible)
- line chart (commonly use in time-series data, mainly use to observed trend)
- pie chart (not recommended, use only if need to compare the size of each feature)
- box plot (useful for identify 25%-50%-75% mark only if the outlier is not extreme)
- scatter plot (useful for examining up to 3 features together, hue as the 3rd feature)
- t-SNE plot (useful for examining features above 3 and more)
- numerical correlation plot (useful if unsure which features to examine)
  - spearman's correlation
  - pearson's correlation
- categorical correlation plot (no negative correlation due the categorical features)
  - phik's correlation matrix

Side note: 
t-SNE and correlation plots are often time-consuming when generating chart. 

# References
https://miykael.github.io/blog/2022/advanced_eda/
https://www-users.york.ac.uk/~mb55/intro/typemiss4.htm
