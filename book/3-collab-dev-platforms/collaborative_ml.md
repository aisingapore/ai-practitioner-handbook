# What are the platforms and their respective considerations required for collaborative ML development?

Contributor(s): Dylan Poh Guan Kiong

With the increasing complexity of Machine Learning projects, highly likely a team will be formed to complete the task. Being able to collaborate efficiently may be more critical than ever before. 

Fundamentally, there are two ways that teams collaborate. <br>
*Luke Marsden: When you boil it down to basics, there are really two fundamental modes of collaborating between different people doing work: synchronous and asynchronous.*

*Synchronous*: Communications are scheduled, real-time interactions by phone, video, or in-person, sometimes interrupting one another for urgent tasks or simply asking a question. In terms of development, the upstream have to complete their tasks before the downstream team can continue with their work (Dependencies issues)

*Asynchronous*: Communication happens on your own time, with a different team or people concurrently working on a different task. An efficient coping mechanism is required to resolve merged conflict. 

With this in mind, we seek to introduce some tools and practices for a team to get started in the hope that stumbling blocks will be reduced to the minimum. The practices introduce here assume development using python as the primary language.

## Communication tools.
Establishing effective communication right from the beginning of any project will allow all team members to align toward the same goal and reduce any possible friction. An example of a quintessential miscommunication is an unclear problem statement leading to team members having different views on the outcome of the projects.
The following tools by no means exhaustive proved to be useful for remote, office, and hybrid working arrangements.
- A big whiteboard often produces the most efficient channel to share ideas. (Physical Meetup)
- [ Google Workspace](https://workspace.google.com/), a full suite of communication tools such as Google meet, shared Google calendar, and Gmail to see the complete list of participants and scheduled meetings. Other option includes the [Microsoft Team](https://www.microsoft.com/en-us/microsoft-teams/log-in).
- [Miro](https://miro.com/) is an easy to use, intuitive, collobration tool that uses little effort to setup quickly. Other option includes [Coggle](https://coggle.it/).

## Code versioning
Jupyter notebook(.ipynb) although powerful has many limitations. Versioning is not one of them and is certainly not the best format to be deployed or go into production. Name and renaming files or folders with comments are also undesirable and difficult to keep track of. Instead, using [git](https://git-scm.com/) for distributed version control and tracking changes helps coordinate work among team members. Developing code in python script (.py) is highly preferred and using [Gitlab](https://about.gitlab.com/) or [Github](https://github.com/) to manage your code online with an advanced interface to resolve merged conflict that occurs frequently for asynchronous work. 

Keeping a standardized environment for development keeps python package dependencies consistent, and together with Git, allows different members to easily switch between different machines such as local machines or machines in the cloud. One popular option that manages the environment is [Conda](https://docs.conda.io/en/latest/) (environment.yml) 

More in-depth info can be found in 3-collab-dev-platforms/repo-structure-setup.md.

## Model/Weight/Data versioning
Shared storage such as cloud storage ensures the team is assessing the correct dataset and having access to a shared transformed dataset cuts down data preprocessing/transformation time allowing the engineer to focus on modeling. Also, weights and datasets should not be push to the version control system, as the repository size might become too large for the local machine.

Having a system to keep track of the trained model and the corresponding dataset early on will prove to be fruitful, as more experiments will make it difficult to trace back. One good practice will be to save the checkpoints and the models together and keep track of the corresponding dataset used for the training. Recommended tools include [MLflow](https://mlflow.org/) and [Weights & Biases](https://wandb.ai/site) for tracking experiments and versioning models. [DVC](https://dvc.org/) and [neptune.ai](https://neptune.ai/) for Data Version Control. Take note even a shared spreadsheet keeping track of model/weights/dataset versioning will pay off eventually.

It is also possible to set up cloud-based compute development environment where all collaborators can share the same environment and tools(VScode, Jupyter Lab) and shared storage. Some of the examples are Amazon EC2 Instance Types, Data Science Virtual Machine and Google Compute Engine