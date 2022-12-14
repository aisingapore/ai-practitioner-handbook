# How do I enhance the workflow with quality-of-life improvements for my end-to-end workflow?

Contributor(s): Syakyr Surani, Platforms Engineer & Ryzal Kamis, Assistant Head (MLOps)

This guide assumes that you have built a basic end-to-end workflow and
want to scale up your workflow while increasing robustness and 
reliability. If you want to know more about building a basic workflow
instead, then you can go to [this section instead](e2e-workflow.md).

As per from that section, this flowchart describes the typical 
end-to-end workflow of an AI project: 

```{mermaid}
flowchart TD
    cicd(CI/CD)
    datastorage[(Data/Artifact Storage & Governance)]
    verctl[(Version Control)]
    devwspace[Developer Workspace]
    modelexp(Model Experimentation)
    modelreg[(Model Registry)]
    contreg[(Container Registry)]
    exptrack(Experiment & Pipeline Tracking)
    modelserv[(Model Serving)]
    modelmon(Model Monitoring)
    style cicd fill:#bbf
    style modelreg fill:#bbf
    style contreg fill:#bbf
    style exptrack fill:#bbf
    style modelmon fill:#bbf
    cicd <---> modelexp
    datastorage <---> modelexp
    datastorage <---> modelreg
    datastorage <-.-> verctl
    verctl <.-> modelreg
    verctl --> devwspace
    verctl <---> contreg
    devwspace --> modelexp
    modelexp --> modelreg
    modelexp <---> contreg
    modelexp ---> exptrack
    modelreg ---> modelserv
    contreg <--> modelserv
    modelserv ---> modelmon
```

This section deals with the other components and processes that are
present in this workflow, but not the simplified version in the other
section.

## Artifact Storage & Governance

Artifacts pertain to data that are not used in training the models in
your project. This can be your configuration settings, logs, etc. On 
the other hand, data and artifact governance refers to the 
authentication and authorisation protocols that are discussed 
previously in the 
[Developer Workspace](e2e-workflow.html#developer-workspace) section.

## CI/CD

Continuous integration and continuous delivery/deployment processes
pertain to the automation of various processes within the workflow 
itself. While this would benefit end-to-end workflows greatly, it is
not implemented within many ML/DL projects due to its complexity and 
time needed to design an effective CI/CD process. If you do want to 
know more about CI/CD, you can refer to [this section][cicd] instead.

[cicd]: ../7-solution-delivery/min-viable-code.md

## Model Registry

This could be seen as a version control for models to manage problems 
such as model drifting and retraining. You may need this component as
your project scales up, and you need to manage multiple models within
the project as well as across multiple projects that may use the same
model(s). This component would also make A/B testing easier since you 
could reference multiple versions of the same model to gauge any 
improvements a new version may provide.

## Container Registry

Containers such as Docker abstracts the codebase while providing a 
sandbox to reduce dependency conflicts while making component 
management easier. This allows better scaling and modularity by 
setting manageable blocks according to their use case instead of by
just the products themselves. However, you should take note whether 
your project requirements allow containerisation as some policies 
within your organisation/client may be against this process due to the 
overheads it may have, especially if the project does not require to be 
designed for scaling.

## Experiment, Pipeline & Model Monitoring/Tracking

The experiment and pipeline tracking as well as model monitoring can be
seen as similar components that target different processes. Experiment
and pipeline tracking focuses more towards monitoring the models as 
they are being trained, and from there, decisions are being made 
through controlling the hyperparameters of the model, or use a 
different model architecture altogether.

On the other hand, model monitoring concerns overseeing the trained 
models and see whether issues are present while it is used for 
inference such as model drifting. These metrics would be collected and
processed to make decisions such as controlling data input requirements
or retraining the model.

## Final Thoughts

There are many more components and processes that could be part of your
end-to-end workflow that are not discussed in this as well as the basic
workflow sections, but the ones that are discussed should be sufficient
for you to build a robust and reliable AI end-to-end workflow. If you 
want to know more about this and MLOps in general, you can take a look
at [ml-ops.org][ml-ops] for more insight.

## Reference

- [MLOps: Machine Learning Operations | InnoQ][ml-ops]

[ml-ops]: https://ml-ops.org/
