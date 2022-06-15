# mikenakis:debug

#### A tiny (~1 KB) library to help with debugging

<p align="center">
<img title="mikenakis:debug logo" src="mikenakis-debug-logo.svg" width="256"/><br/>
The mikenakis:debug logo<br/>
by Mike Nakis<br/>
based on <a href="https://thenounproject.com/icon/ladybug-17110/">original work</a> by <a href="https://thenounproject.com/crosedesign/">Cassandra Bachman</a> from <a href="https://thenounproject.com/">the Noun Project</a><br/>
used under <a href="https://creativecommons.org/licenses/by/3.0/us/">CC BY</a> license.<br/>
</p>

## Description
     
A tiny library (the jar file is under 1 KB) containing a single class with few methods that are crucial for debugging.

For an explanation as to why this is needed, I am going to do some writeup; until then, see https://stackoverflow.com/q/71115356/773113 to get an idea.

Step-by-step guide to configure the IntelliJ IDEA debugger to take advantage of the functionality of theis module:

  - Go to "Run" -> "View Breakpoints..."
    - Under "Java Exception Breakpoints":
      - You should already have one entry for "Any exception" where "Caught exception" is ***unchecked*** and "Uncaught exception" is ***checked*** so that your debugger always stops on any uncaught exception thrown anywhere. We will now add one more exception breakpoint so that your debugger can stop on caught exceptions that are caught by any method in the `Debug` class I showed above.
      - Add a Java Exception Breakpoint.
      - Set the exception class to be `java.lang.Throwable`.
        - PEARL: In the "Search by name" tab of the "Enter Exception Class" dialog, if you check the 'Include non-project items' box and start typing 'Throwable' or 'java.lang.Throwable', IntelliJ IDEA will fail/refuse to find `Throwable`, presumably because it is covered by the 'Any exception' entry which they are already providing, and they cannot imagine why one would need to add one more entry for the same exception class. Luckily, their mechanism of preventing you from finding `Throwable` is half-assed, so it can be circumvented, as follows:
          - Switch to the 'Project' tab instead of the 'Search by Name' tab.
          - Navigate to 'External Libraries', then to your JDK, then to the `java.base` module, then to the `java.lang` package
          - Locate `Throwable` and select it.
      - Ensure "Caught exception" is **checked**.
      - Check the checkbox of "Catch class filters:" and enter `io.github.mikenakis.Debug`.
      - PEARL: The "Breakpoints" dialog of IntelliJ IDEA contains many text boxes expecting class names, and in any of these text boxes you can enter any random garbage, and IntelliJ IDEA will happily accept it, without the slightest hint that it is wrong. Then, when you expect it to break, it will silently fail to break. To avoid this, never type a class name in any of these text boxes, always use the navigation feature to locate a class which is guaranteed to exist. (And good luck if you ever decide to rename or move that class.)

You might ask: so what is the purpose of putting this class all by itself in a separate module, instead of just including a copy of the class in every project that needs it?

The thing is, the debugger must be configured with the fully qualified name of this class, which means that every copy of this class would have to have the exact same fully qualified name. Under normal circumstances it is not a problem, but for my testing needs I am using testana, and due to a bug currently in testana, it does not work very well if different modules contain classes with the exact same fully qualified name.

Once I fix this bug in testana, this library will not be necessary anymore.

## License

This software is published under the [Apache License, version 2.0](https://www.apache.org/licenses/LICENSE-2.0)

## Coding style

When I write code as part of a team of developers, I use the teams' coding style. However, when I write code for myself, I use _**my very own™**_ coding style. More information: [michael.gr - On Coding Style](https://blog.michael.gr/2018/04/on-coding-style.html)
