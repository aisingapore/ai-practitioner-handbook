# Is there a core structure for performing exploratory data analysis in a systematic way?

Contributor: Er YuYang, Senior AI Engineer

---

The purpose of this article is to have a guide to performing exploratory analysis (EDA) in a more systematic manner. This guide is designed for a generic EDA purpose and primarily focuses on tabular data. However, parts of this workflow are still applicable for unstructured data types.

## Overview
Most EDA activities should contain these blocks:

### 1. Structure investigation

This section should contains the most basic checks on the overall completeness of and level of information in the dataset. These include checking the data size and type, as well as granularity/cardinality of each table. It should also examine if the data contains any private or sensitive data.  

### 2. Content investigation

This section looks into the quality, distribution and relationships in the dataset, and need not be in this particular order.

#### 2a. Quality checks

This sub-section should cover aspects of data quality such as missing and erroneous values. The main aim is to identify potential data to drop, repair or impute.

#### 2b. Distribution checks

This sub-section should cover the understanding of each individual feature. The main aim is to find out the chracteristics of each feature, and also to uncover trends or patterns in the data.

#### 2c. Relationship checks

This sub-section should cover more in-depth analyses such as bivariate relationships between features, and between features and target. The main aim is to generate ideas for feature engineering and selection based on observed relationships.

## 1. Structure investigation

This section should be short (about less than 10 notebook cells), as it only aims to gain some insights on the size and datatype of the data. This sections does not go into the content of each variable/feature. 

When checking the datatype, organise features according to whether they are numeric/continuous or categorical. This will help to decide on suitable visualisations when performing content investigation later.

When dealing with private or sensitive data, discuss with stakeholder whether masking or removing them is a better option. When duplicate rows are present, highlight them and discuss with stakeholders on how to deal with them. Inappropriate handling of duplicate rows can results in data leakage when performing data split for model training/evaluation.

When performing granularity/cardinality checks, it is important to understand how fine or coarse each row and column is and verify whether the table is of the correct granularity per the database schema

Expected ouputs of structure investigation: 
- Raw version of data loaded in the notebook
- Size of data, whether parallel processing is needed
- Datatype of features, which features are numeric/continuous, or categorical
- (Optional) Further discussion with stakeholders on handling private/sensitive data and duplicate rows

## 2. Content investigation

### 2a. Quality checks

This sub-section should cover matters relating to data cleaning and imputation. If there are too many missing values, consider dropping the column. However if dropping is not an option, a more sophisticated method for imputing the missing value is to use the other avaiable features to predict the value of that particular column (model-based imputation/multiple imputation). 

The choice of approach for handling missing data is also influenced by the type of "missingness". There are mainly three kinds of "missingness": MCAR, MAR, MNAR (see article link at reference section). Before performing any imputation, it is highly recommended to first consult the stakeholder and understand possible reasons behind the "missingness". 

Generally, there are 4 ways to impute:
- Assign a fixed value(s) based on domain knowledge
- Simple imputation based on statistical summaries
- Model-based imputation
- Multiple imputation (see video link at reference section)

Expected ouputs:
- Cleaned version of data ready for plotting charts
- Identify data/column(s) that requires preprocessing in the datapipeline

### 2b. Distribution checks

This sub-section should cover the generation of distribution and summary statistics. Understanding properties like central tendency (mean), spread (variance) and skewness help you to spot erroneous values and potential outliers easily.

If there are district groups in the data, try grouping them and perform individual analysis for each group, in addition to the analysis for the entire dataset. Try to use looping to cover the entire possible combinations when plotting charts instead of selecting particular features combination that you preceive is useful. Investigate further if certain combination of features have interesting results. 

Perform cardinality checks on categorical features, as there could be similar category due to spelling mistake or variations. Cleaning these erroneous categories will help to reduce unnecessary noise in the analysis. It also helps to assess whether some categories are too sparse and may need to be merged for greater statistical power.

Try to link insights from the analysis to feature engineering. For example, in a parcel delivery context, if you find that number of deliveries (the target) is much higher on Mondays compared to the rest of the week, you could engineer a separate feature `is_monday` to boost the model’s performance. 

Highlight the findings on the notebook regardless of whether they are useful. This allows the reader to understand the purpose of the charts.

The analysis should cover the following:
- Summary statistics of the features
- Distribution of the features
- Feature patterns (trend)

Expected ouputs:
- Characteristics of each feature
- Spotting potential outliers and erroneous values
- Summary of the findings
- Potential feature characteristics that can be used for feature transformation in the data pipeline

### 2c. Relationship checks

This section aims to find out the relationship between feature and target so as to generate ideas for feature engineering and selection (feature importance). The goal is to identify correlated features or categories. Correlated features distort interpretability and feature importance. As such, it is worth exploring dropping or merging collinear features based on domain knowledge. 

In the scenario if there are too few features in the data, feature engineering should be explored. Conversely if there are too many features, feature importance should be explored and then dropping less important features.

If certain features have a very similar relationship to the target and are sparse, you could merge them during feature engineering to create a stronger feature. For instance, `capital_gains` and `capital_loss` can be merged into `is_investor` since if there are not many individuals who invest.

The analysis should cover the following:
- Relationships between each feature and the target
- Relationships between features

Expected ouputs:
- Identify features that are positively/negatively correlated to each other
- Identify features that are positively/negatively correlated to the target label
- Summary of the findings
- Ideas on feature engineering/selection

## Automated EDA tools
Pandas Profiling and Google Facets are two excellent tools for performing EDA. They are useful to provide initial insights before drilling down into areas of interest through manual EDA.

## References
- [EDA structure](https://miykael.github.io/blog/2022/advanced_eda/  )
- [Types of missingness](https://www-users.york.ac.uk/~mb55/intro/typemiss4.html)
- [MissForest](https://towardsdatascience.com/missforest-the-best-missing-data-imputation-algorithm-4d01182aed3)
- [Visualising distributions in seaborn](https://seaborn.pydata.org/tutorial/distributions.html)
- [Bivariate analysis in Python](https://www.analyticsvidhya.com/blog/2022/02/a-quick-guide-to-bivariate-analysis-in-python/)
- [Phi K correlation coefficient](https://towardsdatascience.com/phik-k-get-familiar-with-the-latest-correlation-coefficient-9ba0032b37e7)
- [Multiple imputation (video)](https://www.youtube.com/watch?v=LMsULWGtP2c)
- [Pandas Profiling](https://pypi.org/project/pandas-profiling/)
- [Generate reports using Pandas Profiling](https://www.analyticsvidhya.com/blog/2021/06/generate-reports-using-pandas-profiling-deploy-using-streamlit/)
- [Visualising ML datasets using Google Facets](https://towardsdatascience.com/visualising-machine-learning-datasets-with-googles-facets-462d923251b3)