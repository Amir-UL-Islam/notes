## **Access Levels in Java**

|Modifier|Same Class|Same Package|Subclass (Different Package)|Other Classes|
|---|---|---|---|---|
|`private`|✅ Yes|❌ No|❌ No|❌ No|
|(default)|✅ Yes|✅ Yes|❌ No|❌ No|
|`protected`|✅ Yes|✅ Yes|✅ Yes|❌ No|
|`public`|✅ Yes|✅ Yes|✅ Yes|✅ Yes|

## **Summary of Relationships**

| Principle | Key Focus                                              | Relationship with DIP                                                                              |
| --------- | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------- |
| **DIP**   | Depend on abstractions, not concrete classes           | Helps in decoupling high-level and low-level modules                                               |
| **LSP**   | Subtypes must be replaceable without altering behavior | DIP relies on well-behaved abstractions; LSP ensures implementations respect abstraction contracts |
| **ISP**   | Interfaces should be small and focused                 | DIP depends on interfaces, and ISP ensures those interfaces are well-designed                      |
