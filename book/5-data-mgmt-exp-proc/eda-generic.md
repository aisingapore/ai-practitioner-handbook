# What are the basic core structure for performing EDA and optional blocks for specific AI domain or specific use case?

Contributor: Er YuYang

The purpose of this guide is to have a more systematic approach for performing EDA and some guideline or tips when performing EDA. The guide is design for a generic EDA purpose, and sections should be applied when it is applicable.

# Overview
The organization for most EDA should contain these blocks in the notebook
1. Structure investigation

    This section should cover the understanding the size of the data and data type. Also, examining if the data contains non-PDPA compliance data or other sensitive data.

2. Quality investigation

    This section should cover the quality of the data such as duplicate, missing and erroneous values hence identifying the potential data to drop, repair or impute.

3. Content investigation

    This section should cover the more in-depth analysis such as the relationship for the features. The main aim is to find if there are any trends or patterns in the data.

# Structure investigation

General guideline:

This section should be short (about less than 5 cells), it only aims the gain some insight of the size and datatype of the data. 

Sample python command (for reference):

    a) df.shape
    b) df.info() or df.dtypes or pd.value_counts(df.dtypes)
    c) df.describe()
    d) df.head() or df.tail()

Expected ouput: 

- raw version of data
- gain some insight of the size and datatype of the data

Tips for large data:

In the scenario if the data is too huge, explore using reading by sampling or chunking. Parallel processing like Dask or Ray can also help. For saving big data to disk, other file format (like Pickle, Feather, Parquest and HDF5) can help to compress to reduce the storage size.

# Quality investigation

General guideline:

This section should cover mostly on data cleaning, imputing and feature engineering/feature importance. In the scenario if there are too few features in the data, feature engineering should be explored. Vice versa if there are too many features, feature importance should be explored and then dropping less important features. If there are too many missing values consider dropping the column. However if dropping is not an option, a complex method for imputing the missing value is to use the other avaiable features to predict the value of that particular column. 

Expected ouput:
- cleaned version of data ready for plotting charts

Tips on handling missing values (common techniques):
- do nothing (let the model handle it)
- impute using mean or median
- impute using most frequent or constant (eg. zero) values
- use machine learning model to impute

Tips on cleaning categorial features:

Perform a unique check to see if there are similar category but is categorised differently due to spelling mistake. Determine if the categorial features should be later mapped as ordinal or nominal.

Sample python command (for reference):

    a) df.nunique()
    b) for column_name in df.columns:    
        print(df[column_name].unique())

Tips on currency features:

If multiple currencies are involved as a feature, make sure to convert them into the same currency, otherwise the scale of the different currency will confused the model or EDA findings.

# Content investigation

General guideline:

The analysis should cover the following
- distribution of the features
- features patterns (trend)
- features relationship (correlation)

If there are district groups of data in the data, try grouping these data and performed individual analysis for each group, in additional to these entire data analysis. Try to use looping to cover the entire possible combinations when plotting charts that compare two features instead of selecting particular features combination that you preceive is useful. Investigate further if certain combination of features have interesting results. Highlight the findings (whether there are useful finding or not) on the notebook as well, this allows the reader to understand the purpose of the charts.

Expected ouput:
- Conclusion of the findings of EDA investigation

Tips on the type of plot to use:
- histogram chart (great for viewing distribution of features, and comparing btw different group of data)
- stacked chart (avoid using if possible)
- line chart (commonly use in time-series data, mainly use to observed trend)
- pie chart (not recommended, use only if need to compare the size of each feature)
- box plot (useful for identify 25%-50%-75% mark only if the outlier is not extreme)
- scatter plot (useful for examining up to 3 features together, hue as the 3rd feature)
- tsne plot (useful for examining features above 3 and more)
- coorelation plot (useful if unsure which features to examine)

Side note: 
tsne and coorelation plot often time consuming when generating chart. 

# References
https://miykael.github.io/blog/2022/advanced_eda/