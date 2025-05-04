## What is an Object in Java?

- **interface introduces another problem by introducing one solution?**

An object is an entity in the real world that can be distinctly identified. Objects have states and behaviors. In other words, they consist of methods and properties to make a particular type of data useful.

An object consists of:

- **A unique identity:** Each object has a unique identity, even if the state is identical to that of another object.
- **State/Properties/Attributes:** State tells us how the object looks or what properties it has.
- **Behavior:** Behavior tells us what the object does.
## 1. Abstraction

### **Briefly explain Abstraction**

Abstraction is the concept of hiding complex implementation details and exposing only essential features. It helps in reducing complexity by focusing on what an object does rather than how it does it.

### **2. Example of Abstraction**

```java
abstract class Vehicle {
    abstract void start(); // Abstract method (no implementation)
}

class Car extends Vehicle {
    void start() {
        System.out.println("Car starts with a key.");
    }
}

class Bike extends Vehicle {
    void start() {
        System.out.println("Bike starts with a kick.");
    }
}

```
- **Explanation**: `Vehicle` is an abstract class, and `start()` is an abstract method. The actual implementation is provided by subclasses.
    

### **3. Pros and Cons**

|**Pros**|**Cons**|
|---|---|
|Reduces complexity|Can lead to over-engineering if misused|
|Encourages modularity|Requires careful design to avoid leaky abstractions|
|Enhances code reusability|May introduce performance overhead in some cases|

### **4. Common Problems & Famous Issues**

- **Leaky Abstraction**: When internal details are unintentionally exposed.
```java
    abstract class Database {
        abstract void connect();
        void logConnectionDetails() { // Exposes internal logging mechanism
            System.out.println("Logging DB connection...");
        }
    }
    
```
- **Over-Abstraction**: Creating unnecessary layers.
    

### **5. Ways to Resolve Problems**

- Follow **"Program to an interface, not an implementation"** principle.
	This is a fundamental **OOP design principle** that encourages developers to **depend on abstract interfaces** (or abstract classes) rather than concrete implementations.
	### ❌ **Bad (Tightly Coupled to Implementation)**
	
```java
    class MySQLDatabase {
    public void saveData(String data) {
        System.out.println("Saving to MySQL: " + data);
    }
}

class App {
    private MySQLDatabase db;  // Depends directly on MySQL
    public App() {
        db = new MySQLDatabase();
    }
    public void process(String data) {
        db.saveData(data);
    }
}
```

### ✅ **Good (Program to Interface)**

```java
interface Database {
    void saveData(String data);
}

class MySQLDatabase implements Database {
    public void saveData(String data) {
        System.out.println("Saving to MySQL: " + data);
    }
}

class PostgreSQLDatabase implements Database {
    public void saveData(String data) {
        System.out.println("Saving to PostgreSQL: " + data);
    }
}

class App {
    private Database db;  // Depends on abstraction (interface)
    public App(Database db) {  // Dependency Injection
        this.db = db;
    }
    public void process(String data) {
        db.saveData(data);
    }
}
```


## **Real-World Use Cases**

1. **Dependency Injection (Spring, Guice)**
    - Frameworks inject implementations at runtime.
2. **Collections in Java**
    - `List<String> list = new ArrayList<>();` (Program to `List`, not `ArrayList`).
3. **Strategy Pattern**
    - Different algorithms implement the same interface.

## Principle related t "Program to an interface, not an implementation"
#### **. Dependency Inversion Principle (DIP) – SOLID's 'D'**

**Definition:**

- _"High-level modules should not depend on low-level modules. Both should depend on abstractions."_
    
- _"Abstractions should not depend on details. Details should depend on abstractions."_
    

**How It Connects:**

- **"Program to an interface"** enforces that classes depend on **abstractions (interfaces/abstract classes)** rather than concrete implementations.
    
- This **inverts the dependency** (low-level details depend on high-level policies).
    

**Example:**

```java
// Without DIP (Violation)
class LightBulb {
    void turnOn() { System.out.println("Bulb on"); }
}

class Switch {
    private LightBulb bulb;  // Depends directly on LightBulb (concrete class)
    void operate() { bulb.turnOn(); }
}

// With DIP (Follows "Program to Interface")
interface Switchable {
    void turnOn();
}

class LightBulb implements Switchable {
    public void turnOn() { System.out.println("Bulb on"); }
}

class Fan implements Switchable {
    public void turnOn() { System.out.println("Fan on"); }
}

class Switch {
    private Switchable device;  // Depends on abstraction (interface)
    public Switch(Switchable device) { this.device = device; }
    void operate() { device.turnOn(); }
}

```
**Key Takeaway:**

