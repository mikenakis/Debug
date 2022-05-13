# mikenakis:debug

#### A tiny (~1 KB) library for debugging

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

You might ask: so what is the purpose of putting this class all by itself in a separate module, instead of just including a copy of the class in every project that needs it?

The thing is, the debugger must be configured with the fully qualified name of this class, which means that every copy of this class would have to have the exact same fully qualified name. Under normal circumstances it is not a problem, but for my testing needs I am using testana, and due to a bug currently in testana, it does not work very well if different modules contain classes with the exact same fully qualified name.

Once I fix this bug in testana, this library will not be necessary anymore.

## License

This software is published under the [Apache License, version 2.0](https://www.apache.org/licenses/LICENSE-2.0)

## Coding style

When I write code as part of a team of developers, I use the teams' coding style. However, when I write code for myself, I use _**my very own™**_ coding style. More information: [michael.gr - On Coding Style](https://blog.michael.gr/2018/04/on-coding-style.html)
