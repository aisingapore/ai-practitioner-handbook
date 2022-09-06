# The End-To-End Workflow Process

Contributor(s): Syakyr Surani, Ryzal Kamis

This guide assumes that you know basic data engineering and ML/DL 
modelling, and you want to start to build a workflow so that you have
a working AI-powered product at the end of the project. Also, you might
want to scale up your workflow while increasing robustness and 
reliability.

## What Does It Mean to Have an End-to-End Workflow

When you started learning about ML, most likely you were only taught to
train a model or perhaps to clean the data before training. Having an
end-to-end workflow means you have a birds-eye view on the whole 
project from conception to deployment. This means you can delegate 
tasks better and diagnose issues much more effectively rather than 
overhauling the whole project when something unexpected happens and 
renders the project undeployable or unusable.

The flowchart below describes a typical end-to-end workflow of an ML
project:

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

However, if you're just starting out in building an end-to-end workflow
for your project, this simplified flowchart would be more suitable:

```{mermaid}
flowchart TD
    datastorage[(Data Storage)]
    verctl[(Version Control)]
    devwspace[Developer Workspace]
    modelexp(Model Experimentation)
    modelserv[(Model Serving)]
    datastorage <---> modelexp
    datastorage <-.-> verctl
    verctl --> devwspace
    devwspace --> modelexp
    modelexp ---> modelserv
```

This guide will focus more on the simplified flowchart while expanding
the topic from there.

## Data Storage

This pertains to storing the lifeblood of all ML/DL projects, of which 
it is paramount that you know how and where to store data, and that you
are able to identify raw and processed data. Raw data is defined as 
data that is obtained from primary sources such as temperature sensors,
while processed data is defined as data that is augmented by 
algorithm(s) or from another ML/DL model.

It is also important that you know how the product is to be designed,
such as how data is being fed into the model, or through a
pre-processing algorithm first. You could ingest the data either 
locally or remotely, and remote options differ between using object 
storage for blob-like data such as image and audio files, database 
storage for text data, of which it may be structured (SQL, etc.) or
unstructured (NoSQL, JSON, etc.).

Understanding different types of data storage is important since the
data that you may be given may not be suitable to be fed into the model
directly. For example, you might be given a compressed folder of Excel
sheets, but directly processing them before feeding into the model may
be suboptimal when you could parallise both processes and possibly 
reducing training time. This may also make resuming work easier since 
there are more checkpoints between the raw data and the model itself.

## Version Control

Most, if not all, codebases benefit from version control to reduce 
errors by rolling back changes to a known working source. You may 
already have been exposed to it through GitHub or GitLab, which are the
leading platforms for source code management especially for open source
projects. Understanding how to use version control effectively would 
make the end-to-end workflow easier. Refer to another part of this 
handbook for more information regarding this process.

## Developer Workspace

A workspace is the easiest to understand within the workflow, but can 
also be quite complex, especially pertaining to authentication and
authorisation protocols that your organisation, or client, may have. 
Some reasons may be due to data being sensitive, the machine being 
airgapped, or that the code must be compatible with legacy hardware 
that you cannot interact directly with.

## Model Experimentation

This is the main part, of which the workflow is designed around on. A
well-designed workflow would make this process run more smoothly since
you would not have the need to change the codebase drastically when any
one of the other components have to change due to external events 
beyond your control.

## Model Serving

This may well be the end goal for most, if not all, ML/DL projects. 
Typical tutorials would usually just end it with the model to be served
locally through script execution, more mature projects would require
a remote callable API since processes are usually interacted between
machines rather than only within one machine. These APIs may usually 
use either the REST or gRPC protocol. You would have to decide which 
method is more suitable for your project.

## Other Components and Processes

This section deals with the other components and processes that are
present in the first workflow, but not the other.

### Artifact Storage & Governance

Artifacts pertain to data that are not used in training the models in
your project. This can be your configuration settings, logs, etc. On 
the other hand, data and artifact governance refers to the 
authentication and authorisation protocols that are discussed 
previously in the [Developer Workspace](#developer-workspace) section.

### CI/CD

Continuous integration and continuous delivery/deployment processes
pertain to the automation of various processes within the workflow 
itself. While this would benefit end-to-end workflows greatly, it is
not implemented within many ML/DL projects due to its complexity and 
time needed to design an effective CI/CD process, and therefore not 
part of the simplified workflow.

### Model Registry

This could be seen as a version control for models to manage problems 
such as model drifting and retraining. This is omitted in the 
simplified workflow as small ML/DL projects would benefit little from
this as compared to other components.

### Container Registry

Containers such as Docker abstracts the codebase while providing a 
sandbox to reduce dependency conflicts while making component 
management easier. This is omitted in the simplified workflow as some
policies within your organisation/client may be against this process 
due to the overheads it may have, especially if the project does not
require to be designed for scaling.

### Model Monitoring

This process is needed should you need to monitor issues while serving
the model such as model drifting. These metrics would be collected and
processed to make decisions such as controlling data input requirements
or retraining the model.

