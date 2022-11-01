# What are the basic core structure for performing EDA?

Contributor: Er YuYang

The purpose of this guide is to have a more systematic approach and guideline or tips when performing EDA. The guide is designed for a generic EDA purpose and primarly focus on tabular data, however do note that certain parts of the workflow is still applicable for unstructured data types.

# Overview
The organization for most EDA should contain these blocks in the notebook

1. Structure investigation

    This section should contains the most basic checks on the overall completeness and level of information of the dataset. These includes the checking the data size and type as well as granularity/cardinality of each table. It should also examine if the data contains any private or sensitive data.  

2. Content investigation
    
    This section look into the quality, distribution and relationships in the dataset, and need not be in this particular order.

    2a) Quality checks

    This sub-section should cover the quality of the data such as missing and erroneous values. The main aim is to identify the potential data to drop, repair or impute.

    2b) Distribution checks

    This sub-section should cover the understanding of each individual features. The main aim is to find out the chararterics of the features and also if there are any trends or patterns in the data.

    2c) Relationship checks

    This sub-section should cover the more in-depth analyses such as relationship between feature vs feature and features vs target. The main aim is to generate ideas for feature engineering and selection based on the relationship.

# Structure investigation

General guideline:

This section should be short (about less than 10 cells), it only aims to gain some insights on the size and datatype of the data and do not go into the content of each variable/feature. 

When checking the datatype, organise the features according to whether they are numeric/continuous, or categorical, this will helps to decide on suitable visualisations when performing content investigation later.

When dealing with private or sensitive data, discuss with stakeholder whether masking or removing them is a better option. When duplicate rows are present, highlight those and discuss with stakeholder on how to deal duplicate rows as these rows will introduce data leakage when performing data split for model training/evaluation.

When performing granularity/cardinality checks, it is important to understand how fine or coarse each row and column is and verify whether the table is of the correct granularity per the database schema

Expected ouput: 

- raw version of data loaded in the notebook
- size of data, whether parallel processing is needed
- datatype of features, which features are numeric/continuous, or categorical
- (optional) further discussion with stakeholder on handling private/sensitive data and duplicate rows

# Content investigation

## 2a) Quality checks

General guideline:

This sub-section should cover mostly on data cleaning and imputing. If there are too many missing values consider dropping the column. However if dropping is not an option, a more sophisticated method for imputing the missing value is to use the other available features to predict the value of that particular column (model-based imputation/multiple imputation). 

The choice of approach for handling missing data is also influence by the type of "missingness". There are mainly three kinds of "missingness": MCAR, MAR, MNAR (see article link at reference section). Before performing any imputation, it is highly recommended to first consult the stakeholder and understand possible reasons behind the missingness. 

Generally, there are 4 ways to impute
- assign a fixed value(s) based on domain knowledge
- simple imputation based on statistical summaries
- model-based imputation
- multiple imputation (see video link at reference section)

Expected ouput:
- cleaned version of data ready for plotting charts
- identify data/column(s) that requires preprocessing in the datapipeline

## 2b) Distribution checks

General guideline:

This sub-section should cover generating the distribution and summary statistics. Understanding variable properties like central trends (mean), spread (variance) and skewness help you to spot erroneous values and potential outliers easily.

If there are district groups in the data, try grouping them and perform individual analysis for each group, in additional to the entire data analysis. Try to use looping to cover the entire possible combinations when plotting charts instead of selecting particular features combination that you preceive is useful. Investigate further if certain combination of features have interesting results. 

Perform cardinality check on categorical features as there could be similar category due to spelling mistake or variations. Cleaning these erroneous category will help to reduce unnecessary noise in the analysis. It also helps to assess whether some categories are too sparse and may need to be merged for greater statistical power.

Try to link the insights from the analysis to feature engineering. For example, if you find that number of deliveries (the target) is much higher on Mondays compared to the rest of the week, you could engineer a separate feature is_monday to boost the model’s performance. 

Highlight the findings on the notebook, regardless of whether they are useful or not, this allows the reader to understand the purpose of the charts.

The analysis should cover the following
- summary statistics of the features
- distribution of the features
- feature patterns (trend)

Expected ouput:
- characteristics of each feature
- spotting potential outliers and erroneous values
- summary of the findings
- identify which categorial features to be mapped as ordinal or nominal
- identify potential characteristics in the feature that can extracted further for feature transforming in the datapipeline

## 2c) Relationship checks

General guideline:

To find out the relationship between feature and target so as to generate ideas for feature engineering and selection (feature importance). The goal is to identify multicollinear features or categories. Correlated features distort interpretability and feature importance, droping or merging some collinear features should be explored based on domain knowledge. 

In the scenario if there are too few features in the data, feature engineering should be explored. Conversely if there are too many features, feature importance should be explored and then dropping less important features.

If certain features have a very similar relationship to the target and are sparse, you could merge them during feature engineering to create a stronger feature. For instance, capital_gains and capital_loss can be merged into is_investor since if there are not many individuals who invest.

The analysis should cover the following
- relationships between each feature and the target
- relationships between features

Expected ouput:
- which features are postive/negative correlated to each other
- which features is more/less important to target label
- summary of the findings
- ideas on feature engineering/selection for feature transforming in the datapipeline

# Others
Pandas profiling and Google Facets are 2 excellent tools for performing EDA.

Pandas profiling: 
- https://www.analyticsvidhya.com/blog/2021/06/generate-reports-using-pandas-profiling-deploy-using-streamlit/
- https://pypi.org/project/pandas-profiling/

Google Facets: 
- https://towardsdatascience.com/visualising-machine-learning-datasets-with-googles-facets-462d923251b3
- https://github.com/PAIR-code/facets

# References
## Article link
https://miykael.github.io/blog/2022/advanced_eda/

https://www-users.york.ac.uk/~mb55/intro/typemiss4.htm

https://towardsdatascience.com/missforest-the-best-missing-data-imputation-algorithm-4d01182aed3

https://seaborn.pydata.org/tutorial/distributions.html

https://www.analyticsvidhya.com/blog/2022/02/a-quick-guide-to-bivariate-analysis-in-python/

https://towardsdatascience.com/phik-k-get-familiar-with-the-latest-correlation-coefficient-9ba0032b37e7

## Video link
https://www.youtube.com/watch?v=LMsULWGtP2c
