# What are the platforms and their respective considerations required for collaborative ML development?

Contributor(s): Dylan Poh Guan Kiong, AI Engineer [(GitHub)](https://unicorndy.github.io/Dylan_Poh/)

---

With the increasing complexity of machine learning projects, it is highly likely that a team of developers is required to complete the task. As a result, it is critical to have the ability to collaborate efficiently. 

Fundamentally, there are two ways that teams collaborate.  

*Luke Marsden: When you boil it down to basics, there are really two fundamental modes of collaborating between different people doing work: synchronous and asynchronous.*

*Synchronous*: Communications are scheduled, real-time interactions by phone, video, or in-person, sometimes interrupting one another for urgent tasks or simply asking a question. In terms of development, the upstream have to complete their tasks before the downstream team can continue with their work (Dependencies issues)

*Asynchronous*: Communication happens on your own time, with a different team or people concurrently working on a different task. An efficient mechanism is required to resolve merge conflicts. 

With this in mind, we seek to introduce some tools and practices for a team to get started in the hope that stumbling blocks will be reduced to the minimum. The practices introduced here assume development using Python as the primary language.

## Communication tools
Establishing effective communication right from the beginning of any project will allow all team members to align toward the same goal and reduce any possible friction. A quintessential example of miscommunication is an unclear problem statement leading to team members having different views on the outcome of the project.

The following tools (by no means exhaustive) may be useful for remote, office, and hybrid working arrangements:
- A big whiteboard often produces the most efficient channel to share ideas. (Physical Meetup)
- [Google Workspace](https://workspace.google.com/), a full suite of communication tools such as Google meet, shared Google calendar, and Gmail to see the complete list of participants and scheduled meetings. Other option includes the [Microsoft Team](https://www.microsoft.com/en-us/microsoft-teams/log-in).
- [Miro](https://miro.com/) is an easy to use, intuitive, collobration tool that uses little effort to setup quickly. Other option includes [Coggle](https://coggle.it/).

## Code versioning
Jupyter notebooks (.ipynb) are powerful, but also have many limitations. For example, it is impractical to use pure git for versioning Jupyter notebooks (because of large amounts of embedded and frequently changing HTML). Jupyter notebooks are also unsuitable for deployment or production. Naming and renaming files or folders with comments are also undesirable and difficult to keep track of.

Instead, using [git](https://git-scm.com/) for distributed version control and tracking changes helps coordinate work among team members. Developing code in Python script (.py) is highly preferred and using [GitLab](https://about.gitlab.com/) or [GitHub](https://github.com/) to manage your code online with an advanced interface to resolve merged conflict that occurs frequently for asynchronous work. 

Merge conflicts occur when the source and target branches of a merge request (as termed by GitLab) or pull request (as termed  by GitHub) contain different changes or commits. As mentioned, this is especially common during collaboration when more than two engineers are contributing to the code. In this case, engineers must choose which change to accept. Once the changes are made, you can assign reviewer to inspect the changes which ensure the correctness of the merge and prevent breaking the code. Examples of the occurrence of and tools to handle conflicts are linked here for both [GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github) and [GitLab](https://docs.gitlab.com/ee/user/project/merge_requests/conflicts.html#:~:text=Merge%20conflicts%20happen%20when%20the,GitLab%20can%20merge%20changes%20together.).

Keeping a standardised environment for development keeps Python package dependencies consistent, and together with git, allows different members to easily switch between different machines such as local machines or machines in the cloud. One popular option that manages the environment is [Conda](https://docs.conda.io/en/latest/) (environment.yml) 

More in-depth information on setting up a machine learning project repository can be found [here](https://aisingapore.github.io/handbook-staging/book/3-collab-dev-platforms/repo-structure-setup.html). 

## Model/weight/data versioning
Shared storage such as cloud storage ensures the team is assessing the correct dataset and having access to a shared transformed dataset cuts down data preprocessing/transformation time allowing the engineer to focus on modeling. Also, weights and datasets should not be pushed to the version control system, as the repository size might become too large for the local machine.

Having a system to keep track of the trained model and the corresponding dataset early on will prove to be fruitful, as more experiments will make it difficult to trace back. One good practice will be to save the checkpoints and the models together and keep track of the corresponding dataset used for the training. Recommended tools include [MLflow](https://mlflow.org/) and [Weights & Biases](https://wandb.ai/site) for tracking experiments and versioning models. [DVC](https://dvc.org/) and [neptune.ai](https://neptune.ai/) are tools to consider for data version control. Even a simple shared spreadsheet keeping track of model/weights/dataset versioning will pay off eventually.

It is also possible to set up a cloud-based compute/development environment where all collaborators can share the same environment and tools (VScode, Jupyter Lab) and shared storage. Some of the examples are Amazon EC2 Instance Types, Data Science Virtual Machine and Google Compute Engine.