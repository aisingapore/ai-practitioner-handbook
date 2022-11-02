# What are some of the factors/questions that an AI Engineer should consider during literature review?

Contributor(s): Andy Ong, AI Engineer

Literature reviews are necessary at the start of every AI project to understand and explore available solutions in the market. Different business problems require different solutions, and below are some factors that you can consider while performing your literature review. 

-	Business needs
-	Development time
-	Code Existence & Readability
-	Open-Sourcing of a pre-trained model
-	Key takeaways from the literature


## Business Needs

Business considerations must be taken into account during any literature review. These considerations tend to set restrictions on the project. Understanding these considerations can ensure that you are researching relevant solutions. For example, a medically related project requires model explainability and this will require a search for solutions that has model explainability.

The literature should cover a use case that is in a similar domain to your project. Such literature can introduce different approaches and highlight possible challenges that you might face in your project. You can understand the various approaches and their benefits, and how should you integrate them into your MVM.

## Development time

All projects have a set of timelines to adhere to, and development time may not sufficient to build pipelines from scratch. You will have to allocate time for integration tests, project handover and other ad-hoc tasks such as troubleshooting. You can research and identify potential libraries to aid in your pipeline to avoid building it from scratch. You can also attempt to inherit certain classes from suitable libraries to customise them to your project with minimal code.

## Code Existence & Readability

You should be reading up on literature that has training or inference scripts in their code repository. These solutions can be incorporated into your MVM with ease as compared to solutions without any scripts. [Papers with code](https://paperswithcode.com/) contains papers with open-sourced code repositories. 

If code repositories are supporting the literature, you should consider the readability of the code provided and assess the ease of integration. More often than not, provided code repositories can be challenging to understand, and integration might take more time than supposed.


## Open-Sourcing of a pre-trained model

For projects that involve NLP or CV, it could be beneficial to look for solutions that have its pre-trained model open-sourced. This is to ensure that you can apply transfer learning in such projects, to reduce training time. Language or computer vision models requires extremely long training time, and it could be costly (both time and financially) in a project.

## Key takeaways from the literature

You must never take into account the results published in the paper. They are often inflated, and more importantly, the data used is different. Data is usually the biggest factor contributing to the performance of every model, and since the data between the paper and your project is different, do expect to have a difference in accuracy. You should focus on the algorithms and methods of evaluation used in the literature instead.

# Conclusion

While these factors are non-exhaustive, they can ensure that you are doing a informative yet meaningful literature review.