- `Switch` no longer depends on `LightBulb` (a detail). Instead, both depend on `Switchable` (abstraction).
    

---

### ** Open/Closed Principle (OCP) – SOLID's 'O'**

**Definition:**

- _"Software entities should be open for extension but closed for modification."_
    

**How It Connects:**

- By programming to interfaces, you can **extend functionality** (new implementations) **without modifying existing code**.
    

**Example:**

```java
interface PaymentProcessor {
    void processPayment(double amount);
}

class CreditCardProcessor implements PaymentProcessor {
    public void processPayment(double amount) { 
        System.out.println("Paid via Credit Card: $" + amount); 
    }
}

// Later, add PayPal WITHOUT changing existing code:
class PayPalProcessor implements PaymentProcessor {
    public void processPayment(double amount) {
        System.out.println("Paid via PayPal: $" + amount);
    }
}

class PaymentService {
    private PaymentProcessor processor;  // Depends on abstraction
    public PaymentService(PaymentProcessor processor) {
        this.processor = processor;
    }
    void pay(double amount) {
        processor.processPayment(amount);
    }
}

```
**Key Takeaway:**

- You can add `PayPalProcessor` **without altering** `PaymentService`.
    

---

### **How All Three Concepts Link Together**

| Concept                        | Role                                      | SOLID Principle        |
| ------------------------------ | ----------------------------------------- | ---------------------- |
| **Program to an Interface**    | Design guideline                          | Supported by DIP & OCP |
| **Dependency Inversion (DIP)** | High-level modules depend on abstractions | SOLID's 'D'            |
| **Open/Closed (OCP)**          | Extend without modifying                  | SOLID's 'O'            |


- Use **interfaces** alongside abstract classes for better flexibility.
    

### **6. Advantages of Abstraction**

- Simplifies complex systems.
- Promotes **loose coupling**.
- Enhances maintainability.
    

---

## **2. Inheritance**

### **1. Briefly explain Inheritance**

Inheritance allows a class (**subclass**) to inherit properties and methods from another class (**superclass**). It promotes **code reusability** and **hierarchical classification**.

### **2. Example of Inheritance**


```java
class Animal {
    void eat() {
        System.out.println("Animal eats.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks.");
    }
}
```

- **Explanation**: `Dog` inherits `eat()` from `Animal`.
    

### **3. Pros and Cons**

|**Pros**|**Cons**|
|---|---|
|Code reusability|Tight coupling between classes|
|Method overriding (Polymorphism)|Can lead to the **Diamond Problem** in multiple inheritance|
|Logical hierarchy|Difficult to modify superclass without breaking subclasses|

### **4. Common Problems & Famous Issues**

- **Diamond Problem** (In languages like C++ where multiple inheritance is allowed):
```c++
    
    // Hypothetical Java-like multiple inheritance (not allowed)
    class A {
     void show() { 
     System.out.println("A"); 
     } 
    }
    class B extends A {
     void show() {
      System.out.println("B"); 
      } 
    }
    class C extends A { 
    void show() { 
    System.out.println("C");
     } 
    }
    class D extends B, C {
     } // Which show() to call? Ambiguity!
```
    
- **Fragile Base Class Problem**: Changes in superclass break subclasses.
    

### **5. Ways to Resolve Problems**

- **Use Interfaces** (Java avoids multiple inheritance using interfaces).
    
- **Favor Composition over Inheritance** where applicable.
    

### **6. Advantages of Inheritance**

- **Reduces redundant code**.
- **Supports polymorphism**.

---

## **3. Polymorphism**

### **1. Briefly explain Polymorphism**

Polymorphism allows methods to behave differently based on the object. It has two types:

- **Compile-time (Method Overloading)**
- **Runtime (Method Overriding)**


### **2. Example of Polymorphism**

```java
class Calculator {
    int add(int a, int b) { return a + b; } // Overloading
    double add(double a, double b) { return a + b; }
}

class Animal {
    void sound() { System.out.println("Animal sound"); }
}

class Cat extends Animal {
    void sound() { System.out.println("Meow"); } // Overriding
}
```

### **3. Pros and Cons**

| **Pros**                         | **Cons**                                    |
| -------------------------------- | ------------------------------------------- |
| Flexible and extensible code     | Can lead to confusion if overused           |
| Supports dynamic method dispatch | Performance overhead (runtime polymorphism) |
### **Dynamic Method Dispatch & Polymorphism (Simplified Explanation)**

**Dynamic Method Dispatch** is the mechanism by which Java (and other OOP languages) **determines at runtime** which version of an **overridden method** to call, based on the **actual object type** (not the reference type).

This is a core feature of **Runtime Polymorphism**.

---

## **1. Key Concepts**

