Here we will discuss four major configurations which include:  
**implementation**, **api**, **compileOnly** and **runtimeOnly**

![](https://miro.medium.com/v2/resize:fit:1400/1*wUA8syAGZD9SgHlCOPmdUw.png)

# What are dependency and its configurations?

As a developer, we often need external or internal libraries or modules in our project. When a project, module, or library depends on further modules or libraries hence these modules or libraries on which we depend are called dependencies.

Every dependency declared for a Gradle project applies to a specific scope. For example, some dependencies should be used for compiling source code whereas others only need to be available at runtime. Gradle represents the scope of a dependency with the help of a [Configuration](https://docs.gradle.org/current/dsl/org.gradle.api.artifacts.Configuration.html).

# Why configurations understanding is important?

Each configuration provides a specific scope to a dependency. If we want we can choose a bigger scope than required and it will not throw any error, everything will work fine but with some hidden cost. A better understanding of configurations will help us to remove that hidden cost too.

Choosing a wrong configuration can lead to a bigger size of the build, slower compilation, more recompilation, and/or accidental use of the library which we are not using explicitly.

> **The advantage of choosing the right configuration:**  
> 1. Cleaner classpaths(via right use of configurations,a module will only know about the required modules hence it will lead to simpler and cleaner classpath)  
> 2. Faster compilation due to cleaner classpath  
> 3. Less recompilation (if code change happens in runtime classpath for a module then this module don’t need to recompile)  
> 4. Smaller build size (if we will use compileOnly*)  
> 5. Avoid accidental use of the library which we are not using explicitly  
> 6. Dynamic behaviour of a library (runtimeOnly*)

The core difference between all of the above configurations is how they help us to control the **compile classpath** and **runtime classpath** for a dependency on a **module** and its **consumers**.

**Compile classpath**  
In simple words, we will be able to access only those Classes which will be in its compile classpath, if we try to use a module that is not available in its classpath then the build will fail at compile-time.

**Runtime classpath**  
Classes that would be accessible at runtime, which is only possible after generation of the final build. Hence it will decide whether a class would become part of the final build or not (e.g. apk, jar, and war)

**Configuration Comparison Table:**

![](https://miro.medium.com/v2/resize:fit:1400/1*dYRfyIo404QvgkbmLIiBDw.png)

## **To understand the above table with api example:**

![](https://miro.medium.com/v2/resize:fit:2000/1*h4Bosu3HdWMEgxPctxRuxw.png)

**Two main points in the above example I would like to focus on are:**

**1: Availability**  
Since we are using **api** project(‘:Lib-B’) in **Lib-A** hence **Lib-B** would be available to **Lib-A** at both compile and runtime.

**2: Leak/Expose of a dependency**  
Since we are using **api** project(‘:Lib-B’) in **Lib-A** hence **Lib-B** would leak to the consumer of **Lib-A** which is our main-module in the above example hence Lib-B would be available to main-module at both compile and runtime.

# Details of “**implementation”**

We will use implementation when we don’t want to expose the dependencies to the consumer’s compile classpath but want to expose to runtime classpath.

This means we will not be able to access the code in the consumer module but these dependencies will become part of the final build.

> Earlier we had a configuration called **compile(Deprecated)** which leak dependencies to the consumer’s compile-classpath which can cause dependency pollution (means unnecessary recompile and accidental use of transitive dependency).
> 
> **Two newer alternatives to compile are:**
> 
> **api** (same as compile it also leaks(exposes) dependencies to the consumer’s compile-classpath)
> 
> **implementation** (same as compile except it doesn’t expose the dependencies to consumer’s compile classpath)

![](https://miro.medium.com/v2/resize:fit:1400/1*yq-wLayexPYR_vrYljBqeg.png)

To understand **implementation** consider a case where we want to make an image-loader library and inside our image-loader library, we are using a network-manager library.  
Here we don’t want to expose the network-manager library to the consumers of image-loader compile-time classpath (but will become part of runtime).

But if the network-manager will anyway become part of the final build why we want to hide it from the consumer compile classpath. Let's discuss the advantages to hide it from the consumer compile classpath.

## **Advantage of “implementation” over “api”**

**To avoid accidental use of the library:**  
If we leak the network-manager lib then there is a possibility that some consumers of our imager-loader library will start using it. And if tomorrow we want to change the network-manager lib with some other one then it could the breaking change for the consumers who were using network-module via our image-loader library.

**Faster compilation:**  
Since now we will have a cleaner compile classpath, hence it will lead to lesser compilation time.

**Lesser Recompilation:**  
Change in the network-manager library doesn’t need to recompile the consumer(main-module) of the image-loader library. (But image-loader will need recompile since it can access the network-module inside it)

# Details of “**api”**

Dependencies declared as api will be transitively exported to consumers runtime and compile-time both.

==Now we already discuss the negative== side of using api. but when we should use it, let us understand this via an example.

![](https://miro.medium.com/v2/resize:fit:1400/1*2sUq1dUVfraNYaHjszX2tw.png)

To understand **api** consider the case where we are exposing the other library object from our own library class.  
For example, we have the same image loader library but we also provide one additional feature of ImageTransformation and since image-transformation itself can be used as an independent library to other modules we made it as a separate lib and use as a dependency in our image-loader module. Now since we want to use the image-transformation classes as a parameter or return type in image-loader, then we have to pass it(image-transformation) to consumers compile-classpath hence we will use api.

# Details of “**compileOnly”**

We will use compileOnly when we just want to use it at compile time only and don’t want to have it on the final build(runtime).

Since it doesn’t include to final build which leads to a smaller build size.

> **compileOnly** configuration behaves just like **provided** (which is now **deprecated**)

![](https://miro.medium.com/v2/resize:fit:1400/1*lNzbws3D-LCx1aU6M5nC3w.png)

One of the best example to understand is the Lombok library, Lombok is a library which helps generate the boilerplate code at compile-time with the help of annotations( e.g. to generate getter and setter) and since its scope is only limited to compile-time hence we should use compileOnly.

# Details of “**runtimeOnly”**

when we don't want the dependency at compile time but do need it at runtime.

> Android: This configuration behaves just like **apk** configuration (which is now **deprecated**).

This is a rarely used configuration and less easy to digest than others hence let's understand it via examples :

**Example 1:**[SLF4J](https://www.slf4j.org/) is one of the best examples of runtimeOnly, where we will use slf4j-api as implementation configuration and implementation of slf4j-api (like slf4j-log4j12 or logback-classic, etc) as runtimeOnly configuration.

**Example 2:**

![](https://miro.medium.com/v2/resize:fit:1400/1*RFEuNIfRYGMr6dbHPTwtgg.png)

Another way is to use with compileOnly configuration. Consider a case where we want to log the message via logger library, but we want to change the behavior for the runtime. Hence we will create a logger-api module that will only have the structure of Logger class so that we can use it on main-module at compile-time. We will create two different modules (logger-systrace and logger-crashlytics) with the same structure but different behavior and we will use one of these modules (logger-systrace and logger-crashlytics) as runtimeOnly.  
Now since logger-systrace or logger-crashlytics will be add at runtime hence recomiple would only occur to changed module(logger-systrace or logger-crashlytics)

# Conclusion:

1. **implementation**: mostly we are using implementation configuration and it hides the internal dependency of the module to its consumer to avoid accidental use of any transitive dependency, hence faster compilation and less recompilation.  
2. **api:** must be used very carefully, since it leaks the to consumer’s compile classpath, hence misusing of api could lead to dependency pollution.  
3. **compileOnly**: when we don’t need any dependency at runtime, since compileOnly dependency won’t become the part of the final build. we will get a smaller build size.  
4. **runtimeOnly**: when we want to change or swap the behavior of the library at runtime (in final build).