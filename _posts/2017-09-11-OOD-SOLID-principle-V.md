---
layout: post
title: "OOD SOLID principle V"
date: 2017-09-11
permalink: /technique/:year/:month/:day/:title
section: "technique"
---

### Dependency inversion principle
High level modules should not depend upon low-level modules. Both should depend upon abstractions.

Abstractions should never depend upon details. Details should depend upon abstractions.

在传统的应用架构中，低层次的组件设计用于被高层次的组件使用，这一点提供了逐步的构建一个复杂系统的可能。在这种结构下，高层次的组件直接依赖于低层次的组件去实现一些任务。这种对于低层次组件的依赖限制了高层次组件被重用的可行性。

依赖反转原则的目的是把高层次组件从对低层次组件的依赖中解耦出来，这样使得重用不同层级的组件实现变得可能。把高层组件和低层组件划分到不同的包/库（在这些包/库中拥有定义了高层组件所必须的行为和服务的接口，并且存在高层组件的包）中的方式促进了这种解耦。由于低层组件是对高层组件接口的具体实现，因此低层组件包的编译是依赖于高层组件的。

From
```java
package com.tidyjava.weather;

import com.tidyjava.weather.api1.WeatherApi1;
import com.tidyjava.weather.api2.WeatherApi2;

public class WeatherAggregator {
    private WeatherApi1 weatherApi1 = new WeatherApi1();
    private WeatherApi2 weatherApi2 = new WeatherApi2();

    public double getTemperature() {
        return (weatherApi1.getTemperatureCelcius() + toCelcius(weatherApi2.getTemperatureFahrenheit())) / 2;
    }

    private double toCelcius(double temperatureFahrenheit) {
        return (temperatureFahrenheit - 32) / 1.8f;
    }
}
```

To
```java
// --------------------------- //
package com.tidyjava.weather;

public interface WeatherSource {
    float getTemperatureCelcius();
}

// --------------------------- //
package com.tidyjava.weather.api2;

import com.tidyjava.weather.WeatherSource;

public class WeatherApi2 implements WeatherSource {
    @Override
    public double getTemperatureCelcius() {
        return toCelcius(getTemperatureFahrenheit());
    }

    private double getTemperatureFahrenheit() {
        // some logic
    }

    private double toCelcius(double temperatureFahrenheit) {
        return (temperatureFahrenheit - 32) / 1.8f;
    }
}

// --------------------------- //
package com.tidyjava.weather;

import java.util.List;

public class WeatherAggregator {
    private List<WeatherSource> weatherSources;

    public WeatherAggregator(List<WeatherSource> weatherSources) {
        this.weatherSources = weatherSources;
    }

    public double getTemperature() {
        return weatherSources
            .stream()
            .mapToDouble(WeatherSource::getTemperatureCelcius)
            .average()
            .getAsDouble();
    }
}
```

### Adapter pattern
与之相关的有Adapter pattern。Ref 2中有详细解释。

Adapter Pattern is a design pattern that allows us to use a class via an interface it does not derive from. It is implemented in two variations – class adapter (using inheritance) and object adapter (using composition). 

Adapter pattern can be used to invert a dependency on a class that is not under our control (e.g. create an adapter that implements WeatherSource and internally uses SpringWeatherApi.)

```java
public class SpringWeatherApiAdapter implements WeatherSource {
    private SpringWeatherApi weatherApi;

    public SpringWeatherApiAdapter(SpringWeatherApi weatherApi) {
        this.weatherApi = weatherApi;
    }

    @Override
    public double getTemperatureCelcius() {
        return toCelcius(weatherApi.getTemperatureFahrenheit());
    }

    private double toCelcius(double temperatureFahrenheit) {
        return (temperatureFahrenheit - 32) / 1.8f;
    }
}
```

### Look further: Composite
The composite pattern describes a group of objects that is treated the same way as a single instance of the same type of object. The intent of a composite is to "compose" objects into tree structures to represent part-whole hierarchies.

From
```java
public class WeatherAggregator {
    private WeatherApi1 weatherApi1;
    private WeatherApi2 weatherApi2;

    public WeatherAggregator(WeatherApi1 weatherApi1, WeatherApi2 weatherApi2) {
        this.weatherApi1 = weatherApi1;
        this.weatherApi2 = weatherApi2;
    }
    // rest of the logic
}
```
To
```java
public class WeatherAggregator {
    private List<WeatherSource> weatherSources;

    public WeatherAggregator(List<WeatherSource> weatherSources) {
        this.weatherSources = weatherSources;
    }

    public double getTemperature() {
        return weatherSources
            .stream()
            .mapToDouble(WeatherSource::getTemperatureCelcius)
            .average()
            .getAsDouble();
    }
}
```

### Reference
1. [依赖反转原则](https://zh.wikipedia.org/wiki/%E4%BE%9D%E8%B5%96%E5%8F%8D%E8%BD%AC%E5%8E%9F%E5%88%99)
2. [Adapter pattern](http://tidyjava.com/dependency-inversion-in-java/)