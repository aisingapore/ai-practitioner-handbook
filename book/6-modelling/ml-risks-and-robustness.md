# What are some ML risks I should be aware of and how it relates to model robustness. What are some tools I can use to assess model robustness?

Contributor(s): Kew Wai Marn, AI Engineer

## Brief overview of Machine Learning (ML) risks

Risks of ML systems can come from data, model, and/or infrastructure.
According to the Architectural Risk Analysis by Berryville Institute of
Machine Learning, the top risk is adversarial examples. This is when an attacker
tries to fool the system by giving malicious input (small perturbations that
cause mispredictions). These perturbations are derived from model’s
vulnerabilities, which are areas where the model fails to perform ie. predict
incorrectly.

However this is just one side of the story, risks can also come
from intrinsic design flaw of the system which are different from intentional
attacks. The intrinsic design flaw of the system can include areas which the
model does not perform as it should be.

It is important to consider ML robustness because if your model is not robust,
it would be less reliable (when it fails unexpectedly) ie. road sign detection
in autonomous vehicles, misclassify stop sign as a speed limit sign would
result in life threatening consequences.

## What is ML Robustness?

According to Singapore's Model AI Governance Framework, ML Robustness is defined
as whether the system can function with unexpected inputs. The ability of the
model to perform with unexpected inputs affects the reliability of the ML system.
Unexpected inputs can be from adversarial or non-adversarial origin.

### Adversarial Robustness

Because of adversarial examples as the top risk of ML systems as mentioned
earlier, there is a need to look at adversarial robustness where it is defined
as the minimal perturbation value that the attacker must introduce for a
successful attack (model fails to infer correctly with adversarial input). If
a model is adversarially robust, it will require more pertubations for a
sucessful attack. It is to note that there are many other metrics that can be
used to measure adversarial robustness ie. CLEVER, loss sensitivity, etc.

### Non-adversarial Robustness

On the other hand, apart from attacks, the ML model itself could be flawed (not
able to perform as it should be). Unexpected inputs, mentioned in the definition
above, can be quite ambiguous. One type of unexpected inputs can be
out-of-distribution (OOD) data. OOD data are data that has a different
distribution from your training data but is still within the problem scope where
it might appear in production. For example, images from a different camera of
the same brand.

This risk can be reduced if data representativeness was considered in the data
collection phase, as mentioned in [Chapter 1](../1-pre-project-phase/key_areas_in_data.html#is-the-training-data-representative-of-the-production-data).

## Robustness Testing

One way to ensure robust ML systems is to do robustness testing, where we can
anticipate the robustness of the models using adversarial examples and
OOD data.

For adversarial robustness testing, the goal is to test how resilient the model
is to adversarial examples, or how easily adversarial examples can be created
from the model.

For non-adversarial robustness testing, the goal is to test where the model fails
using OOD data.

There are two ways to obtain OOD data. Either collect from another source, or to
generate it by applying metamorphic mutation. Metamorphic mutation comes from
software testing, where we mutate data that was inferred correctly by the model
in a way that does not change the label (label-preserving mutations) eg.
horizontally flip an image. For text, it is slightly trickier as valid
mutations depends on your model's objective. For example, adding typos would be
a valid mutation if your model is supposed to be invariant on typos ie. not a spell
checker. For tabular data, the mutation strategies are still under research.

### Robustness Testing Tools

Below are some tools you can try for specific types of data, model and task.

|                                         Tool                                        |                                                     Data Type                                                     |                                   Model Type                                  |           Task Type (Nature of model output)           |
|-------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------:|:------------------------------------------------------:|
| [IBM ART, Adversarial](https://github.com/Trusted-AI/adversarial-robustness-toolbox)|                   Generally arrays of numeric data (i.e. Images, Audio), but is attack specific                   | Any for black box attacks, specific model type for specific white box attacks |          Attack-specific, Mainly classification        |
|            [TextAttack, Adversarial](https://github.com/QData/TextAttack)           |                                                        Text                                                       | Any for black box attacks. specific model type for specific white box attacks |          Classification, Sequence-to-sequence          |
|       [Microsoft CheckList. Non-adversarial](https://github.com/marcotcr/checklist) | Any arbitrary format (as the mutation functions can be user-defined). Only some text mutations supported in tool. |                                      Any                                      | Any (as the expectation functions can be user-defined) |

### When to do it?

Using the robustness testing tools, you can test your model in the CI/CD pipeline,
at the same level as model evaluation, to get a good evalutation of your model.
Just like unit testing or integration testing, you only need to set it up once.
With every new retraining, you can compare the robustness between the model
versions.

## Words of caution

The goal of robustness testing is to find areas where your model does not
perform, and improve on them, rather than deciding whether the model is robust
or not robust. There is always a need for comparison between models versions
(especially for adversarial robustness testing). Testing the robustness of one
model does not tell you anything other than where it fails. Lastly, you might
find that standard accuracy might have a trade off with robustness, this is
still (as of writing) an area under research.

__Reference(s):__

- [BIML Architectural Risk Analysis](https://berryvilleiml.com/docs/ara.pdf)
- [Singapore's Model AI Governance Framework](https://file.go.gov.sg/aiverify.pdf)
- [DeepFool](https://arxiv.org/pdf/1511.04599.pdf)
- [IBM-ART](https://github.com/Trusted-AI/adversarial-robustness-toolbox)
- [Microsoft CheckList](https://github.com/marcotcr/checklist)
- [TextAttack](https://github.com/QData/TextAttack)
- [Test ML like software](https://towardsdatascience.com/why-dont-we-test-machine-learning-as-we-test-software-43f5720903d)
- [Metamorphic Testing](https://arxiv.org/pdf/2002.12543.pdf)
