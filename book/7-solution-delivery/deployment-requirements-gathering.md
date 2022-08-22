# What are some questions to be asked to the project sponsor to understand their deployment requirements?

Contributor(s): Siti Nuruljannah Baharudin

| Question | Considerations |
|---|---|
| **General** |  |
| Where would the final solution be deployed? | Options may include a cloud service, an on-premise server, or an edge device. If the specifications are fixed, the client should provide them as soon as possible in order for the team to assess whether they are sufficient for the AI solution to operate on. |
| How should the application be packaged for deployment? | Although containerising the application is a common solution, some organisations may have restrictions on the containerisation technology allowed on their servers, or even disallow containerisation altogether. If so, it is recommended that you assess the impact on the deployment effort. For instance, the team may lack expertise in the containerisation technology used, or when containerisation is not used, more system integration testing may be required. These would result in additional effort to prepare the deployment package, which should be communicated to the client. |
| Are there any restrictions or preferences regarding the operating system on which the solution should be deployed? |  |
| Would a staging environment or test device be provided for developers to test with prior to initial deployment? | If not provided, you would need to commission an internal environment that closely mirrors the specifications of the environment on which the solution would eventually be deployed. |
| **Data** |  |
| Where would the data to be used for retraining and inference be located in the production environment? |  |
| Where would the model outputs be stored? Is there any storage size limit on this location? |  |
| If the data storage is located remotely, what is the authentication method to be used to access it? |  |
| **Usage** |  |
| What is the frequency at which the user intends to run the retraining and inference pipelines? |  |
| Is batch inference a requirement? If so, what is the expected size or volume of data in a single batch? |  |
| What are the requirements on inference speed and training time? | You would need to consider whether the limitations of the chosen deployment device would affect these requirements. If refinements can be made to the code to meet the requirements, the additional effort would also need to be considered. |
| What are the requirements on the size of the trained model? |  |
| **Interfacing** |  |
| Is the application required to interface with another system via an API? |  |
| If an API is to be supported, would the application function as the server or a client? |  |
| Which type of API should be supported? | If the client does not have specific requirements on the API, you may recommend them the most commonly used choice that can be easily supported by the tech stack you are using. |
| What is the required format of the API payload? | If the client has provided a specific format, you would need to consider how the size of the payload may affect the inference speed requirements. Performing some benchmarking tests using sample payload files would enable you to better determine this. |
| If no API is required, is there any preferred way for users to trigger the training or inference engine? |  |