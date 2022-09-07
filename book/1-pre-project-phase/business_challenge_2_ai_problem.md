# How does the AI engineer translate the business challenge into an AI problem?
Contributor: Tan Kwan Chet 

---

## Framing Problem Statement from The Business Challenge

Most projects begin when a sponsor has 1 or a few business challenges to solve. As an outsider, understanding business context and process is a great starting point to frame the AI problem. It allows you to understand the sponsor's long term goal and identify the problem statement that affects the sponsor's business or represents a pain point that the sponsor wants to solve.

It takes a lot of creativity to formulate the problem statement. Sponsor tends to speak about their business problems at a high level. So your job is to filter the high level information shared by sponsor to a low level where the problem may relate to their employees who face the pain point on a day-to-day basis. This is important since your AI solution will likely be replacing a repetitive task that their employees may be facing. To form the problem statement, you could use the following steps (illustrated as a map diagram below):

1. Identify the target audience (e.g. employee)
2. Define the problem from target audience's perspective (i.e. understand their pain point)
3. Understand when and where the problem is ocurring
4. Discover the benefit for the target audience and value for the business
5. Convert the information into a HMW (How Might We) problem statement 

### Example - Map Diagram

![Map Diagram](../assets/images/diagrams/map_diagram.jpg)


## Translation of Problem Statement into AI Problem

Next, it is wise to decompose the problem statement into different technical requirements of an AI problem. This can be done by asking a series of questions to prompt the sponsor to better describe their technical requirements. 

### Example - Translation from Problem Statement to Technical Requirements

Sponsor's Problem Statement: "How might we build an AI model to count cells on microscopy images?"

|  Question | Rationale |Technical Requirement |
|---|---|---|
| what is the main task that you are keen to replace? | This gives you an idea on what is the main task that AI needs to automate |  AI model to detect cells by size |
|  What is the type of the data involved? | By knowing if the data is image/video, text or tabular, it will help you focus on a set of technologies such as Computer Vision and Natural Language Processing  | Annotation required to support the detection of cells in images |
| Is the main task achievable by AI model alone?| You check if there is a need to use heuristic method | Aggregate counts of the AI model predictions by prediction class |
| How do you envision to use the AI model? | You understand how the sponsor uses the AI model | This gives you an insight into their deployment infrastructures|

Now, you will have gain an understanding into the business challenge and the AI problem. This will give you a coverage of what the sponsor hopes to achieve from its envisioned AI model. 

## References
- [Sprint: How to Solve Big Problems and Test New Ideas in Just Five Days](https://www.thesprintbook.com/the-design-sprint)
- [Data Science for Business](https://www.oreilly.com/library/view/data-science-for/9781449374273/)