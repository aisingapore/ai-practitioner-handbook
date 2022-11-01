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

Sample Python command (for reference):

    a) df.shape
    b) df.info() or df.dtypes or pd.value_counts(df.dtypes)    
    c) df.head() or df.tail()
    d) sum(df.duplicated())
    e) df.nunique()

Expected ouput: 

- raw version of data loaded in the notebook
- size of data, whether parallel processing is needed
- datatype of features, which features are numeric/continuous, or categorical
- (optional) further discussion with stakeholder on handling private/sensitive data and duplicate rows

a.) Tips for large data:

In the scenario if the data is too huge, explore using reading by sampling or chunking. Parallel processing like Dask or Ray can also help. For saving big data to disk, other file format (like Pickle, Feather, Parquest and HDF5) can help to compress to reduce the storage size.

b.) Tips for performing granularity checks 

Purpose is to understand how fine or coarse each row and column is and verify whether the table is of the correct granularity per the database schema. These are some checklist questions for granularity checks

- What does a record represent?
  - Is it wide format? (repeated responses will be in a single row, and each response is in a separate column)
  <img src="../assets/images/screenshots/wide_format.PNG" width="500" height="120" />

  - Is it long/stacked format? (each row is one time point per subject)
  <img src="../assets/images/screenshots/long_format.PNG" width="400" height="300" />

- Do all records capture granularity at the same level?
- If the data were aggregated, how was the aggregation performed?
- What kinds of aggregations can we perform on the data?

c.) Tips for performing cardinality checks 

Purpose is to find out how many distinct value in each features. Considered dropping high cardinality feature(s) that have almost equal or close to number of rows in the dataset. For example, unique id and remarks which is not useful for EDA as there are no trend in these feature(s).

# Content investigation

## 2a) Quality checks

General guideline:

This sub-section should cover mostly on data cleaning and imputing. If there are too many missing values consider dropping the column. However if dropping is not an option, a more sophisticated method for imputing the missing value is to use the other avaiable features to predict the value of that particular column. 

Expected ouput:
- cleaned version of data ready for plotting charts
- identify data/column(s) that requires preprocessing in the datapipeline

a.) Tips on missing data

The choice of approach for handling missing data is also influence by the type of "missingness". Before performing any imputation, it is highly recommended to first consult the stakeholder and understand possible reasons behind the missingness. There are three kinds of missing data.

- Missing completely at random (MCAR)
  
  There is no relationship between the missingness of the data and any values observed or missing. There is nothing systemic going on that makes some data more likely to be missing than others.

- Missing at random (MAR)

  An observation is missing has nothing to do with the missing values, but it does have to do with the values of the an individual's observed variable(s). For instance, men are more likely to tell you their weight than women, hence weight feature is considered as MAR.

- Missing not at random (MNAR)
  
  There is relationship between the inclination or natural tendency of the value to be missing and its values. For example, individual with the lowest eduation may have their missing value on the education feature.

Generally, there are 4 ways to impute

- Assign a fixed value(s) based on domain knowledge
  
  Try to obtain the missing data from stakeholder or relevant subject matter expert (SME). For instance, stakeholder might said that the data is for a certain health campaign was for breast cancer screening, hence missing Gender can be imputed as Female.

- Simple imputation based on statistical summaries

  For numerical features, impute using mean or median of that feature. For categorical features, impute using mode (most frequent) of that feature.

- Model-based imputation

  Using other available features as predictors (eg. MissForest: see article link at reference section)

- Multiple imputation 

  Most sophisticated imputation method, more time consuming but has unbiased outcome. It takes random samples for each imputation, and take the average of the predictions from each imputation. (see video link at reference section)

b.) Tips on cleaning categorial features:

Perform cardinality check on categorical features as there could be similar category due to spelling mistake or variations. Cleaning these erroneous category will help to reduce unnecessary noise in the analysis. It also helps to assess whether some categories are too sparse and may need to be merged for greater statistical power.

At the same time, determine if the categorial features should be later mapped as ordinal or nominal. Converting categorial into numerical helps to include these catagerial features in the pairwise coorelation algothrim.

Sample Python command (for reference):

    categorical_columns = ['<column1>', '<column2>', ..., '<columnN>']
    for column_name in categorical_columns:
      print(df[column_name].unique())

c.) Tips on cleaning multiple currency type in same column:

If multiple currencies are involved as single feature, make sure to convert them into the same currency in the same column, otherwise the scale of the different currency will confuse the model when training or EDA findings.

## 2b) Distribution checks

General guideline:

This sub-section should cover generating the distribution and summary statistics. Understanding variable properties like central trends (mean), spread (variance) and skewness help you to spot erroneous values and potential outliers easily.

If there are district groups in the data, try grouping them and perform individual analysis for each group, in additional to the entire data analysis. Try to use looping to cover the entire possible combinations when plotting charts that compare two features instead of selecting particular features combination that you preceive is useful. Investigate further if certain combination of features have interesting results. 

Highlight the findings on the notebook, regardless of whether they are useful or not, this allows the reader to understand the purpose of the charts.

