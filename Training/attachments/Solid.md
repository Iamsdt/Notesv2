---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - coding
  - solid
---


### 1. **Single Responsibility Principle (SRP)**:
- **Definition**: A class should have only **one responsibility** or reason to change.
- **Car Example**: Imagine a `Car` class that handles **both driving the car** and **calculating fuel efficiency**. These are two different responsibilities. If something changes in fuel efficiency calculations, it shouldn't impact the driving logic. 
  - **Solution**: Create two separate classes: `Car` for driving and `FuelEfficiencyCalculator` for calculating fuel. Each class has one responsibility, making the system easier to maintain.

```java
class Car {
    void drive() {
        // Drive logic
    }
}

class FuelEfficiencyCalculator {
    double calculateFuelEfficiency(Car car) {
        // Fuel efficiency logic
        return 0;
    }
}
```

---

### 2. **Open/Closed Principle (OCP)**:
- **Definition**: A class should be **open for extension** but **closed for modification**. This means you should be able to add new functionality without changing existing code.
- **Car Example**: Let’s say your `Car` class has a method `start()`, and now you want to support different types of starting mechanisms like **electric start** and **key start**.
  - **Solution**: Instead of modifying the `Car` class every time you add a new start type, you can extend it by creating separate classes that implement a `StartStrategy`.

```java
interface StartStrategy {
    void start();
}

class ElectricStart implements StartStrategy {
    public void start() {
        System.out.println("Electric start");
    }
}

class KeyStart implements StartStrategy {
    public void start() {
        System.out.println("Key start");
    }
}

class KeyStart implements StartStrategy {
    public void start() {
        System.out.println("Key start");
    }
}

class Car {
    private StartStrategy startStrategy;

    public Car(StartStrategy startStrategy) {
        this.startStrategy = startStrategy;
    }

    void start() {
        startStrategy.start();
    }
}
```

---

### 3. **Liskov Substitution Principle (LSP)**:
- **Definition**: Subclasses should be able to **replace** their parent class without breaking the application.
- **Car Example**: If you have a `Car` class and a `ElectricCar` subclass, the `ElectricCar` should behave like a `Car` and not break the system.
  - **Bad Example**: If `ElectricCar` changes how `drive()` works in a way that breaks other parts of the system that expect a regular `Car` behavior, it would violate LSP.
  - **Solution**: The subclass should implement the parent class's behavior correctly.

```java
class Car {
    void drive() {
        System.out.println("Driving car");
    }
}

class ElectricCar extends Car {
    @Override
    void drive() {
        System.out.println("Driving electric car");
    }
}
```

---

### 4. **Interface Segregation Principle (ISP)**:
- **Definition**: A class should not be forced to implement interfaces it doesn't use. Instead, create smaller, more specific interfaces.
- **Car Example**: Imagine a `Vehicle` interface that requires all classes to implement methods like `fly()` and `drive()`. A `Car` should only implement methods it needs, like `drive()`, and not unrelated methods like `fly()`.
  - **Solution**: Split the `Vehicle` interface into smaller ones, so `Car` only implements what it needs.

```java
interface Drivable {
    void drive();
}

interface Flyable {
    void fly();
}

class Car implements Drivable {
    public void drive() {
        System.out.println("Car driving");
    }
}
```

---

### 5. **Dependency Inversion Principle (DIP)**:
- **Definition**: High-level modules should not depend on low-level modules; both should depend on abstractions.
- **Car Example**: If your `Car` class depends directly on an `Engine` class, and the `Engine` class changes, the `Car` class would break. Instead, both `Car` and `Engine` should depend on an abstraction (like an `Engine` interface).
  - **Solution**: Use interfaces or abstract classes to reduce the dependency between `Car` and specific engine implementations.

```java
interface Engine {
    void start();
}

class PetrolEngine implements Engine {
    public void start() {
        System.out.println("Petrol engine starting");
    }
}

class Car {
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }

    void startCar() {
        engine.start();
    }
}
```

### Summary:
- **SRP**: One class, one responsibility.
- **OCP**: Extend a class's behavior without modifying existing code.
- **LSP**: Subclasses should be replaceable for their parent class.
- **ISP**: Don't force a class to implement unnecessary methods.
- **DIP**: Depend on abstractions, not concrete classes.