# How do we make data splits repeatable?

Contributor(s): Lee Xin Jie, Senior AI Engineer (100E)

---

It is common for ML beginners to adopt naive random data splitting. In this approach, you may randomly select 80%, 10%, 10% of the data for your training, validation and testing data each time you run the algorithm. However, naive random data splitting is often not repeatable. While you may be able to fix random seeds to ensure some repeatability in data splitting on your machine, this repeatability is not guaranteed when the dataset has changed, or when your colleagues run the same data split algorithm on a different machine.

Having a repeatable train test split ensures that your experiments are reproducible not just by yourself, but by others. 

_Model reproducibility is discussed in detail later in the section [How can I maximise model reproducibility](../6-modelling/model-reproducibility.md)._

Firstly, let’s introduce the concept of hashing.

Hashing is a one way transformation of any given string or key into a hash value, which is often an output of a fixed length. A hash function is always deterministic, and the same input will always generate the same output. Since it is a one way transformation, you are not able to retrieve the original string or key from the hash value.

One approach to ensure the data splits are repeatable is to take a selected set of column/columns and hash it. You can then make use of the hash to split your data. This hash value will always be the same every time you run the algorithm.

Columns that are candidates for hashing should:
1. Not be features or labels that are used for training
2. Not be correlated to label
3. Be granular enough

Features and labels should not be used for hashing, as doing so may inadvertently introduce bias into the data splits. This is because data with certain features or labels may appear more in some data splits, and less in the other data splits. Columns selected for hashing should also be granular enough, hence columns such as year should not be selected. 

Examples of columns that could be used are ID columns. Alternatively, you can concatenate all columns as a string and hash on that.

Once the column/columns are hashed, a simple approach for performing train-test split will be as follows. As an example, if you want 80% of your dataset to be allocated into the training set, 10% to the validation set and 10% to the test set, you can apply the modulo operator to the hashed value. Data points with remainders of less than 8 can be assigned to the training set. Those with remainders of 8 can be assigned to the validation set and those with remainders of 9 can be assigned to the test set.

| Date | Store | Hash(Date,Store) % 10 | Data Split |
|------|-------|-----------------------|------------|
| 10 November 2022 | ABC | 6 | Train |
| 10 November 2022 | XYZ | 8 | Validation |
| 11 November 2022 | ABC | 3 | Train |
| 12 November 2022 | DEF | 1 | Train |

To do this in python, an example will be: 
```
s = "10november2022abc"
hashed_value = hash(s)
remainder = hashed_value % 10
```

If there is a combination of columns that determine if 2 data points are correlated, and you want these data points to be grouped together in the same split, you can concatenate these columns together in a string and hash it. 

Repeatable data splitting is not just limited to the above mentioned method. The key thing is to ensure the repeatability of the splitting process by any users on any machines.

For time series problems, you may want to adopt temporal data splits. You can adopt various data splitting approaches as long as you version control the data split logic to ensure its reproducibility.

Examples of applicable data splits are:
1. Select cutoff datetimes for data split, e.g. data before 2022-12-15 00:00:00.000000 to be in the training set, data after 2022-12-15 00:00:00.000000 to be in the validation set, etc.
2. Selecting the first 10 months of every year to be in the training set, 11th month to be in the validation set, and the 12th month to be in the test set.
3. Selecting the first 20 days of every month to be in the training set, the next 5 days to be in the validation set, and the last 5 days to be in the test set.

## References
- [Machine Learning Design Patterns: Solutions to Common Challenges in Data Preparation, Model Building, and MLOps](https://www.oreilly.com/library/view/machine-learning-design/9781098115777/)