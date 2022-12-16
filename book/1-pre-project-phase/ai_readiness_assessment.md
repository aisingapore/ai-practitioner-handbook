# What are some questions that an AI engineer can ask the client during pre-project scoping to assess their AI readiness?
Contributor: Joy Lin, Senior AI Technical Consultant
 
---

## Who is this for?
This article is aimed at AI engineers in an organisation like AI Singapore, who are building a solution for another company (henceforth referred to as the client) to take over and implement. In AI Singapore, the business development/presales team, together with the AI engineer, scope for feasible AI projects. In doing so, they assess whether the client has the capability to take over the final solution, integrate and maintain it, as the goal is to enable companies to build their own AI capabilities in the long run. Assuming that the client's proposed AI solution has an established business value and is ethical, this article narrows the focus to the technical aspects of AI readiness.

## Why does AI engineer need to assess client's AI capabilities?
When participating in pre-project scoping, it is beneficial for you to gauge if the client is capable of taking over your solution for deployment. Most AI projects end up in failures during deployment phase due to three main reasons:

1. Technical hurdles in implementing/integrating model into existing operations
2. Decision makers unwilling to approve change to existing operations
3. Model performance not considered strong enough by decision makers

## What can the AI engineer look out for?
To ensure a successful project, let us focus on three broad areas to help you assess the client's AI readiness level. 

### 1. Organisational readiness
> Is there an existing technical team who is able to integrate and maintain the AI models? If not, what are the client's plans to hire the necessary resources?

> Is the client's management supportive of AI projects and team expansion if necessary?

> Do the client's management and key stakeholders allow room for experimentation and development?

As an organisation looking to use AI solutions, the client's management should understand that model building and maintenance requires iterative experimentation and continuous re-training, in turn supporting the investment of right resources.

### 2. Infrastructure readiness
> Is there appropriate infrastructure to hold data in a centralised and standardised manner (e.g. data warehouse), or is the client relying on disparate file systems?

> Are there sufficient computational resources (e.g. CPUs, GPUs, memory) to support model deployment and maintenance for this project? If not, are there plans to acquire more or re-allocate resources?

Preparing for the above strengthens the client's infrastructure capabilities, easing their transition from deployment to integration with minimal disruption to their existing activities.

### 3. Data readiness
> Does the centralised data warehouse provide consistent data format, up-to-date metadata and a single source of truth?

> Is there accurate and complete data to be used in this project?

It is important for the client to maintain high quality and consistent data that can be used for re-training when model drifts over time.

Note: Click [here](key_areas_in_data.md) to read about data readiness on a *project* level.

---
More details available below to help in your assessment:
1. [AI Readiness Index (AIRI)](https://aisingapore.org/innovation/airi/) developed by AI Singapore and increasingly used by organisations in Singapore
2. [Oxford’s Government AI readiness index](https://www.oxfordinsights.com/government-ai-readiness-index2021)
