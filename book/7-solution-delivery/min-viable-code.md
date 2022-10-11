# How Can We Build a Minimum Viable Code/Configuration for CI/CD Automation Into an Existing Codebase?

Contributor(s): Syakyr Surani, Platforms Engineer

This guide assumes that you have some basic knowledge of [CI/CD][CICD] 
and an existing codebase. The codebase is in a working state and while 
currently you find it manageable, you anticipate that you need to move
away from manual testing that can be unreliable even with a checklist
to work with. You may have multiple projects to manage, or there are 
more contributors raising a pull/merge request than you can possibly
handle just by manual testing. You have heard about CI/CD, but you do
not know where to start. 

[CICD]: https://dev.to/kirekov/basics-of-cicd-5e16

This guide will not recommend specific CI/CD products or tools, but 
a general outline to adhere to for an effective minimum implementation,
and where to go from there. The flowchart below gives the outline of 
the guide:

```{mermaid}
flowchart LR
    step1(Identify Current Processes)
    step2(Create Sample Data)
    step3(Identify Stages of Deployment)
    step4(Start Small)
    step1 --> step2 --> step3 --> step4
```

## Identify Current Processes

Before anything can happen, it is best to plan your actions out. For
that, you would need to list out the actions taken to run manual 
testing for your codebase. This is made easier if you already have a
checklist of processes to test before pushing/merging to a branch. Here
is a list to check against to see if you have missed anything:

- Linting
- Error checking (whether the code produces any unexpected errors)
- Packaging (Docker, PyPI, etc.)

Since we focus mainly on AI projects, there should also be a 
consideration to allow for fast prototyping of model training before
packaging the project into a viable product to be interacted by the
stakeholders.

## Create Sample Data

Due to the nature of our organisation, we deal with data more often
than other tech firms. As such, it is imperative that we create and
build sample data to test out the functionality of our codebase before
running it on the full dataset in order to reduce time taken bugfixing
or adding new features. 

## Identify Stages of Deployment

This step is important in order to reduce time taken to test and have
less resources used prior to the main events such as training and 
monitoring during deployment. Some stages of testing can be defined as
follows:

- Tests made while committing to a bugfix/feature branch (linting, 
  etc.)
- Tests made before doing a pull/merge request to dev (main) branch 
  (error checking, etc.)
- Tests made from dev branch to release (production) (deployment 
  builds, etc.)

## Start Small

This final step is paramount as to not paralyse yourself in the vast 
overarching process of CI/CD automation. Start with a small subset of
the codebase to familiarise yourself with the process before attempting
to refactor an entire codebase, especially if you are working in a 
project with large teams or with critical infrastructure. Iterative 
development is key to managing a large undertaking, one step at a time.

If you need some guidance on where to start, you could refer to 
[this section of the handbook][flowchart] under the simplified 
workflow for more information.

[flowchart]: ../5-data-mgmt-exp-proc/e2e-workflow.md

## Final Thoughts

Every project is different, and therefore there is no one Minimum 
Viable Code/Configuration that can be proposed without first 
understanding the nature of such projects. Nevertheless, it is with 
hope that this guide can point out your first steps in building and 
integrating CI/CD automation into your codebase for a more robust and 
resilient one.

Below are some of the references you can look at to supplement your
CI/CD journey.

## References

- [Gitlab - How to learn CI/CD fast](https://about.gitlab.com/blog/2022/04/13/how-to-learn-ci-cd-fast/)
- [Spiceworks - Top 10 CI/CD Best Practices for 2022](https://www.spiceworks.com/tech/devops/articles/what-is-ci-cd/#_004)

