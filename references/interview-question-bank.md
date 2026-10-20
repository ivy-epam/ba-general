---
description: Pre-defined interview question bank for analyst candidates, grouped by aspect. Used by the assess-candidate skill.
---

# Interview Question Bank

Questions for every interview aspect except **candidate assessment focuses**, which `assess-candidate` generates per candidate. How many questions each aspect gets is set by the allocation in `assess-candidate` Step 6.

| Aspect | Section | When to use |
|---|---|---|
| Analysis focus | [Business](#business-analysis) · [System](#system-analysis) · [Data](#data-analysis) | Only the 1–2 focuses confirmed for the role |
| Plus responsibility | [Project Manager](#project-manager) · [Product Owner](#product-owner) · [Scrum Master](#scrum-master) · [Quality Assurance](#quality-assurance) | Only the plus responsibility confirmed for the role, if any |
| Agile methodology | [Agile](#agile-methodology) | Every interview |
| AI use in daily work | [AI](#ai-use-in-daily-work) | Every interview |
| Soft skills | [Soft skills](#soft-skills) | Every interview |

**Type:** **Mandatory** questions are always selected when their section is used and count toward its allocation; **Optional** questions are selected per candidate, with a rationale. **Competency** names match `references/seniority-competency-definition-business-analysis.md` where one applies.

**When editing the bank:** a section's Mandatory questions must never exceed its smallest allocation in `assess-candidate` Step 6 — Business/System/Data ≤ 4 (when used as a secondary focus with a plus responsibility), each plus responsibility ≤ 3, Agile ≤ 3, Soft skills ≤ 2, AI ≤ 1. Keep fewer than the maximum so Optional picks can tailor the interview.

## Business Analysis

| ID | Type | Competency | Question |
|---|---|---|---|
| BA-01 | Mandatory | BA SDLC awareness | Walk me through one project from intake to production. What did you personally own at each stage, and what did you hand over to others? |
| BA-02 | Optional | Business Analysis Approach Definition | You join a new project as the only BA. What factors would shape your BA approach — ways of working, deliverables, tools — and how would you agree it with the team? |
| BA-03 | Optional | Elicitation of information | You join a company where the sales process is manual and error-prone. How would you discover and document the current process, and how would you confirm it reflects what people actually do? |
| BA-04 | Optional | Elicitation of information | Business stakeholders have only a vague idea of what they want. How would you gather and clarify their requirements? |
| BA-05 | Optional | Business analysis information management | You need to model a business process spanning several external vendors and internal departments. Which techniques and notation would you use, and when would you choose a diagram over text requirements? |
| BA-06 | Mandatory | BA artifacts documentation | Rewrite this requirement as a user story with acceptance criteria: *"The system should be fast and easy to use for managers."* |
| BA-07 | Optional | BA Quality control | How do you decide a requirement is ready for development? What do you check, and who is involved? |
| BA-08 | Optional | BA Quality control | Several departments have conflicting requirements for a new CRM system. How would you validate them and reach agreement? |
| BA-09 | Optional | BA Quality control | How do you keep requirement quality consistent across distributed vendor teams? |
| BA-10 | Optional | Business analysis information management | How do you keep requirements up to date and accessible to business, engineering, and project teams as they change? |
| BA-11 | Mandatory | Requirements approval and prioritization | You're asked to define the MVP scope. How would you set priorities, and what factors drive the decisions? |
| BA-12 | Optional | Requirements and Change management | Mid-delivery, a senior stakeholder asks for a "small" addition. How do you protect scope while still accommodating a genuinely critical change? |
| BA-13 | Optional | Requirements and Change management | A new regulation requires changes to several business processes. How would you assess the impact, update documentation, and ensure compliance? |
| BA-14 | Optional | BA Stakeholders management | A critical risk is discovered mid-project that could delay delivery. How would you communicate it, and what would you do to mitigate it? |
| BA-15 | Optional | BA Stakeholders management | How do you analyse the stakeholders on a new project, and how does that change how you communicate with management, developers, and QA? |
| BA-16 | Optional | Efforts estimation | How would you estimate the effort for your own BA work on a new feature? Walk me through a recent example. |
| BA-17 | Optional | BA Risk management | In a legacy-to-modern migration, what are the top BA risks, and how would you mitigate them? |
| BA-18 | Optional | Business need definition | A stakeholder asks for a new report "because the current one is wrong". How do you get to the real business need? |
| BA-19 | Optional | Solution assessment | A feature you specified has been live for a month, but users aren't adopting it. How would you find out why and what to do next? |
| BA-20 | Optional | Requirements traceability management | How do you keep traceability between business goals, requirements, and test cases, and when has it helped you? |
| BA-21 | Optional | Understanding the organization | You join a client in an industry you don't know. How do you get up to speed on the domain quickly enough to be useful? |
| BA-22 | Optional | Elicitation Techniques | Which elicitation technique do you rely on least, and in what situation would it still be the right choice? |

## System Analysis

| ID | Type | Competency | Question |
|---|---|---|---|
| SA-01 | Mandatory | System interactions | You need to document how a new e-commerce platform interacts with its payment gateway. Which tools or techniques would you use? |
| SA-02 | Optional | System analysis | You need to understand a legacy inventory management system. What steps would you take to learn its functionality and find areas for improvement? |
| SA-03 | Mandatory | API requirements | What would you include in the requirements for a new customer-portal API? |
| SA-04 | Optional | API integration | You're integrating a third-party payment service via its API. How would you confirm it meets both business and technical requirements? |
| SA-05 | Optional | API requirements | What would you specify for an API's error handling and logging, and why does it matter? |
| SA-06 | Mandatory | Issue analysis | An end user reports a system issue. Walk me through how you gather information, reproduce it, and what you do if you can't reproduce it. |
| SA-07 | Optional | Issue management | You find a critical bug affecting many users. How do you prioritise it and communicate your findings to the team and stakeholders? |
| SA-08 | Optional | Issue management | How do you document the steps and solution from a debugging investigation so the team learns from it? |
| SA-09 | Optional | Issue management | A fix for a user-reported issue introduces a new problem. How do you handle the regression and protect overall system stability? |
| SA-10 | Optional | Non-functional requirements | How would you elicit and specify non-functional requirements — such as performance, availability, and security — for a new system? |
| SA-11 | Optional | Data flow analysis | Data moves between three systems during order processing. How would you document the data flow and field mappings between them? |
| SA-12 | Optional | System behaviour modelling | An order can be created, paid, shipped, cancelled, or refunded. How would you specify its lifecycle and the rules for each transition? |
| SA-13 | Optional | Data modelling | How would you capture the data model for a new feature, and how do you validate it with the development team? |
| SA-14 | Optional | Architecture awareness | How does the choice between a monolith and microservices affect the requirements you write? |
| SA-15 | Optional | Integration patterns | When would you specify synchronous API calls versus asynchronous messaging or events between systems? |
| SA-16 | Optional | Security requirements | What authentication, authorisation, and data-protection requirements would you specify for an application handling customer data? |
| SA-17 | Optional | Migration analysis | You're moving data from a legacy system to a new platform. What would you specify to make the migration safe? |
| SA-18 | Optional | Performance analysis | Users complain that a key screen has become slow. How would you analyse the problem and specify the improvement? |
| SA-19 | Optional | Interface specification | A partner system sends files to yours in batches. What would you include in the interface specification? |
| SA-20 | Optional | Technical documentation | How do you keep system documentation useful for developers and support teams after go-live? |

## Data Analysis

| ID | Type | Competency | Question |
|---|---|---|---|
| DA-01 | Mandatory | Elicitation of information | When starting a new analytics project, what questions would you ask stakeholders to clarify their data requirements? |
| DA-02 | Optional | BA artifacts documentation | Walk me through how you'd document the data requirements for a new reporting solution. Which artifacts would you produce? |
| DA-03 | Optional | Requirements approval and prioritization | Several departments each define "active customer" differently. How would you collect and reconcile these definitions? |
| DA-04 | Optional | Data lifecycle | Take a recent analysis you worked on. What were the steps from the initial question to the final insight, and which step was hardest? |
| DA-05 | Optional | Data preparation | You're given a dataset with missing values and outliers. How would you prepare it for analysis? |
| DA-06 | Optional | Data visualisation | You need to analyse customer purchase data to identify trends. Which tools would you use, and how would you present your findings? |
| DA-07 | Optional | Data integration | You're integrating data from multiple sources (e.g. CRM, ERP, web analytics). How would you ensure consistency and accuracy? |
| DA-08 | Mandatory | Data analysis | Sales figures differ between two departments' reports. How would you investigate and resolve the discrepancy? |
| DA-09 | Optional | Reporting | You're asked to automate recurring analysis reports. What tools and techniques would you use to keep them reliable and scalable? |
| DA-10 | Optional | Data compliance | How would you make sure the data you use for analysis complies with privacy regulations such as GDPR? |
| DA-11 | Optional | Data quality management | You're responsible for data quality in a live dashboard. What metrics and processes would you put in place? |
| DA-12 | Mandatory | KPI definition | A stakeholder asks for a dashboard showing "customer engagement". How would you turn that into measurable KPIs? |
| DA-13 | Optional | Data modelling | How would you design the data model for a reporting solution — for example, choosing between a star schema and a flat table? |
| DA-14 | Optional | SQL and data querying | Walk me through how you'd write a query to find customers whose spending dropped by more than 50% between two quarters. |
| DA-15 | Optional | Stakeholder communication | Your analysis contradicts what a senior stakeholder believes. How do you present the findings? |
| DA-16 | Optional | Data governance | How do you establish ownership and definitions for key data so different teams use it consistently? |
| DA-17 | Optional | Data analysis | How would you design an A/B test to check whether a new checkout flow increases conversion? |
| DA-18 | Optional | Data visualisation | A dashboard has 30 charts and nobody uses it. How would you redesign it? |
| DA-19 | Optional | Data requirements | A source system will change a field your reports depend on. How do you assess and manage the impact? |
| DA-20 | Optional | Data storytelling | Describe a time your analysis changed a business decision. How did you present it to make that happen? |

## Project Manager

| ID | Type | Competency | Question |
|---|---|---|---|
| PM-01 | Optional | Planning | You're both BA and PM on a new project. How do you build the delivery plan, and how does your analysis feed into it? |
| PM-02 | Optional | Risk and issue management | How do you track and manage project risks and issues day to day? Give a recent example. |
| PM-03 | Optional | Status reporting | How do you report project status to senior stakeholders, and what do you do when the project is going off track? |
| PM-04 | Optional | Resource and capacity management | Your team is overcommitted and a new priority arrives. How do you rebalance the work? |
| PM-05 | Mandatory | Role balance | When you hold both the BA and PM roles, how do you keep one from crowding out the other? |
| PM-06 | Optional | Budget and cost control | Your project is forecast to exceed its budget by 15%. What do you do? |
| PM-07 | Optional | Dependency management | Your delivery depends on another team's component that is slipping. How do you manage it? |
| PM-08 | Optional | Project closure | How do you close a project properly, and what do you hand over? |

## Product Owner

| ID | Type | Competency | Question |
|---|---|---|---|
| PO-01 | Optional | Product vision | How do you turn a product vision into a backlog the team can deliver against? |
| PO-02 | Optional | Backlog prioritisation | Three stakeholders each insist their feature is the top priority. How do you decide, and how do you communicate the decision? |
| PO-03 | Optional | Value measurement | How do you know whether a delivered feature actually achieved its goal? |
| PO-04 | Optional | Stakeholder alignment | The team and a key stakeholder disagree on what "done" means for a feature. How do you resolve it? |
| PO-05 | Mandatory | Role balance | As both BA and PO, how do you separate deciding *what* to build from analysing *how* it should work? |
| PO-06 | Optional | Roadmapping | How do you build and maintain a product roadmap when priorities keep changing? |
| PO-07 | Optional | Release planning | How do you decide what goes into a release, and when it's ready to go live? |
| PO-08 | Optional | User feedback | How do you collect user feedback and turn it into backlog items? |

## Scrum Master

| ID | Type | Competency | Question |
|---|---|---|---|
| SM-01 | Optional | Facilitation | How do you keep sprint ceremonies effective rather than routine? Give an example of a change you made. |
| SM-02 | Optional | Impediment removal | A developer is blocked by another team that isn't responding. What do you do? |
| SM-03 | Optional | Team coaching | The team keeps missing its sprint commitments. How would you help them improve? |
| SM-04 | Optional | Agile metrics | Which metrics do you use to understand a team's health and delivery, and how do you avoid misusing them? |
| SM-05 | Mandatory | Role balance | When you're both BA and Scrum Master, how do you stay neutral in discussions where you also hold a requirements view? |
| SM-06 | Optional | Retrospectives | The team's retrospectives produce the same complaints every sprint and nothing changes. What would you do? |
| SM-07 | Optional | Conflict within the team | Two developers have a recurring conflict that is affecting the team. How do you handle it? |
| SM-08 | Optional | Scaling and coordination | Your team must coordinate delivery with three other Scrum teams. How do you keep everyone aligned? |

## Quality Assurance

| ID | Type | Competency | Question |
|---|---|---|---|
| QA-01 | Optional | Test design | How do you derive test cases from a user story's acceptance criteria? Walk me through an example. |
| QA-02 | Optional | Test planning | You're asked to define the testing approach for a new feature. What would your test plan cover? |
| QA-03 | Optional | Defect management | How do you write and manage a defect so developers can act on it quickly? |
| QA-04 | Optional | UAT coordination | How would you plan and run UAT with business users? |
| QA-05 | Mandatory | Role balance | When you both write the requirements and test them, how do you avoid testing only what you expect to see? |
| QA-06 | Optional | Test automation awareness | How do you decide which tests are worth automating? |
| QA-07 | Optional | Risk-based testing | Time is short before a release. How do you decide what to test? |
| QA-08 | Optional | Non-functional testing | How would you make sure performance and security requirements are actually tested? |

## Agile Methodology

| ID | Type | Competency | Question |
|---|---|---|---|
| AG-01 | Optional | BA SDLC awareness | From your experience, how does a BA's day-to-day work differ between Agile and Waterfall delivery? When would Agile not be the right choice? |
| AG-02 | Optional | BA artifacts documentation | You join a team that is new to Agile. How would you introduce user stories and explain why they matter? |
| AG-03 | Mandatory | BA SDLC awareness | What does a BA contribute to each Scrum ceremony — refinement, planning, review, and retrospective? |
| AG-04 | Mandatory | BA Quality control | How do you take a story from idea to "ready" through backlog refinement? What does your Definition of Ready include? |
| AG-05 | Optional | Scope decomposition | How do you split a large epic into stories that each deliver value within a sprint? |
| AG-06 | Optional | BA SDLC awareness | On an Agile team with both a BA and a Product Owner, how would you divide responsibilities? |
| AG-07 | Optional | Agile estimation | How do you take part in story estimation, and what do you do when the team's estimates vary widely? |
| AG-08 | Optional | Definition of Done | What should a team's Definition of Done include, and how does it differ from acceptance criteria? |
| AG-09 | Optional | Kanban | When would you recommend Kanban over Scrum for a team, and what changes for the BA? |
| AG-10 | Optional | Agile at scale | Have you worked in a scaled Agile setup (e.g. SAFe)? How did requirements flow from portfolio to team level? |

## AI Use in Daily Work

| ID | Type | Competency | Question |
|---|---|---|---|
| AI-01 | Mandatory | GenAI for BA Productivity & SDLC | Which AI tools do you use in your BA work? Walk me through one task where AI helped, and how you checked the output. |
| AI-02 | Optional | GenAI for BA Productivity & SDLC | How do you verify the accuracy and relevance of AI-generated requirements or documentation before sharing them? |
| AI-03 | Optional | GenAI for BA Productivity & SDLC | What information would you never put into an AI tool, and how do you work within your organisation's AI policy? |
| AI-04 | Optional | GenAI for BA Productivity & SDLC | How would you use AI to draft acceptance criteria for a user story? Describe the prompt you'd write. |
| AI-05 | Optional | GenAI for BA Productivity & SDLC | When introducing an AI tool into an existing team workflow, what do you consider to ensure adoption and measurable value? |
| AI-06 | Optional | GenAI for BA Productivity & SDLC | How do you stay current on AI tools, and how do you decide whether a new tool suits a specific task? |
| AI-07 | Optional | GenAI BA Modelling & Diagramming | Have you used AI to create diagrams or models, such as process flows? How did you check them? |
| AI-08 | Optional | GenAI for BA Productivity & SDLC | Give an example where AI gave you a wrong or misleading answer during your work. How did you catch it? |
| AI-09 | Optional | GenAI BA Visualisation & Prototyping | How could AI help you prototype or visualise a requirement for stakeholders? |
| AI-10 | Optional | GenAI for BA Productivity & SDLC | How would you measure whether using AI is actually making your BA work better? |

## Soft Skills

| ID | Type | Competency | Question |
|---|---|---|---|
| SS-01 | Optional | Collaboration | You're on a cross-functional team spread across countries. Midway through, language barriers and different work styles cause communication breakdowns. What would you do? |
| SS-02 | Optional | Expectation management | During UAT, a client insists on a last-minute change they call critical. Your team is stretched and the PM is unavailable. How do you handle it? |
| SS-03 | Mandatory | Communication | Tell me about a time you explained a complex idea to a non-technical stakeholder. How did you make sure they understood? |
| SS-04 | Optional | Initiative | Give an example of an improvement you identified and drove in your team or project, without being asked. |
| SS-05 | Optional | Conflict management | Tell me about a disagreement with a developer or stakeholder over a requirement. How was it resolved? |
| SS-06 | Optional | Ownership | Tell me about a time something went wrong on a deliverable you owned. What did you do? |
| SS-07 | Optional | Adaptability | Tell me about a time priorities or scope changed suddenly. How did you adapt? |
| SS-08 | Optional | Influencing without authority | How have you persuaded a stakeholder to change direction when you had no authority over them? |
| SS-09 | Optional | Feedback | Tell me about a time you received critical feedback on your work. What did you do with it? |
| SS-10 | Optional | Time management | How do you manage competing deadlines from several stakeholders? |
