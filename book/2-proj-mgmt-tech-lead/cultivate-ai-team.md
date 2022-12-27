# How can I cultivate an effective and cohesive AI development team?  
Contributor: Kenny WI Chua, Senior AI Engineer

---  

## Introduction  
Engineers in charge of a development team take on the role of a technical lead. This entails a set of responsibilities that are distinct from those of an individual contributor. Engineers, especially those who are inexperienced with leadership responsibilities, may face challenges in rallying their team.

An effective team is one that is able to deliver project requirements on time and on target. A cohesive team is one that is well-aligned towards a single, common goal. This article provides suggestions on promoting effective and cohesive teams by operationalising general leadership principles within the context of an AI development team. 

The article assumes that the reader has some (but not necessarily extensive) knowledge of a AI project life cycle and typical activities that occur in each stage.

## Promote a shared vision  
During early stages of a project, developers can come onboard with divergent expectations of project deliverables. They will also come with their own set of (sometimes rigid and specific) expectations on what they wish to learn from a project, e.g., specific tech stacks. These factors present a risk to the cohesiveness of the team.

It is therefore the responsibility of the technical lead to promote a shared vision for the team. This vision includes the technical direction, scope and expected quality of work. The early stages of the project represents a critical window to align expectations on the project vision. As much as possible, the project vision ought to be practically and tangibly laid out in the form of system [architecture diagrams](../8-documentation-handover/documenting-architecture-processes.md), rather than left as potentially ambiguous textual/verbal descriptions. Areas that are out-of-scope also need to be made explicit as much as possible, such that the team can come to a common understanding of the work that needs to be prioritised for project delivery.

An effective vision requires buy-in from the project team. One way to facilitate this is to articulate how developers can benefit from the project. This frequently comes in the form of opportunities for professional/technical growth, e.g., by learning new technologies. However, it should also be carefully hedged that the choice of technologies used in the project need to be guided by project requirements rather than learning needs. While it is critical to foster technical growth amongst junior developers, their learning should occur in the form of on-job-training while keeping project needs as a priority.

## Model the way  
A technical lead may have a specific mental picture of the deliverables and ideal approach for a given task, but the end result may differ when delegated to developers. One possible reason is imperfect communication, such that developers do not entirely understand the specifications that have been laid out (hence the need for architecture diagrams). Alternatively, developers may not be entirely convinced about the need to adhere strictly to certain best practices.

In such a context, it is important for the technical lead to be able to demonstrate some of these values and practices that he/she espouses. For example, a technical lead can cultivate a team habit of writing well-structured and documented code by taking on a few of such tasks himself/herself. This may be particularly fruitful when onboarding a new team of junior developers who are not yet familiar with the required standards.

A technical lead can cultivate an environment for innovation by enforcing a no-blame culture for failed experiments. This involves focusing on and rectifying the work process that led to the failure, rather than paying attention to the personnel involved. There is also a need to choose the *correct* measurement of success. For example, developers should not be judged in terms of model evaluation metrics, which are strongly dependent on data quality which is largely beyond the team's control. It would perhaps be fairer and more fruitful to assess the developers' adherence to best practices (e.g., judicious data splits, systematic model experimentation).

As the technical lead, take responsibility for the team's failures, while giving full credit to the team for success. While there is a need to balance practical considerations of the project, the aim of these activities is to build a safe space that encourages developers to experiment.

## Challenge the process
Developers within the team can come from different backgrounds, and can therefore contribute diverse, innovative ideas. Taken discerningly, this can present a significant advantage for the project.

Complementing an innovative culture, an effective team also strives for iterative improvement that brings the project closer to established best practices. This requires the technical lead to keep up to date by spending a significant portion of his/her time reading broadly about and evaluating best practices for each stage of the AI project lifecycle. Such information can be obtained by discerningly following tech blogs and influential thought leaders on social media platforms. Reading/research need not be confined to the specific subdomain of the current project, as ideas in other areas may be transferrable or can provide inspiration.

Iterative improvements come at the inter- and intra-project levels. At the inter-project level, an experienced technical lead can evaluate past projects to identify areas of workflow improvement. The technical lead can also network and share regularly with other technical leads in order to facilitate inter-project transfer of ideas. At an intra-project level, Agile philosophy stresses the importance of iterative development. When time allows, the project team can revisit previously written code in order to further improve it to more closely align with best practices.

## Enable others to act  
The primary responsiblity of the technical lead is to be an enabler rather than a "super contributor". While a technical lead can contribute directly to the codebase at times, he/she needs to be aware that this comes with a trade-off of spending less time on enablement activities. Enabling activities are those that amplify/multiply the effectiveness of the team. These include researching and evaluating potential approaches, planning and delegation, as well as removing technical blockers.

Technical enablements include boilerplate code and abstract classes, which can help developers onboard more quickly and with greater consistency. Additionally, a robust [MLOps workflow](../5-data-mgmt-exp-proc/e2e-workflow.md) provides automation that enables to developers to concentrate of feature development and modelling activities rather than infrastructural work.

Pay particular attention during stand-up meetings and sprint retrospectives. These are platforms during which developers are likely to raise their concerns regarding technical blockers. The technical lead can triage the list in order to identify and resolve the most urgent and important blockers. Relatedly, regular one-on-one meetings with developers can also help encounter personal/interpersonal blockers that may not surface during meetings with the whole team.

## Encourage the heart  
Morale is a key driver of an effective and cohesive development team. Developing under tight deadlines and high expectations is stressful, so take time to celebrate small project milestones. Beyond providing words of affirmation, demonstrate your appreciation for the team in tangible ways that will actually help/be appreciated by the developers.

For example, encourage the team to slow down after a particularly challenging sprint, or gather the team for a nice lunch after a milestone deployment. While some of these activities can incur some short-term costs in terms of time, the idea is to provide some time and space for developers to recharge so that can be greater long-term gains.

## References
- [The Leadership Challenge: How to Make Extraordinary Things Happen in Organizations](https://www.wiley.com/en-us/The+Leadership+Challenge%3A+How+to+Make+Extraordinary+Things+Happen+in+Organizations%2C+6th+Edition-p-9781119278962)
- [1-on-1s](https://github.com/LappleApple/awesome-leading-and-managing/blob/master/One-on-Ones.md)
- [Your team needs a tech lead, not a lead techie](https://zuehlke.github.io/machines-code-people/articles/tech-lead-needed.html)