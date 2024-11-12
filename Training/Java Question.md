---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - java
---


### Stream
3. Declarative Approach to Data Processing
4. Immutability and Clean Code
5. Support for Parallel Processing **parallelStream** leading to **faster execution on large datasets**.


**Sealed Classes** in Java, introduced in **Java 17**, restrict which classes can extend or implement them. By declaring a class as `sealed`, the developer explicitly controls its subclassing, ensuring only specific classes can extend it. This is useful for modeling closed hierarchies where the number of subclasses is fixed.

### Key Points:
- **Syntax**: Use the `sealed` keyword, followed by a `permits` clause to specify allowed subclasses.
- Subclasses must be `final`, `non-sealed`, or `sealed`.
  
### Example:
```java
public sealed class Shape permits Circle, Square {
    // common properties and methods
}

public final class Circle extends Shape { }
public final class Square extends Shape { }
```

**Benefits**:
- **Better control over class hierarchies**.
- **Improved maintainability** and **exhaustive pattern matching**.


### Virtual Threads
**Virtual Threads**, introduced in **Project Loom** (Java 19 Preview), are lightweight threads managed by the JVM, allowing for high concurrency with minimal resource overhead. Unlike traditional OS threads, virtual threads are not tied to a specific OS thread, making them more scalable and efficient for I/O-bound tasks.

**Key Points**:
- **Lightweight**: Thousands or millions of virtual threads can run concurrently without consuming large system resources.
- **Non-blocking**: Blocking a virtual thread (e.g., for I/O) doesn't block the underlying OS thread, enabling better resource utilization.


**Structured Concurrency** is a concurrency paradigm where tasks are organized in a **structured and scoped manner**. Instead of managing threads manually, tasks are grouped into hierarchies, ensuring that parent tasks control and manage the lifecycles of their child tasks, making concurrency more predictable and easier to reason about.
**Key Points**:
- **Task hierarchies**: Parent tasks are responsible for managing child tasks.
- **Automatic resource cleanup**: Helps avoid thread leaks and simplifies error handling.
- **Improves readability**: Concurrency flows are structured like nested function calls, making code more maintainable.

Epsilon Garbage Collector (GC) vs  Z Garbage Collector (ZGC)

The **Z Garbage Collector (ZGC)** is a scalable, low-latency garbage collector introduced in **Java 11** and stabilized in **Java 15**. ZGC is designed for applications requiring **large heaps** and **low GC pause times** (typically less than 10 ms), even with heap sizes up to **terabytes**.


### 1. Singleton Pattern
Ensures that a class has only one instance and provides a global access point to it.

**Code Example**:
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() { } // private constructor

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

---

### 2. Observer Pattern
Defines a one-to-many relationship between objects, so when one object changes state, the others are notified automatically.

**Code Example**:
```java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update(String message);
}

class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

class ConcreteObserver implements Observer {
    @Override
    public void update(String message) {
        System.out.println("Received update: " + message);
    }
}
```

---

### 3. Factory Method Pattern
Delegates object creation to subclasses to promote flexibility and extendibility.

**Code Example**:
```java
abstract class Product {
    abstract void use();
}

class ConcreteProductA extends Product {
    @Override
    void use() {
        System.out.println("Using Product A");
    }
}

class ConcreteProductB extends Product {
    @Override
    void use() {
        System.out.println("Using Product B");
    }
}

abstract class Creator {
    abstract Product createProduct();
}

class ConcreteCreatorA extends Creator {
    @Override
    Product createProduct() {
        return new ConcreteProductA();
    }
}

class ConcreteCreatorB extends Creator {
    @Override
    Product createProduct() {
        return new ConcreteProductB();
    }
}
```


