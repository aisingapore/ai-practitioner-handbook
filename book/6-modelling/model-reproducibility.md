# What are the checklist of items to look out for to ensure reproducibility of the model pipeline as much as possible?

Contributor(s): Kew Wai Marn, AI Engineer

## Model reproducibilty

Apart from ensuring reproducibilty in the data and the code of the ML system,
you would need to check your model as well. Assuming you have the same training
code, and the same training data, you should be able to produce the same model.

Reproducible models are important because it allows independent researchers to
be able to achieve the same results, which improves communication and
collaboration. Furthermore, reproducible models makes them less error-prone which
increases its reliability.

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

To reduce the risk of API calls breaking, you can version the libraries used eg.
create a software enviroment with specific and static dependency versions
recorded down in a requirements file.

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

A stable model would be reproducible as it produces consistent results. During
model training for nerual networks, your weights and layer outputs should not be
`NaN` or `Inf`. A given layer should also not return zeroes for more than half
of its outputs. Write tests to check for `NaN` and `Inf` values in your weights
and layer outputs.

Furthermore, do sensitivity analysis on the hyperparameters of your ML system
to ensure system hyperparameter stability.

### 2. Deterministically seed the random number generator (RNG)

Apart from fixing the seed value for data splits, you should use a fixed seed
value across all the libraries in the code base in order to reduce
non-deterministic behaviours eg. weight initialization, regularization, and
optimization in neural networks, split points in random forest algorithm.

Seeding the RNG from python ie. `random.seed()` is not enough as certain
packages have their own implementation of a pseudorandom number generator
eg. NumPy. Do check their documentation on how they generate the random numbers.

However, there will still be areas of randomness that are irreducible, such as
randomness in third party libraries and in configurations of GPUs. Refer to this
[section](#inherent-stochasticity).

### 3. Model version control

Other than versioning the data, model versioning is important to ensure
reproducibility. By taking snapshots of the entire ML pipeline, it is possible
to reproduce the same output again, with the trained weights. Each model version
should also be tagged to it's corresponding metadata (ie. hyperparameters),
training data, and code. Model registries and feature stores help in mainining
model versions.

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

## Inherent stochasticity

As mentioned earlier, the entire ML pipeline is not always reproducible. There
exist inherent stochasticity, such as when using GPUs, randomness in backend
libraries, and stochastic ML algorithms. In order to improve reproducibility,
you can report the average performance of your model using multiple runs or even
build an ensemble of models, each trained with a different random number seed.
The last resort is to record down any potential stochasticity that exist.

__Reference(s):__

- [Testing for Deploying Machine Learning Models](https://developers.google.com/machine-learning/testing-debugging/pipeline/deploying)
- [Testing Pipelines in Production](https://developers.google.com/machine-learning/testing-debugging/pipeline/production)
- [AWS Whitepaper Reproducibility](https://docs.aws.amazon.com/whitepapers/latest/ml-best-practices-healthcare-life-sciences/reproducibility.html)
- [Building a Reproducible Machine Learning Pipeline](https://arxiv.org/pdf/1810.04570.pdf)
- [Reproducible AI: What it is, Why it Matters & How to Improve it?](https://research.aimultiple.com/reproducible-ai/)
- [Introduction to Random Number Generators for Machine Learning in Python](https://machinelearningmastery.com/introduction-to-random-number-generators-for-machine-learning/)
- [Embrace Randomness in Machine Learning](https://machinelearningmastery.com/randomness-in-machine-learning/)
