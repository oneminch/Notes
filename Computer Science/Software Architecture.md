
> [!example]- Learning Roadmap
> - [Software Design and Architecture Roadmap](https://roadmap.sh/software-design-architecture)
> 
> - [How to Learn Software Design and Architecture | The Full-stack Software Design & Architecture Map](https://khalilstemmler.com/articles/software-design-architecture/full-stack-software-design/)
> - [Everything You NEED to Know About WEB APP Architecture - YouTube](https://www.youtube.com/watch?v=sDlCSIDwpDs)
> - [Client-Side Architecture Basics (Khalil Stemmler)](https://khalilstemmler.com/articles/client-side-architecture/introduction/)
> - **Microservices**
>     - *Crash Course*: [Microservices Explained](https://www.youtube.com/watch?v=T-m7ZFxeg1A)
>     - [Microservices (Telusko)](https://www.youtube.com/watch?v=Jl9OKQ92SJU&t=36392s)
>     - [Testing of Microservices - Spotify Engineering : Spotify Engineering](https://engineering.atspotify.com/2018/01/testing-of-microservices/)
> - **Front-End Architecture**
>     - [Fundamentals of Frontend Architecture (Frontend at Scale)](https://frontendatscale.com/courses/frontend-architecture)
> - **Local-First** 
>     - [Local-First Web Development](https://localfirstweb.dev/)
>     - [A Local-First Case Study | jakelazaroff.com](https://jakelazaroff.com/words/a-local-first-case-study/)
> - Twelve Factor Apps
>     - https://12factor.net/

---
## Patterns

### Monolithic

- This pattern consists of a single, unified unit for the entire application.
- All components exist in a single codebase.
    - They are tightly integrated and deployed together.
- Examples:
    - A simple web application that serves HTML pages with a backend that handles user data, such as a blog or a CMS.
    - A mobile or desktop application that has a single executable, such as Microsoft Word.
- **Advantages**:
    - Simple and easy to develop for small to medium-sized applications.
    - Fast development cycles and quicker time-to-market for new features.
    - Simpler deployments with less risk of deployment errors.
    - Easier to understand how different parts of the application work together
    - Easier to debug and trace issues with tools.
- **Disadvantages**:
    - Becomes more complex and harder to manage as the application grows.
    - Debugging and tracing issues can become difficult in large applications.
    - Limited flexibility in technology choices and scalability options.

### Multi-Tier

- This pattern divides the application into multiple layers or tiers.
- Each tier is responsible for a specific functionality or task.
    - Commonly used layers include presentation, application, and data layers.
- It's ideal for 
    - new applications that need to be built quickly, 
    - enterprise or business applications, 
    - teams with inexperienced developers, and 
    - applications requiring strict maintainability and testability standards.
- Examples:
    - A distributed system that has a separate presentation layer for the user interface, an application layer for the business logic, and a data layer for storing data, with each layer running on a separate server or cluster of servers.
- **Advantages**:
    - Allows for easier updating and enhancing of layers separately.
    - Improves maintainability and testability by isolating layers.
- **Disadvantages**:
    - Can lead to a "big ball of mud" if not properly organized.
    - Layer isolation can make it hard to understand the architecture without understanding every module.
    - Monolithic deployment is often unavoidable, requiring complete redeployment for small changes.

### Microservices

- This pattern consists of multiple independent applications, each implementing specific business logic for a function area.
    - They are split based on business functionalities.
    - Each service has its own database and communicates with other services through APIs.
- Examples:
    - A complex web application that has multiple services, such as a shopping cart, payment processing, and inventory/user management
    - A cloud-native application that has multiple services, such as a social media platform with services for user profiles, news feeds, and messaging
- **Advantages**:
    - Faster deployment and testing of individual services
    - Supports multiple technology stacks for different services
    - Segregates subdomains by their characteristics for better availability and security
- **Disadvantages**:
    - Can be more complex to design and implement due to distributed operations and eventual consistency
    - Increased operational overhead due to managing multiple services and databases
    - Requires more planning and coordination to ensure smooth communication between services

### Serverless

- This pattern reduces the requirement for managing servers, allowing developers to focus solely on writing code while cloud providers manage the infrastructure.
- Applications are broken up into individual functions that can be invoked and scaled individually.
- It is ideal for applications with variable workloads and sporadic traffic patterns.
- Examples:
    - Trigger-based actions or running scheduled tasks
    - Building RESTful APIs for web and mobile applications
    - Automating [[CI & CD|CI/CD]] pipelines
    - Integrating with third-party services and APIs
- **Advantages**: 
    - Automation
    - Scalability
    - Productivity
    - Cost Efficiency - pay-per use model can result in cost savings
    - Operational Efficiency - simplified infrastructure management tasks
- **Disadvantages**:
    - Performance issues - delays in response time when unused for a certain period, aka "cold starts"
    - Vendor lock-in
    - Limited flexibility
    - Security - each function can serve as a potential attack surface
    - Monitoring and debugging challenges due to the application's distributed nature
    - Expensive for certain use cases, especially ones with high execution times or frequent invocations
    - Complexity in managing and coordinating multiple functions and services

---
## Further

### Books 📚

- A Philosophy of Software Design (John Ousterhout)

- Building Microservices (Sam Newman)

- Building Micro-Frontends (Luca Mezzalira)

- Clean Architecture (Robert C. Martin)

- Design It! (Michael Keeling)

- Fundamentals of Software Architecture (Mark Richards & Neal Ford)

- Patterns of Enterprise Application Architecture (Martin Fowler)

- Release It! (Michael T. Nygard)

- Software Design Decoded (Marian Petre)

- [SOLID](https://solidbook.io/) (Khalil Stemmler)

- Tidy First? (Kent Beck)

### Learn 🧠

- [Software Design and Architecture (Coursera)](https://www.coursera.org/specializations/software-design-architecture)

- [Domain-Driven Hexagon](https://github.com/Sairyss/domain-driven-hexagon#readme)

#### Front-End Architecture

- [Architectures of modern Front-end applications](https://blog.meetbrackets.com/architectures-of-modern-front-end-applications-8859dfe6c12e)

- [Front End System Design Guide (GreatFrontEnd)](https://www.greatfrontend.com/system-design)

- [Frontend System Design Interview Guide](https://www.frontendinterviewhandbook.com/front-end-system-design)

- [Front-End System Design (YouTube)](https://www.youtube.com/playlist?list=PLI9W87-Dqn7j_x6QtR6sUjycJR7nQLBqT)

### Podcasts 🎙

### Local-First (LoFi)

- [localfirst.fm - A podcast about local-first software development.](https://www.localfirst.fm/)

### Reads 📄

#### Front-End Architecture

- [Build a Simple MVC App From Scratch in JavaScript - Tania Rascia](https://www.taniarascia.com/javascript-mvc-todo-app/) ⭐

- [How to Design a Web Application: Software Architecture 101](https://www.educative.io/blog/how-to-design-a-web-application-software-architecture-101)

- [System Design Guide for Front-end Developers (DEV)](https://dev.to/hellonehha/system-design-guide-for-front-end-developers-5fkl)

### Resources 🧩

- [Architecture Weekly (Substack)](https://www.architecture-weekly.com/)

- [Software Architecture Guide (Martin Fowler)](https://martinfowler.com/architecture/)

#### Front-End Architecture

- [Front-End Engineer (YouTube)](https://www.youtube.com/@FrontEndEngineer)

- [devkodeio/frontend-system-design (GitHub)](https://github.com/devkodeio/frontend-system-design)

- [greatfrontend/awesome-front-end-system-design (GitHub)](https://github.com/greatfrontend/awesome-front-end-system-design)

- [Micro-frontends and composable frontend architectures](https://microfrontend.dev/)

### Roadmap 🗺

- [Software Architect Roadmap](https://roadmap.sh/software-architect)

- [Software Design and Architecture Roadmap](https://roadmap.sh/software-design-architecture)

### Videos 🎥

![Just in Time Architecture - Macklin Hartley - NDC Porto 2023 (YouTube)](https://www.youtube.com/watch?v=REbnvajTlko)

![Basic Microservices (3 NodeJS + 1 Load Balancer containers) with Docker Compose](https://www.youtube.com/watch?v=9sAg7RooEDc)

#### **Front**-End Architecture

- [Front-End System Design (YouTube)](https://www.youtube.com/playlist?list=PLI9W87-Dqn7j_x6QtR6sUjycJR7nQLBqT)