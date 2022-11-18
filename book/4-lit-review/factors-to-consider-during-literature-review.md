# What are some of the factors/questions that an AI Engineer should consider during literature review?

Contributor(s): Andy Ong, AI Engineer

Literature reviews are necessary at the start of every AI project to understand and explore available solutions in the market. Different business problems require different solutions, and below are some factors that you can consider while performing your literature review. 

-	Business needs
-	Development time
-	Code Existence & Readability
-	Open-Sourcing of a pre-trained model
-	Key takeaways from the literature


## Business Needs

Business considerations must be taken into account during any literature review. These considerations tend to set restrictions on the project. Understanding these considerations can ensure that you are researching relevant solutions. For example, a medically related project requires model explainability and this will require a search for solutions that has model explainability. In a different scenario, if the use case requires edge deployment in mobile devices, this would further direct the selection of literature toward those that support smaller and quicker models.

The literature should not be limited to your project's domain. A common example is using autoencoders for anomaly detection when autoencoders are typically used for computer vision. Such literature can introduce different approaches and highlight possible challenges that you might face in your project. You can understand the various approaches and their benefits, and how should you integrate them into your MVM.

## Development time

All projects have a set of timelines to adhere to, and development time may not be sufficient to build pipelines from scratch. You will have to allocate time for integration tests, project handover and other ad-hoc tasks such as troubleshooting. You can research and identify potential libraries to aid in your pipeline to avoid building it from scratch. You can also attempt to inherit certain classes from suitable libraries to customise them to your project with minimal code. The following sections are specific examples of strategies that can aid in shortening development time.

## Code Existence & Readability

You should be reading up on literature that has training or inference scripts in their code repository. These solutions can be incorporated into your MVM with ease as compared to solutions without any scripts. [Papers with code](https://paperswithcode.com/) contains papers with open-sourced code repositories. 

If the literature is supported by code repositories, you should evaluate the readability of the code and the complexity of integration. The majority of the time, supplied code repositories can be difficult to understand, and integration may take longer than anticipated. Additionally, some repositories/implementations may be more comprehensive than others, such as those that contain class weights as configurable hyperparameters or include an evaluation function.

Consider the copyright agreements and licenses for the papers and codes in light of this. It's possible that your project won't be able to use commercial IP software or certain licenses (like the GPL). Examples of permissive licenses with few limitations on use include the MIT and BSD licenses.

## Open-Sourcing of a pre-trained model

It may be advantageous to search for solutions whose pre-trained model is open-sourced for NLP or CV projects. This will cut down on training time by ensuring that you can use transfer learning to such tasks. Long training times are needed for language or computer vision models, which can add time and cost to a project. It is advantageous if the pre-trained model was developed using datasets from a field related to your use case. For instance, if your use case involves evaluating financial accounts, FinBERT, a pre-trained NLP model, may be more immediately applicable than bert-base.


## Key takeaways from the literature

The results reported in the study should never be taken into consideration. They frequently entail some cherry-picking, and more crucially, the data that is employed varies. Since data differs between the paper and your project, expect to see a change in accuracy since data is typically the main element affecting how well any model performs. Instead, you ought to concentrate on the evaluation techniques and algorithms employed in the literature.

# Conclusion

While these factors are non-exhaustive, they can ensure that you are doing a informative yet meaningful literature review.