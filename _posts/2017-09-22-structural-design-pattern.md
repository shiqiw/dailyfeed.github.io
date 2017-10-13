---
layout: post
title: "Structural design pattern"
date: 2017-09-21
permalink: /technique/:year/:month/:day/:title
section: "technique"
---

### Goal
In software engineering, structural design patterns are design patterns that ease the design by identifying a simple way to realize relationships between entities.

### Adapeter pattern
The adapter pattern is a design pattern that is used to allow two incompatible types to communicate. (Correlated design principal: dependency inversion)

![Figure 1]({{ site.url }}/assets/adapter.jpg){:class="post-image"}

### Bridge pattern
A design pattern that separates the abstract elements of a class from its technical implementation. This provides a cleaner implementation of real-world objects and allows the implementation details to be changed easily.

On of the biggest benefits of Bridge pattern is ability to change implementation details at run time. This could permit the user to switch implementations to determine how the software interoperates with other systems.

![Figure 2]({{ site.url }}/assets/bridge.jpg){:class="post-image"}

### Composite pattern
A design pattern that is used when creating hierarchical object models. The pattern defines a manner in which to design recursive tree structures of objects, where individual objects and groups can be accessed in the same manner.

![Figure 3]({{ site.url }}/assets/composite.jpg){:class="post-image"}

### Decorator pattern
The decorator pattern is a design pattern that extends the functionality of individual objects by wrapping them with one or more decorator classes. These decorators can modify existing members and add new methods and properties at run-time.

![Figure 4]({{ site.url }}/assets/decorator.jpg){:class="post-image"}

### Facade pattern
The facade pattern is a design pattern that is used to simplify access to functionality in complex or poorly designed subsystems. The facade class provides a simple, single-class interface that hides the implementation details of the underlying code.

![Figure 5]({{ site.url }}/assets/facade.jpg){:class="post-image"}

### Flyweight pattern
The flyweight pattern is a design pattern that is used to minimize resource usage when working with very large numbers of objects. When creating many thousands of identical objects, stateless flyweights can lower the memory used to a manageable level.

![Figure 6]({{ site.url }}/assets/flyweight.jpg){:class="post-image"}

### Proxy pattern
Proxy in a most general form is an interface to something else (Subject class). Proxy can be used when we don’t want to access to the resource or subject directly because of some base of permissions or if we don’t want to expose all of the methods of subject class. In some cases proxies can add some extra functionality. Using proxies is very helpful when we need to access resources which are hard to instantiate, are slow to execute or are resource sensitive.

![Figure 7]({{ site.url }}/assets/proxy.jpg){:class="post-image"}

### Reference
1. [Structural Design Patterns](https://www.codeproject.com/articles/438922/design-patterns-of-structural-design-patterns#Introduction)