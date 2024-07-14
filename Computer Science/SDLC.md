---
alias: Software Development Lifecycle
---

- SDLC (Software Development Life Cycle) is a systematic approach to software development that aims to minimize project risks and ensure that software meets customer expectations during delivery
- It consists of several key stages: 
    - ==Planning==: includes tasks like cost-benefit analysis, scheduling, resource estimation, and allocation, with a software requirement specification document setting expectations and defining common goals for project planning.
    - ==Requirement Analysis==: involves gathering, analyzing, and documenting software requirements from the client, stakeholders, and end-users.
    - ==Design==: involves software engineers analyzing requirements and identifying the best solutions to create the software, considering factors like integration with existing IT infrastructure.
    - ==Build== / ==Implementation==: involves coding the product, with the development team analyzing requirements to identify smaller coding tasks that can be completed daily to achieve the final result.
    - ==Documentation==
    - ==Testing==: involves automation and manual testing to check the software for bugs and ensure it meets customer requirements.
    - ==Deployment==: involves releasing the software to production and making it available to end-users.
    - ==Maintenance==
- [[CI & CD|CI/CD]] helps automate and integrate these stages to enable faster and more reliable releases.
- SDLC models include the waterfall model, Agile model, iterative model, spiral model, and V-shaped model, each with its own unique process for addressing project challenges.
- Security is critical to the SDLC, with DevSecOps practices emphasizing the integration of security assessments throughout the entire SDLC to ensure that software is secure from initial design to final delivery.
- Effective communication across the entire team is the most important best practice to implement into an SDLC.
- Common mistakes and challenges in SDLC implementation include failing to account for and accommodate customer and stakeholder needs, project complexity, and a lack of strict adherence to all aspects of the parameters and design plans.

## SDLC Models

### Waterfall

- This model is a linear and sequential model that follows a strict order of phases:
    - Requirements -> Design -> Implementation -> Verification -> Maintenance
        - There's no going back to a certain stage.
        - Decisions from previous phase are permanent.
- It emphasizes strong documentation, low customer involvement, and a sequential structure with little room for changes once a phase is completed.

- **Advantages**:
    - Simple to understand and manage
    - Suitable for small or mid-sized projects with clear requirements
    - High management simplicity due to its rigidity
- **Disadvantages**:
    - Not suitable for complex or object-oriented projects
    - Feedback loop can be slow, making it difficult to apply changes
    - High risks and uncertainty due to lack of flexibility

### Agile

- This model is designed to facilitate change and eliminate waste processes. 
- It emphasizes collaboration, working software, and customer involvement. 
- It is highly adaptive and encourages iterative development, allowing for frequent changes based on customer feedback.

- **Advantages**:
    - Quick delivery of working projects
    - Emphasizes collaboration and direct communication
    - Allows for frequent changes based on customer feedback
- **Disadvantages**:
    - High dependency on customer interaction
    - Documentation is often completed at later stages
    - May not be suitable for projects with strict requirements or limited resources
- Before Agile:
    - Waterfall
    - Other solutions:
        - XP
        - Lean
        - BFC / Toyota Way
- Each Agile methodology tends to follow the same basic process, which includes:
    - Project planning
    - Product roadmap creation
    - Release planning

#### The Agile Manifesto

> **[The Agile Manifesto](https://agilemanifesto.org/)**

- **Values**:
    - ==Individuals and interactions== over processes and tools
    - ==Working software== over comprehensive documentation
    - ==Customer collaboration== over contract negotiation
    - ==Responding to change== over following a plan
- **Principles**
    - MVP through continuous delivery
    - Welcome changes in requirements
    - Collaboration across domains
    - Trust in motivated individuals
    - Direct communication
    - Sustainable development
    - Reflection and adaptation
- **Key Components**
    - User stories
        - High-level definitions of a work request.
        - A short, simple description is written from the user’s perspective and focuses on outlining what your client wants (their goals) and why.
        - It contains minimal information so the team can produce a reasonable estimate of the effort required to accomplish the request.
        - General format: "As a _user_ I want to _functionality_ so that _motivation._"
            - e.g. As a manager, I want to be able to understand my team members' progress, so I can better report our success and failures.
    - Sprints
        - A short iteration, usually between one to three weeks to complete, where teams work on tasks determined in the sprint planning meeting. 
        - Continuously repeated until the product is feature ready.
        - Once the sprint is over, review the product to see what is and isn’t working, make adjustments, and begin another sprint to make improvements.
        - Implemented in the Agile framework Scrum but not in some other frameworks like Kanban.
    - Stand-up meetings
        - Daily stand-up meetings (under 10 minutes), also known as “daily Scrum meetings,” are a great way to ensure everyone is on track and informed.
        - Participants are required to stay standing to keep the meetings short and to the point.
    - Agile board
        - Helps teams track the progress of a project.
        - Can be a whiteboard with sticky notes, a simple Kanban board, or a function within a project management software.
    - Backlog
        - As project requests are added through the intake system, they become outstanding stories in the backlog.
        - During Agile planning, teams will estimate story points to each task.
        - During sprint planning, stories in the backlog are moved into the sprint to be completed during the iteration.
        - Managing the backlog is a vital role for project managers in an Agile environment.
- **Mindset**
    - Learning
    - Doing
    - Reflection
    - Adaptation

#### Extreme Programming (XP)

- XP is an Agile software development framework that emphasizes frequent iteration, collaboration, and adaptation.
- It is based on five core values:
    - **Communication**
        - XP recognizes that problems often arise due to a lack of communication. 
        - It emphasizes continuous and constant communication among team members, managers, and customers.
    - **Simplicity**
        - XP believes in "doing the simplest thing that could possibly work" and implementing a new capability in the simplest possible way.
    - **Feedback**
        - XP encourages frequent feedback, with working software delivered early to the customer for feedback and necessary changes.
    - **Courage**
        - XP provides courage to developers to focus on what is required, communicate and accept feedback, tell the truth about progress and estimates, refactor the code, adapt to changes, and throw away code when necessary.
    - **Respect**
        - Everyone contributes value, and management respects the right of developers to accept responsibility and receive authority over their own work.
#### Scrum

- Scrum is a framework for Agile development that is designed to facilitate rapid development and delivery of high-quality software.
- It is based on a set of principles and practices that promote continuous improvement, collaboration, and transparency:
    - It is based on the idea of *breaking down complex projects* into smaller, more manageable pieces and iterating on them over time.
    - It promotes the idea of *iterative and incremental development*, with each iteration adding new features and functionality.
    - It emphasizes the importance of *self-organizing teams*, where team members are empowered to make decisions and take ownership of their work.
    - It promotes *transparency* by encouraging regular communication and collaboration between team members and stakeholders.
- It divides the entire project into small incremental builds, with each iteration lasting from one to three weeks.
- It is often used in conjunction with other Agile methodologies, such as Kanban, to create a more comprehensive approach to software development.
- Scrum ceremonies
    - aka Scrum events, Scrum meetings, or Agile ceremonies
    - form the backbone of the methodology
        - Spring Planning
        - Daily Stand-up
        - Sprint Review
        - Sprint Retrospective
    - Sprint planning occurs before the sprint, daily stand-up meetings take place during the sprint, and the review and retrospective come after the sprint has ended.

