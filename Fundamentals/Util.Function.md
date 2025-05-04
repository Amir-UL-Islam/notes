A gateway into Functional world for Java Developers
> Core
- Function<T, R> 
	- R as return Type and T is the input parameter Type
	- `R apply(T t)`
- BiFunction<T, U, R> 
	- R as Return Type and T & U as Inputs
	- `R apply(T t, U u)`
	
- Predicate<T. >
	- Returns weather T is True or False
	- `boolean test(T t)` 
- BiPredicate<T, U>
	- Also Returns boolean Type
	-  `boolean test(T t, U u)
- Consumer<T.>
	- Takes an Input and Make Side Effect to it and Dose not returns anything[If you are like me Could not help yourself to find out Code implementation]
	-  `void accept(T t)`
	- ``