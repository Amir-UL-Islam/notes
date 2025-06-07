A **race condition** happens when two or more threads access shared data **at the same time**, and the final outcome **depends on the order** in which the threads execute.

The `synchronized` keyword in Java is used to ensure **thread safety** — meaning that only one thread can access a block of code or method at a time. This prevents **race conditions** and **inconsistent data states** when multiple threads are trying to read/write shared resources.

### 🔐 Where it can be used:

1. **Instance methods**
2. **Static methods**
3. **Code blocks**

---

### ✅ 1. **Synchronized Instance Method**

Locks the current object (`this`) so only one thread per instance can execute it at a time.

java

CopyEdit

`public class Counter {     private int count = 0;      public synchronized void increment() {         count++;     } }`

---

### ✅ 2. **Synchronized Static Method**

Locks the class (`ClassName.class`) so only one thread per class (not instance) can access it at a time.

java

CopyEdit

`public class Counter {     private static int count = 0;      public static synchronized void increment() {         count++;     } }`

---

### ✅ 3. **Synchronized Block**

You can synchronize a specific block of code instead of the whole method. This improves performance by only locking critical sections.

java

CopyEdit

`public class Counter {     private int count = 0;      public void increment() {         synchronized (this) {             count++;         }     } }`

You can also use a custom lock object:

java

CopyEdit

`public class Counter {     private int count = 0;     private final Object lock = new Object();      public void increment() {         synchronized (lock) {             count++;         }     } }`