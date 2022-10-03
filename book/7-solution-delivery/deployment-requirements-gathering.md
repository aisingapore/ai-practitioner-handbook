# What are some questions to be asked to the project sponsor to understand their deployment requirements?

Contributor(s): Siti Nuruljannah Baharudin, AI Engineer

## General
1. Where would the final solution be deployed? 
    - Options may include a cloud service, an on-premise server, or an edge device. If the specifications are fixed, the client should provide them as soon as possible in order for the team to assess whether they are sufficient for the AI solution to operate on.
2. How should the application be packaged for deployment? 
    - Although containerising the application is a common solution, some organisations may have restrictions on the containerisation technology allowed on their servers, or even disallow containerisation altogether. If so, it is recommended that you assess the impact on the deployment effort. For instance, the team may lack expertise in the containerisation technology used, or when containerisation is not used, more system integration testing may be required. These would result in additional effort to prepare the deployment package, which may impact the project schedule.
3. Are there any restrictions or preferences regarding the operating system on which the solution should be deployed? 
4. Are there any restrictions on software licenses to be used?
    - Many open source libraries used in machine learning projects are licensed under Apache 2.0, MIT and BSD licenses. If your solution requires the use of libraries with less permissive licenses, it would be best to check with the project sponsor. 
5. Would a staging environment or test device be provided for developers to test with prior to initial deployment? 
    - If not provided, you would need to commission an internal environment that closely mirrors the specifications of the environment on which the solution would eventually be deployed.

## Data & Model Outputs
1. Where would the data to be used for retraining and inference be located in the deployment environment? 
2. Where would the model outputs be stored? Is there any storage size limit on this location? 
3. If the data storage is located remotely, what is the authentication method to be used to access it?

## Usage
1. What is the frequency at which the user intends to run the retraining and inference pipelines? 
    - Generally, the requirements and considerations for inference are more critical compared to retraining, as the latter is usually performed less frequently and is less time-sensitive.
2. Is batch inference a requirement? If so, what is the expected size or volume of data in a single batch? 
3. What are the requirements on inference speed and training time? 
    - You would need to consider whether the limitations of the chosen deployment device would affect these requirements. If refinements can be made to the code to meet the requirements, the additional effort would also need to be considered.
4. What are the requirements on the size of the trained model? 

## Integration
1. Is the application required to interface with another system via an API? 
2. If an API is to be supported, would the application function as the server or a client? 
3. Which type of API should be supported? 
    - If the client does not have specific requirements on the API, you may recommend them the most commonly used choice that can be easily supported by the tech stack you are using.
4. What is the required format of the API payload? 
    - If the client has provided a specific format, you would need to consider how the size of the payload may affect the inference speed requirements. Performing some benchmarking tests using sample payload files would enable you to better determine this.
5. If no API is required, is there any preferred way for users to trigger the training or inference engine? 