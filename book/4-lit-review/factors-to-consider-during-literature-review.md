# What are some of the factors that an AI Engineer should consider during literature review?

Contributor(s): Andy Ong, AI Engineer

---

Literature reviews are necessary at the start of every AI project to understand and explore available solutions in the market. Business problems require different solutions, and below are some factors that you can consider while performing your literature review. 

-	Business needs
-	Development time
-	Existing code respositories
-	Pre-trained models
-	Reported results


## Business needs

Business considerations must be taken into account during any literature review. These considerations tend to set restrictions on the project. Understanding these considerations can ensure that you are researching relevant solutions. For example, a medical AI project requires model explainability, and this will require a search for solutions involving explainable models. Alternatively, if the use case requires edge deployment in mobile devices, this would instead direct the selection of literature toward those that support smaller and quicker models.

The literature search should not be limited to your project's domain. An example is using autoencoders for anomaly detection even though they are typically used for computer vision. Such literature can introduce different approaches and highlight possible challenges that you might face in your project. You can understand the various approaches and their benefits, and how you can integrate them into your solution.

## Development time

All projects have a set of timelines to adhere to, and development time may not be sufficient to build pipelines from scratch. You will have to allocate time for integration tests, project handover and other ad-hoc tasks such as troubleshooting. You can research and identify potential libraries to aid in your pipeline to avoid building it from scratch. You can also attempt to inherit certain classes from suitable libraries to customise them to your project with minimal code. The following sections are specific examples of strategies that can aid in shortening development time.

## Existing code repositories

You should be reading up on literature that include training or inference scripts in their code repository. These solutions can be incorporated into your codebase with ease as compared to solutions without any scripts. [Papers with Code](https://paperswithcode.com/) contains papers with open-sourced code repositories. 

If the literature is supported by code repositories, you should evaluate the readability of the code and complexity of integration. Supplied code repositories can often be difficult to understand, and integration may take longer than anticipated. Additionally, some repositories/implementations may be more comprehensive than others, such as those that contain class weights as configurable hyperparameters or include an evaluation function.

Consider the copyright agreements and licenses for the papers and codes in light of this. It's possible that your project will not be able to use commercial IP software or certain licenses (like the GPL). Examples of permissive licenses with few limitations on use include the MIT and BSD licenses.

## Pre-trained models

For NLP or CV projects, it may be advantageous to search for solutions with pre-trained, open-sourced models. This will cut down on training time by ensuring that you can use transfer learning to such tasks. Long training times are needed for language or computer vision models, which can add time and cost to a project. It is advantageous if the pre-trained model was developed using datasets from a field related to your use case. For instance, if your use case involves evaluating financial accounts, FinBERT, a pre-trained NLP model, may be more immediately applicable than BERT-base.


## Reported results

The results reported in the study should be interpreted in a discerning manner. Reported results may entail some cherry-picking. More crucially, the data used is likely different from your project's use-case. Consequently, expect to see a difference in accuracy, since data is typically the main element affecting how well any model performs. Rather than focusing on the reported results, you should instead concentrate on the evaluation techniques and algorithms employed in the literature.