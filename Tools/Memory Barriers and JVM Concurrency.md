The Java virtual machine is a model of a whole computer so this model naturally includes a memory model. The Java memory model specifies how the Java virtual machine works with the computer's memory (RAM). 

**The Java memory model specifies how and when different threads can see values written to shared variables by other threads, and how to synchronize access to shared variables when necessary.**
![[Screenshot 2025-02-03 at 2.27.29 PM.png]]

Each thread running in the Java virtual machine has its own thread stack. The thread stack contains information about **what methods the thread has called to reach the current point of execution**. **The thread stack also contains all local variables for each method being executed (all methods on the call stack).**

A thread can only access it's own thread stack. Local variables created by a thread are invisible to all other threads than the thread who created it.
One thread may pass a copy of a pritimive variable to another thread, but it cannot share the primitive local variable itself.
![[Screenshot 2025-02-03 at 3.21.32 PM.png]]




