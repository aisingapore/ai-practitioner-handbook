# What are the checklist of items to look out for to ensure reproducibility of the model pipeline as much as possible?

Contributor(s): Kew Wai Marn, AI Engineer

## Model reproducibilty

Apart from ensuring reproducibilty in the data and the code of the ML system,
you would need to check your model as well. Assuming you have the same training
code, and the same training data, you should be able to produce the same model.

## What to check to ensure model reproducibility?

If you have the same training code, and the same training data, but you are
not able to produce the same model, below are several things you should check to
ensure reproducibility of your model. The main goal is to reduce
non-deterministic behaviour in ML modelling as much as possible.

### 1. Model tests

Apart from testing code, you should test your model as well. Below are several
things to test your model for.

#### a. API calls

One of the things you can test is to test the API calls. As ML frameworks and
libraries are constantly getting upgraded, you need to make sure the API calls
are working as expected. Write unit tests with random input data running
through the API call (ie. a single step of gradient descent).

#### b. Algorithmic correctness

Other than testing the API calls, you should make sure your model's performance
is not due to luck.

To check for algorithmic correctness you can:

- Verify that the loss decreases with increasing training iterations.

- Verify that without regularization, the training loss is low enough. If your
model is complex enough, it will capture information from the training data.

- Test specific subcomputations of your algorithm. (ie. test that neural network
weights are updated with every pass).

#### c. Test that model is stable

A stable model would be reproducible as it produce conssitent results. During
model training, your weights and layer outputs should not be `NaN` or `Inf`.
Write tests to check for `NaN` and `Inf` values in your weights and layer
outputs. More than half of the outputs of a layer should not be zero as well.

Furthermore, do sensitivity analysis on the hyperparameters of your ML system
to ensure system hyperparameter stability.

### 2. Deterministically seed the random number generator (RNG)

Apart from fixing the seed value for data splits, you should use a fixed seed
value across all the libraries in the code base in order to reduce
non-deterministic behaviour.

### 3. Model version control

Other than versioning the data, model versioning is important to ensure
reproducibility. By taking snapshots for the entire ML pipeline, it is possible
to reproduce the same output again, even with the trained weights. Furthermore,
each model version should be tagged to it's corresponding metadata
(ie. hyperparameters), training data, and code.

### 4. Integration tests

As a ML pipeline consiste of several components, tests that runs the entire
pipeline end-to-end should be written. To run integration tests faster, train on
a subset of the data or with a simpler model.

### 5. Logging

It is important to log everything used in ML modelling (ie. model parameters,
hyperparameters, feature transformations, order of features, method to select
them, structure of the ensemble (if ensembles were used), specifications of
the hardware used to run the model). This would help to recreate the environment
the model was created in. Furthermore, there should be reporting of any
dependency changes, eg. changes in API calls should be notified.

__Reference(s):__

- [Testing for Deploying Machine Learning Models](https://developers.google.com/machine-learning/testing-debugging/pipeline/deploying)
- [Testing Pipelines in Production](https://developers.google.com/machine-learning/testing-debugging/pipeline/production)
- [AWS Whitepaper Reproducibility](https://docs.aws.amazon.com/whitepapers/latest/ml-best-practices-healthcare-life-sciences/reproducibility.html)
- [Building a Reproducible Machine Learning Pipeline](https://arxiv.org/pdf/1810.04570.pdf)