The analysis should cover the following
- summary statistics of the features
- distribution of the features
- feature patterns (trend)

Expected ouput:
- characteristics of each feature
- spotting potential outliers and erroneous values
- summary of the findings
- potential characteristics in the feature that can extracted further for feature transforming in the datapipeline

a.) Tips on the summary statistics

  Perform summary statistics separately on numerical vs categorial features so as certain statistics is not useful for categorical (eg. no percentiles for categorical) and vice-versa (eg. no frequency and unqiue count for continous numerical values).

  Python command (for reference):

  For numerical features:

      a) df.describe(include=[np.number]) 
      b) df.numeric.describe()
      c) df.describe(percentiles=[.1, .5, .9]))

  For categorical features:

      a) df.describe(exclude=[np.number])
      b) df.describe(include=[object])  

  Others:

      a) df.describe(include='all')
      b) df.describe(datetime_is_numeric=True)

b.) Tips on the type of plot for univariate data (only one variable):

- Histogram chart (great for viewing distribution of features, and comparing 
between different group of data)

  Sample python command for choosing bin size

      sns.displot(df, x="<column_name>", binwidth=3)
      sns.displot(df, x="<column_name>", binwidth=20)

- Kernel density estimation (KDE)
  
  A histogram aims to approximate the underlying probability density function that generated the data by binning and counting observations.

  Sample python command for choosing smoothing bandwidth

      sns.displot(df, x="<column_name>", kind="kde", bw_adjust=.25)
      sns.displot(df, x="<column_name>", kind="kde", bw_adjust=2)  

- Stacked chart 
  
  Avoid using if possible.

- Line chart 

  Commonly use in time-series data, mainly use to observe trend over a time period.

- Pie chart 
  
  Not recommended, use only if need to compare the size of each category.

- Box plot 

  Useful for identify 25%-50%-75% mark and outlier(s), only if the outlier is not extreme. Especially useful for indicating whether a distribution is skewed.


## 2c) Relationship checks

General guideline:

To find out the relationship between feature and target so as to generate ideas for feature engineering and selection (feature importance). The goal is to identify multicollinear features or categories. Correlated features distort interpretability and feature importance, droping or merging some collinear features should be explored based on domain knowledge. 

Also, in the scenario if there are too few features in the data, feature engineering should be explored. Conversely if there are too many features, feature importance should be explored and then dropping less important features.

The analysis should cover the following
- relationships between each feature and the target
- relationships between features

Expected ouput:
- which features are postive/negative correlated to each other
- which features is more/less important to target label
- summary of the findings
- ideas on feature engineering/selection for feature transforming in the datapipeline

a.) Tips on the pairwise correlation:

- Categorical vs Categorical

  - Crosstabs

    Compute a simple cross tabulation of two (or more) factors.

    Sample Python command (for reference):

        s1 = pd.Categorical(['p', 'q'], categories=['p', 'q', 'r'])
        b1 = pd.Categorical(['s', 't'], categories=['s', 't', 'u'])
        pd.crosstab(s1, b1, dropna=False)

- Numerical vs Numerical correlation 

  - Spearman's & Pearson's correlation 
    
    Output single numerical value as the degree of correlation, no distribution. Key difference is Pearson coefficient works with a linear relationship between the two variables whereas the Spearman Coefficient works with monotonic relationships as well. (Monotonic relationship: rate at which an increase or decrease occurs does not necessarily have to be the same for both unlike linear relationship)
  
  - Seaborn's pairplot

    It has distribution information and views strength of correlation by shape of distribution. "/" is positive correlated while "\\" as negative correlated.

- Categorical & numerical correlation (no negative correlation due the categorical features)

  - Phi_K's correlation matrix

    Phi_K is a new correlation coefficient between categorical, ordinal, and interval variables with Pearson characteristics (see article link at reference section)

  - Preprocessing method  

    Converting categorical to numerical forms with techniques like ordinal or nominal encoding and then normalizing to the same scale so that it can be use for numerical vs numerical correlation.

b.) Tips on the bivariate/multivariate correlation (two/three different variables):

For comparing specific features

- Scatter plot 
  
  Useful for examining up to 3 features together, hue as the 3rd feature. The hue feature can be categorical instead of numerical.

- Joint plot

  Combination of scatter and distribution plot of first two features, hue as the 3rd feature. Additional distribution information is available as multiple same points is not easily detected in scatter plot.

- Joint grid

  Combination of scatter and box plot of 2 features. Great for identifying 25%-50%-75% mark as additional information.

- t-SNE plot 
  
  Useful for examining features above 3 by compressing the multiple features into 2 dimension and hue as the target feature. This allows you to immediately discern whether the classes are separable based on the features.

c) Tips on feature engineering:

Try to link the insights from the analysis to feature engineering. For example, if you find that number of deliveries (the target) is much higher on Mondays compared to the rest of the week, you could engineer a separate feature is_monday to boost the model’s performance. 

If certain feature have a very similar relationship to the target and are sparse, you could merge them during feature engineering to create a stronger feature. For instance, capital_gains and capital_loss can be merged into is_investor since if there are not many individuals who invest.

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
