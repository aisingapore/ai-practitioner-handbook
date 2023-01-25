# How can I build an effective AI development team?  
Contributor: Kenny WJ Chua, Senior AI Engineer

---  

## Introduction  
The responsbilities of a technical lead are different from those of an individual contributor. Engineers, especially those who are who are unfamiliar with leadership responsibilities, may face a learning curve in fulfilling these responsibilities.

A technical lead indirectly delivers an AI project on time and on target by building an **effective** AI development team. This article provides suggestions on promoting effective teams by contextualising general leadership principles. 

In AISG, an engineer serves as technical lead for a small team of apprentices (i.e., 'developers'). Therefore, the contents of this article would be useful to any AI practitioner who is in a similar leadership role.

This article requires some basic knowledge of a [AI project life cycle](https://www.datacamp.com/blog/machine-learning-lifecycle-explained) and typical activities that occur in each stage. The article on [building a *cohesive* AI development team](../2-proj-mgmt-tech-lead/cohesive-ai-team.md) may also be useful for engineers in the role of technical lead.

## Model the way  
A technical lead may have a specific mental picture of the deliverables and ideal approach for a given task, but the end result may differ when delegated to developers. One possible reason is imperfect communication, such that developers do not entirely understand the specifications that have been laid out (hence the need for architecture diagrams). Alternatively, less experienced developers may not understand the need to adhere strictly to certain best practices.

In such a context, it is important for the technical lead to be able to **demonstrate** some of these values and practices that he/she espouses. For example, a technical lead can cultivate a team habit of writing well-structured and documented code by taking on a few of such tasks himself/herself. This may be particularly fruitful when onboarding a new team of junior developers who are not yet familiar with the required standards.

A technical lead can cultivate an environment for innovation by enforcing a **no-blame culture** for failed experiments. This involves focusing on and rectifying the work process that led to the failure, rather than paying attention to the personnel involved. There is also a need to choose the *correct* measurement of success. For example, developers should not be judged in terms of model evaluation metrics, which are strongly dependent on data quality which is largely beyond the team's control. It would perhaps be fairer and more fruitful to assess the developers' adherence to best practices (e.g., judicious data splits, systematic model experimentation).

As the technical lead, take responsibility for the team's failures, while giving full credit to the team for success. While there is a need to balance practical considerations of the project, the aim of these activities is to build a safe space that encourages developers to experiment.

## Challenge the process
Developers within the team can come from different backgrounds, and can therefore contribute diverse, innovative ideas. Taken discerningly, this can present a significant advantage for the project.

Complementing an innovative culture, an effective team also strives for **iterative improvement** that brings the project closer to established best practices. This requires the technical lead to keep up to date by spending a significant portion of his/her time **reading broadly about and evaluating best practices** for each stage of the AI project lifecycle. Such information can be obtained by discerningly following tech blogs and influential thought leaders on social media platforms. Reading/research need not be confined to the specific subdomain of the current project, as ideas in other areas may be transferrable or can provide inspiration.

Iterative improvements come at the inter- and intra-project levels. At the inter-project level, an experienced technical lead can evaluate past projects to identify areas of workflow improvement. The technical lead can also network and share regularly with other technical leads in order to facilitate inter-project transfer of ideas. At an intra-project level, Agile philosophy stresses the importance of iterative development. When time allows, the project team can revisit previously written code in order to further improve it to more closely align with best practices.

## Enable others to act  
The primary responsiblity of the technical lead is to be an **enabler** rather than a "super contributor". While a technical lead can contribute directly to the codebase at times, he/she needs to be aware that this comes with a trade-off of spending less time on enablement activities. Enabling activities are those that amplify/multiply the effectiveness of the team. These include researching and evaluating potential approaches, planning and delegation, as well as removing technical blockers.

Technical enablements include **boilerplate code and abstract classes**, which can help developers onboard more quickly and with greater consistency. Additionally, a robust [MLOps workflow](../5-data-mgmt-exp-proc/e2e-workflow.md) provides automation that enables to developers to concentrate of feature development and modelling activities rather than infrastructural work.

Pay particular attention during **stand-up meetings** and **sprint retrospectives**. These are platforms during which developers are likely to raise their concerns regarding **technical blockers**. The technical lead can triage the list in order to identify and resolve the most urgent and important blockers. Relatedly, regular **one-on-one meetings** with developers can also help encounter personal/interpersonal blockers that may not surface during meetings with the whole team.

## References
- [The Leadership Challenge: How to Make Extraordinary Things Happen in Organizations](https://www.wiley.com/en-us/The+Leadership+Challenge%3A+How+to+Make+Extraordinary+Things+Happen+in+Organizations%2C+6th+Edition-p-9781119278962)
- [AI project life cycle](https://www.datacamp.com/blog/machine-learning-lifecycle-explained)
- [1-on-1s](https://github.com/LappleApple/awesome-leading-and-managing/blob/master/One-on-Ones.md)
- [Your team needs a tech lead, not a lead techie](https://zuehlke.github.io/machines-code-people/articles/tech-lead-needed.html)