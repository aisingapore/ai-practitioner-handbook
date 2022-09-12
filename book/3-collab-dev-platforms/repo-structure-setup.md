# What are some considerations in setting up a project repository to facilitate collaboration and establish good coding practices among developers?

Contributor(s): Siti Nuruljannah Baharudin

## Use of existing project templates

Prior to setting up a repository, you would want to plan the structure of your code base. If your organisation provides an existing template for machine learning projects, that would be a good place to start. Otherwise, you may want to consider using one of the many open-source frameworks available, which come with boilerplate code for the various components in a typical ML project. The scaffolding provided by such frameworks would not only save you some effort in setting up the project, but also help to establish a standard for developers to create modular and maintainable code.

## Configuration management

Regardless of the framework or template used, management of configuration files is an important area of consideration in any ML project, since ML pipelines designed to be flexible and extensible would rely heavily on configuration files as inputs. You are recommended to keep all configuration files in a single directory, separate from the source code files. It is also good practice to maintain separate configuration files for each environment developers work in. For instance, configuration files for the local development environment could be placed in a subdirectory `/config/local`, files for the test server environment in `/config/test`, and so on. 

## General file management

In a Git repository, a [.gitignore](https://git-scm.com/docs/gitignore) file is crucial in helping you filter out files and directories that should not be pushed to the repository, such as configuration files for a developer’s local environment, which would likely contain settings unique to the individual’s workspace. Other examples of files that should not end up in the repository are authentication keys, data files, log files and trained model weights.

Typically, individual developers would create their own notebooks containing EDA-related code or prototype code for the models being explored. Although these may end up as throwaway code, they serve the useful purpose of knowledge sharing at the beginning of a project. It is recommended that these files are placed in a `notebooks` subdirectory and pushed to the repository within each developer’s personal branch, which do not need to be merged to the main branch.

## Dependency management

Another area to consider is the management of code dependencies. At the start of a new project, initialising a single set of initial dependencies would suffice. In a Python project, this could mean maintaining a single `requirements.txt` file. As the code increases in complexity, or if separate components of the application are to be deployed in different environments, it is common for conflicting dependencies to occur. In this case, developers would need to maintain multiple sets of dependencies. These dependency files could be named with suffixes indicating the environment or module it is for, e.g. `requirements-train.txt`.

## Developer productivity tools

Besides software-related components, your repository may contain other files such as issue templates and hook scripts. Issue templates are used to pre-fill issue descriptions with custom fields or sections, which guides developers to include all necessary information when creating an issue. For instance, an issue template for a bug could include sections like “Steps to reproduce”, “Expected result” and “Actual result”. 

In a Git repository, [hooks](https://githooks.com/) are scripts that Git executes locally before or after events such as commit and push. For example, you could set up a pre-commit script to run code through a linter, ensuring it meets the standards before it is allowed to be committed. With the numerous hook scripts and frameworks available, hooks do not require a lot of effort to set up, yet can greatly increase developer productivity when used appropriately.

__Reference(s):__ 
- [AI Singapore's Cookiecutter Template for End-to-end ML Projects](https://github.com/aisingapore/ml-project-cookiecutter-gcp)
- [Kedro](https://github.com/kedro-org/kedro) - A Python framework for creating reproducible, maintainable and modular data science code
- [Git Branch tutorial](https://www.atlassian.com/git/tutorials/using-branches)