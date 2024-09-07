- [Software Design and Architecture Roadmap](https://roadmap.sh/software-design-architecture)

---

**You Ain't Gonna Need It (YAGNI)**

- Only implement functionality that is actually needed for immediate requirements; try not to implement things that you anticipate will be needed.

**The Don't Repeat Yourself Principle (DRY)**

> Every piece of knowledge must have a single, unambiguous, authoritative representation within a system. [^1]

- Same pieces of code used in multiple places can be merged into a single source and reused on demand.

- SOLID
- KISS

### TDD

### Architectural Patterns

- [[Software Architecture]]

## SOLID

- The SOLID principles are best practices to follow when working with [[Object-Oriented Programming|OOP]] languages.

-  **SRP**
    - **Single Responsibility Principle**
    - Each class should have only one clear responsibility.
    - e.g. A `User` class should be responsible for user-specific tasks like auth.

- **OCP**
    - **Open/Closed Principle**
    - Software entities should be open for extension but closed for modification.
    - New functionality can be added to a system without modifying existing code.
    - In [[Java]], this can be accomplished using interfaces, abstract classes & polymorphism.
    - e.g. A `PaymentProcessor` interface can be implemented to specific needs like `CreditCardProcessor` and `PayPalProcessor`

- **LSP**
    - **Liskov Substitution Principle**
    - Subtypes should be sustitutable for their base types.
    - Any instance of a base class should be able to be replaced by an instance of a subclass without affecting the correctness of the program, or subclasses created should be able to be used in place of their superclass. 
    - The subclass should not change the behavior of the superclass.
    - e.g. In a banking system, `SavingsAccount` & `CheckingAccount` inherit from a base `Account` class. Common features such as deposits and withdraws should remain consistent regardless of the specific account type. According to LSP, a system expecting an instance of `Account` should  seamlessly work with any instance of a subclass. 

- **ISP**
    - **Interface Segregation Principle**
    - Clients should not be forced to depend on interfaces they do not use. 
    - Interfaces should be small and focused, and clients should only depend on the interfaces they need. 
    - Avoid creating large, general-purpose interfaces that are used by many clients. Instead, create multiple small interfaces that are each focused on a specific set of functionality, so that clients can then depend on only the interfaces they need.
    - e.g. In a messaging system, instead of having a single interface with multiple methods (e.g. `sendMessage`, `receiveMessage`, etc), create separate interfaces (e.g. `Sender`, `Receiver`) that clients can implement to match their specific needs.

- **DIP**
    - **Dependency Inversion Principle**
    - High-level modules should not depend on low-level modules. Both should depend on abstractions. 
    - Abstractions should not depend on details. Details should depend on abstractions. 
    - Use interfaces or abstract classes to define the behavior of your classes, and then use dependency injection to provide the specific implementations.
    - e.g In an e-commerce system, an `OrderProcessor` class should depend on a `PaymentGateway` interface instead of a specific payment gateway implementation. This will allow for easier switching between different payment gateway providers without impacting core logic.

---
## Further

### Footnotes 📝

[^1]: [Wikipedia - The DRY Principle](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
