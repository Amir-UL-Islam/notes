### 🧠 #1 SOLID - A set of five design principles

> "Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion."

SOLID is an acronym for five design principles that promote cleaner, more maintainable software. These principles help software engineers write code that is easier to understand, extend, and modify.

By following SOLID, you ensure that your software design is flexible and scalable. It reduces the risk of changes breaking existing functionality, which is crucial when working on large systems. Here's a breakdown of each principle:

- **SRP - Single Responsibility Principle**
    
    - **Why it matters**: Each class should have one responsibility, meaning it should have only one reason to change. This makes your code easier to understand and modify.
        
    - **How to apply it**: Break down your classes so that each one has a clear, singular responsibility. For instance, in a user management system, you might separate the logic for user authentication and user profile management into different classes. It’s okay to have a single user class at the beginning, but be ruthless splitting in simpler classes.
        
- **OCP - Open/Closed Principle**
    
    - **Why it matters**: Software should be open for extension but closed for modification. This allows you to add new functionality without altering existing code, reducing the risk of introducing bugs.
        
    - **How to apply it**: Use inheritance or interfaces to extend the behavior of your classes. For example, you can add new features by creating subclasses or implementing new interfaces rather than modifying the original class.
        
- **LSP - Liskov Substitution Principle**
    
    - **Why it matters**: Derived classes must be substitutable for their base classes without altering the correctness of the program. This ensures that your class hierarchy is logically sound and predictable.
        
    - **How to apply it**: Ensure that objects of a subclass can be used interchangeably with the parent class. For example, a `Square` class should be able to replace its parent `Rectangle` class without breaking the code that works with the `Rectangle`.
        
        [
        
        ![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdec1c3ad-c79c-4ab2-b0a3-b21d262a0250_1000x712.png)
        
        
        
        ](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fdec1c3ad-c79c-4ab2-b0a3-b21d262a0250_1000x712.png)
        
        [source](https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898)
        
- **ISP - Interface Segregation Principle**
    
    - **Why it matters**: Clients should not be forced to depend on interfaces they do not use. This helps keep your interfaces simple and focused, preventing unnecessary dependencies and making the code easier to understand.
        
    - **How to apply it**: Split large interfaces into smaller, more specific ones. For instance, if an interface `Shape` has methods for both `draw()` and `resize()`, split it into two separate interfaces: `Drawable` and `Resizable`.
        
- **DIP - Dependency Inversion Principle**
    
    - **Why it matters**: High-level modules should not depend on low-level modules; both should depend on abstractions. This decouples your system, making it more flexible and easier to maintain.
        
    - **How to apply it**: Depend on interfaces or abstract classes rather than concrete implementations. For example, instead of hardcoding a specific database connection class, use an interface for the database operations, allowing different implementations (e.g., MySQL, PostgreSQL).
        

By applying these principles, you'll create software that is easier to maintain, test, and extend while avoiding common pitfalls like tightly coupled code and excessive complexity.

### 🔧 #2 KISS - Keep It Simple, Stupid

> Where to place the comma matters 😛.  
> It's up to you to decide if the code should be stupid or if we are the stupid ones writing complex code.

The KISS principle emphasizes simplicity in design. Avoid over-complicating your codebase with unnecessary features or complex structures. Keeping things simple leads to maintainable and easy-to-debug code.

**Why it matters:** Software that is simple is easier to understand, debug, and modify. By focusing on simplicity, you reduce the chances of introducing errors and increase productivity over time.

**How to apply it:** When designing software, always ask yourself if there’s a simpler solution that still meets your requirements. Avoid adding features that aren’t needed right now, and focus on creating a clean, straightforward implementation.

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F51df9872-6eef-459c-bb52-5a30e4fa83eb_1140x1140.jpeg)



](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F51df9872-6eef-459c-bb52-5a30e4fa83eb_1140x1140.jpeg)