### **(1) Polymorphism**

- **"One interface, multiple implementations."**
- Two types:
    - **Compile-time (Static)** → Method Overloading.
    - **Runtime (Dynamic)** → Method Overriding + Dynamic Dispatch.
### **(2) Method Overriding**

- A subclass provides its own implementation of a method already defined in its superclass.
- Requires:
    - Same method name & parameters.
    - `@Override` annotation (recommended in Java).
### **(3) Dynamic Method Dispatch**

- The JVM (not the compiler) decides which overridden method to execute **at runtime** based on the **actual object type**.
---

## **2. How It Works?**

### **Example**
```java
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal;  // Reference of type Animal

        myAnimal = new Dog();  // Actual object is Dog
        myAnimal.makeSound();  // Output: "Dog barks" (Dynamic Dispatch)

        myAnimal = new Cat();  // Actual object is Cat
        myAnimal.makeSound();  // Output: "Cat meows" (Dynamic Dispatch)
    }
}

```
**Output:**
Dog barks  
Cat meows  

### **What Happens?**
1. **Compile-time:**
    - Compiler checks if `makeSound()` exists in `Animal`.   
    - It doesn’t know which subclass method will run.
        
2. **Runtime:**
    - JVM checks the **actual object type** (`Dog` or `Cat`).
    - Calls the appropriate overridden method.
### **4. Common Problems**
- **Method Signature Mismatch** (Overriding fails if signatures differ).
- **Accidental Overriding** (Using same method name unintentionally).
    

### **5. Ways to Resolve Problems**
- Use `@Override` annotation in Java to avoid mistakes.
- Follow **Liskov Substitution Principle (LSP)**.
    

### **6. Advantages of Polymorphism**

- **Enhances modularity**.
    
- **Makes code more flexible**.
    

---

## **4. Encapsulation**

### **1. Briefly explain Encapsulation**

Encapsulation is the bundling of data (variables) and methods into a single unit (class) while restricting direct access using **access modifiers** (`private`, `protected`, `public`).

### **2. Example of Encapsulation**

```java
class BankAccount {
    private double balance; // Hidden (encapsulated)

    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    public double getBalance() {
        return balance;
    }
}

```
### **3. Pros and Cons**

|**Pros**|**Cons**|
|---|---|
|Data protection|Can introduce boilerplate (getters/setters)|
|Prevents unauthorized access|Slightly more verbose|

### **4. Common Problems**

- **Exposing Mutable Objects** (Returning references to private fields).
    
```java
    class Employee {
        private List<String> projects;
        public List<String> getProjects() { return projects; } // Bad! Exposes internal list.
    }
```
### **5. Ways to Resolve Problems**
- Return **defensive copies** of mutable objects.
- Use **immutable objects** where possible.
    

### **6. Advantages of Encapsulation**
- **Improves security**.
- **Easier to maintain and debug**.
    

---

## **5. Composition**

### **1. Briefly explain Composition**

Composition is a design principle where a class contains objects of other classes (**"has-a" relationship**) instead of inheriting from them.

### **2. Example of Composition**

```java
class Engine {
    void start() { System.out.println("Engine starts."); }
}

class Car {
    private Engine engine; // Composition
    Car() { engine = new Engine(); }
    void start() { engine.start(); }
}
```

### **3. Pros and Cons**

| **Pros**                       | **Cons**                     |
| ------------------------------ | ---------------------------- |
| More flexible than inheritance | Slightly more boilerplate    |
| No tight coupling              | Requires explicit delegation |

### **4. Common Problems**

- **Overusing Composition** can make code complex.
    
### **5. Ways to Resolve Problems**

- Follow **"Favor Composition over Inheritance"** (Effective Java).
    
### **6. Advantages of Composition**

- **Better control over behavior**.
    
- **Avoids inheritance-related issues**.
    

---

## **6. Inheritance vs. Composition Debate**

### **When to Use Inheritance?**

- When there’s a clear **"is-a"** relationship (e.g., `Dog` is an `Animal`).
- When you need **polymorphism**.
    

### **When to Use Composition?**
- When you need **"has-a"** relationships (e.g., `Car` has an `Engine`).
- When you want **flexibility and loose coupling**.
    

### **Example Comparison**
```java
// Inheritance (Tight Coupling)
class Bird extends Animal { void fly() { } }
class Penguin extends Bird { } // Problem: Penguins can't fly!

// Composition (Flexible)
class Bird {
    private FlyingBehavior flyer; // Can be changed at runtime
    void fly() { flyer.fly(); }
}

```
### **Conclusion**

- **Inheritance** is useful for **strict hierarchies**.
- **Composition** is better for **flexibility and maintainability**.