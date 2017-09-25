---
layout: post
title: "Creational design pattern"
date: 2017-09-17
permalink: /technique/:year/:month/:day/:title
section: "technique"
---

### Abstract factory
A Factory now represents a "family" of objects that it can create. This family of objects created by factory is determined at run-time according to the selection of concrete factory class.

![Figure 1]({{ site.url }}/assets/abstract-factory.jpg){:class="post-image"}

### Builder
A design pattern that allows for the step-by-step creation of complex objects using the correct sequence of actions.

![Figure 2]({{ site.url }}/assets/builder.jpg){:class="post-image"}

### Factory
A design pattern that allows for the creation of objects without specifying the type of object that is to be created in code. A factory class contains a method that allows determination of the created type at run-time. This pattern is also known as Virtual Constructor pattern.

![Figure 3]({{ site.url }}/assets/factory.jpg){:class="post-image"}

### Prototype
A design pattern that is used to instantiate a class by copying, or cloning, the properties of an existing object. The new object is an exact copy of the prototype but permits modification without altering the original.

![Figure 4]({{ site.url }}/assets/prototype.jpg){:class="post-image"}

### Singleton
A design pattern that is used to ensure that a class can only have one concurrent instance. Whenever additional objects of a singleton class are required, the previously created, single instance is provided.

```java
    public sealed class Singleton
    {
        private static volatile Singleton _instance;
        private static readonly object _lockThis = new object();

        private Singleton() { }

        public static Singleton GetSingleton()
        {
            if (_instance == null)
            {
                lock (_lockThis)
                {
                    if (_instance == null) _instance = new Singleton();
                }
            }
            return _instance;
        }
    }
```

![Figure 5]({{ site.url }}/assets/singleton.jpg){:class="post-image"}

### Reference
1. [Creational Design Patterns](https://www.codeproject.com/Articles/430590/Design-Patterns-of-Creational-Design-Patterns)
