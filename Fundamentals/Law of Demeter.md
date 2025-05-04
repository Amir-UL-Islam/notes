The Law of Demeter defines, how objects interact with each other. It says that you should talk only to the object that you directly know.

The law of Demeter simplifies methods by limiting the number of used types inside them. It promotes information hiding with proper abstraction and narrow interfaces.

A single method can only operate on objects that are:
- Passed as arguments to the method
- Values of fields defined in this class
In addition to that, ==all globally available values==, or objects created within methods, can also be used, as they are considered as method arguments.