[source](https://www.comicagile.net/comic/simplicity/)

---

### 🛠️ #3 EAFP - Easier to Ask Forgiveness than Permission

This principle suggests that it's often more efficient to handle exceptions after they occur, rather than checking for every condition before performing an action. It’s a mindset shift from over-engineering to flexibility.

Unless you are a tech giant and a mistake can cost you millions, better to iterate fast than to have 100% certainty. Having 100% certainty means you are moving slow.

**Why it matters:** In software development, you can save time by assuming things will work and catching exceptions when they don’t. Over-checking conditions can make your code unnecessarily complicated and harder to maintain.

**How to apply it:** Instead of validating every possible error condition up front, try executing the action first and catch the exceptions if they occur. This approach keeps your codebase simpler and more readable.

---

### 🧐 #4 LBYP - Look Before You Leap

This principle is the opposite of EAFP. It advises engineers to check for conditions and edge cases before executing actions, preventing errors and ensuring the stability of the system.

**Why it matters:** By checking conditions before performing actions, you reduce the likelihood of errors and unexpected behavior. This approach helps you write safer code, especially when interacting with external systems or complex data.

**How to apply it:** Always validate inputs and conditions before executing an action. If you’re interacting with a database, for example, check that the data is valid before updating records.

[

![Ask Forgiveness : r/webcomics](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fad2022d7-f85d-456d-a130-050f7b07cb6f_672x864.jpeg "Ask Forgiveness : r/webcomics")



](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fad2022d7-f85d-456d-a130-050f7b07cb6f_672x864.jpeg)

---

### ⚙️ #5 BDD - Behavior-Driven Development

BDD is an agile software development approach that involves writing tests in a natural language format, allowing all stakeholders (including non-developers) to understand and contribute to the development process. I’m sure you have worked in codebases with “Given/When/Then“ unit tests.

**Why it matters:** BDD encourages collaboration between developers, QA, and non-technical stakeholders. It ensures that everyone understands the expected behavior of the software, improving the quality of communication and reducing misunderstandings.

**How to apply it:** Write tests in plain language that describe the system’s behavior from the user’s perspective. Work with your team to ensure these tests cover all key user interactions and edge cases.

[

![Implementing Behavior-Driven Development in your organisation | by Marko  Jevtic | alephnull.eu | Medium](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe98d174f-0882-49b3-a831-d6e3b3370957_923x322.png "Implementing Behavior-Driven Development in your organisation | by Marko  Jevtic | alephnull.eu | Medium")



](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe98d174f-0882-49b3-a831-d6e3b3370957_923x322.png)

[source](https://medium.com/alephnulleu/implementing-behavior-driven-development-in-your-organisation-e5be0c33787c)

---

### 🔄 #6 TDD - Test-Driven Development

TDD is a software development process where you write tests before you write the code to pass them. This ensures that your code meets requirements from the start and helps catch bugs early.

The point is to always write a test case based on the requirements that fails because it’s not yet implemented. Then iterate, first making the test pass, then writing the next test that fails.

**Why it matters:** TDD leads to better-designed, more reliable software. By writing tests first, you ensure that your code is built with testability in mind, making it easier to refactor and maintain.

**How to apply it:** Start by writing a test that defines the behavior you want to implement. Then, write the minimal code necessary to pass the test. Repeat this cycle of writing a test, coding, and refactoring as needed.

[

![Test-Driven Development – Comic Agilé](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9c309551-a948-46a5-8159-d67e10cb29dc_1140x1003.jpeg "Test-Driven Development – Comic Agilé")



](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9c309551-a948-46a5-8159-d67e10cb29dc_1140x1003.jpeg)

[source](https://www.comicagile.net/comic/test-driven-development/)

---

### 🪠 #7 CI/CD - Continuous Integration/Continuous Deployment

CI/CD is a set of practices that involve automatically integrating code changes and deploying them to production frequently. This helps improve code quality and accelerates delivery.

**Why it matters:** With CI/CD, you can catch integration issues early and deploy changes faster and more reliably. It reduces the risk of deployment errors and enables faster iterations.

**How to apply it:** Set up automated build and deployment pipelines that integrate code from all developers and run tests automatically. When changes pass all tests, they can be deployed to production with minimal manual intervention.

[

![You Need DevOps](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F365af620-4247-4f42-ba24-3348c5f3ef88_2500x2200.jpeg "You Need DevOps")



](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F365af620-4247-4f42-ba24-3348c5f3ef88_2500x2200.jpeg)

[source](https://www.comicagile.net/comic/you-need-devops/)

---

### 🚫 #8 DRY - Don't Repeat Yourself

The DRY principle aims to reduce duplication in code. By avoiding repetition, you can keep your codebase smaller, more manageable, and easier to maintain.

**Why it matters:** Repeated code is harder to modify and leads to bugs when changes need to be made in multiple places. By following DRY, you ensure that each piece of logic exists in one place, making your code easier to maintain and less error-prone.

**How to apply it:** Extract common functionality into reusable functions, classes, or modules. If you find yourself writing the same code multiple times, consider refactoring it into a shared utility.

[

![Write Readable Code](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F34f73c1c-9aa4-42df-8736-0681f295f785_774x294.png "Write Readable Code")



](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F34f73c1c-9aa4-42df-8736-0681f295f785_774x294.png)

---

### 💸 #9 YAGNI - You Aren't Gonna Need It

YAGNI encourages developers to only build what is required right now. Avoid adding features or functionality unless there is a clear and present need. The truth is that we are clueless about how the code will evolve. Avoid premature optimization.

**Why it matters:** Over-engineering can lead to wasted time, unnecessary complexity, and future maintenance headaches. YAGNI helps focus development efforts on what’s most important at the moment.

**How to apply it:** Focus on the immediate requirements of your project and build only what’s necessary. Avoid designing features that you think might be useful in the future but don’t currently have a clear use case.

[

![YAGNI](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe68414fa-df26-45f4-bba8-02ff32ddf28f_735x688.jpeg "YAGNI")



](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe68414fa-df26-45f4-bba8-02ff32ddf28f_735x688.jpeg)

[source](https://www.monkeyuser.com/2019/yagni/)

---

### 🧩 #10 SOC - Separation of Concerns

SOC is a design principle that recommends separating different aspects of software into distinct modules or layers, each with its own responsibility.

**Why it matters:** By separating concerns, you create modular, maintainable systems. It allows teams to work on different components independently, reduces complexity, and improves scalability.

**How to apply it:** Break your software into distinct layers or modules. For example, separate the business logic, user interface, and data access layers, ensuring each layer has a single responsibility

[

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0c00007e-5bcb-48c1-b08b-0d638e952f6d_657x659.png)

](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0c00007e-5bcb-48c1-b08b-0d638e952f6d_657x659.png)