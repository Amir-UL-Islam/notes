The basic idea of a Domain-Specific Language (DSL) is a computer language that's targeted to a particular kind of problem, rather than a general purpose language that's aimed at any kind of software problem.

DSLs are very common in computing: examples include CSS, regular expressions, make, rake, ant, SQL, HQL, many bits of Rails, expectations in JMock, graphviz's dot language, FIT, strut's configuration file....

An important and useful distinction I make is between internal and external DSLs. **==Internal DSLs==** ==are particular ways of using a host language to give the host language the feel of a particular language.== This approach has recently been popularized by the Ruby community although it's had a long heritage in other languages - in particular Lisp. Although it's usually easier in low-ceremony languages like that, you can do effective internal DSLs in more mainstream languages like Java and C#. Internal DSLs are also referred to as embedded DSLs or FluentInterfaces

**External DSLs** have their own custom syntax and you write a full parser to process them. There is a very strong tradition of doing this in the Unix community. Many XML configurations have ended up as external DSLs, although XML's syntax is badly suited to this purpose.

DSLs can be implemented either by interpretation or code generation. Interpretation (reading in the DSL script and executing it at run time) is usually easiest, but code-generation is sometimes essential. Usually the generated code is itself a high level language, such as Java or C.