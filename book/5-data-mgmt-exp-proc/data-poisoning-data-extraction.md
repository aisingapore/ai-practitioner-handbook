# What can I reduce the risks of data poisoning and data extraction?

Contributor(s): Kew Wai Marn, AI Engineer

## Data poisoning

Ideally, data should be collected and labeled in a controlled and safe
environment. Practically, this is time-consuming, and thus expensive, which not
everyone can afford. Therefore, data is sometimes collected from the Internet or
other untrusted sources. This poses a huge risk as an adversary can
intentionally manipulate the data, which causes the ML system to be compromised.
For example, training data can be injected with specific features that causes the model to fail
during inference when inference data with such features are used; i.e. model
"backdoors".

## Data extraction (inference/inversion attacks)

Other than manipulating the data, an adversary may extract details of the
training data by querying the model or inspecting it directly. When
the adversary has unlimited query access to the model, they can use that to
predict whether or not a particular example was contained in the model’s
training dataset.

## How to check your data sources

In order to reduce the risk of data poisoning and extraction, you should check
the following in your ML system:

### 1. Proper access control to protect the raw and processed data from unauthorized users.

To prevent data manipulation, the first thing to do is to secure it (e.g. only
authorized personnel are allowed to access within a specified time frame).

### 2. Ensure the integrity of the data sources for your ML system

Other than securing your data, it is important to know about the data's history
ie. data generation, collection, and assembly process, especially if the source
is public. In addition, list down any potential considerations for data quality
(e.g. trustworthiness, reliability, etc), so that it is easy to backtrack when
necessary.

Examples of considerations and measures:

- How do you ensure that the raw data was not manipulated or poisoned, even by
authorized personnel?

- Have you implemented measures in the data collection process to ensure the
reliability of the data collected? (e.g. if your raw data is collected from
sensors, possible measures to ensure reliability include regular re-calibration,
and/or redundant streams with multiple correlated and overlapping sensors)

- How do you assure the quality of your labeling process, and validate the
resulting labels?

The main idea is to not use data blindly. Take time to understand the data
source,. You can also analyse the data to look for inconsistencies i.e. look at
feature value range, statistics ie. mean for numerical data, data frequencies
for categorical data.

### 3. Ensure that the model output is not part of the input

This is important for models using data crawled from the internet. For example,
when translations of pages done by the model were used as training data for the
model.

### 4. Model only outputs what the user requires (e.g. no confidence score unless necessary)

This is to prevent an adversary in trying to extract information from your model.
For example, for a image classifier, knowing confidence score can allow the
adversary to predict whether or not a particular image was contained in the
model’s training dataset.

### 5. Limit queries by users

As mentioned earlier, if an adversary were given unlimited query access to a
model, they can bombard the model with potential data candidates, in order to
predict the distribution of the training data.

### 6. Anonymize the dataset

As the last line of defense, annoymizing the dataset would prevent any personal
identifiable information (PII) from leaking, as per Singapore's Personal Data
Protection Act (PDPA). However, by itself this is not enough as it does not
protect the proprietary data.

__Reference(s):__

- [BIML Architectural Risk Analysis](https://berryvilleiml.com/docs/ara.pdf)
- [Machine Learning Security against Data Poisoning: Are We There Yet?](https://arxiv.org/pdf/2204.05986.pdf)
- [Just How Toxic is Data Poisoning? A Unified Benchmark for Backdoor and Data Poisoning Attacks](https://arxiv.org/pdf/2006.12557.pdf)
- [Model Inversion Attacks that Exploit Confidence Information and Basic Countermeasures](https://rist.tech.cornell.edu/papers/mi-ccs.pdf)
- [PDPA Overview](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) 
