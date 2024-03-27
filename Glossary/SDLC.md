---
alias: Software Development Lifecycle
---

- SDLC (Software Development Life Cycle) is a systematic approach to software development that aims to minimize project risks and ensure that software meets customer expectations during delivery
- It consists of several key stages: 
    - ==Planning==: includes tasks like cost-benefit analysis, scheduling, resource estimation, and allocation, with a software requirement specification document setting expectations and defining common goals for project planning.
    - ==Requirement Analysis==: involves gathering, analyzing, and documenting software requirements from the client, stakeholders, and end-users.
    - ==Design==: involves software engineers analyzing requirements and identifying the best solutions to create the software, considering factors like integration with existing IT infrastructure.
    - ==Implementation==: involves coding the product, with the development team analyzing requirements to identify smaller coding tasks that can be completed daily to achieve the final result.
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

---
## Further

### Books 📚

- Clean Code (Robert C. Martin)

- Modern Software Engineering (David Farley)

- The Mythical Man-Month (Frederick P. Brooks Jr.)

- Code Complete (Steven C. McConnel)

- Refactoring (Martin Fowler)

- The Clean Coder (Robert C. Martin)

- The Rules of Programming (Chris Zimmerman)