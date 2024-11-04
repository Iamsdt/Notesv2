
Object-Oriented Programming (OOP) is a dominant programming paradigm that structures software design around "objects," which encapsulate both data (fields/attributes) and the procedures (methods/functions) that operate on that data. This approach offers significant advantages in terms of modularity, reusability, maintainability, and scalability.  Let's delve into the core OOP concepts, using an extended `Car` example and the concept of sealed classes.

**1. What is OOP?**

OOP shifts the focus from procedures to objects.  Instead of thinking primarily about *what actions to perform*, we think about *what objects are involved* and *how they interact*. This models real-world scenarios more effectively in software. A car, for instance, is an object with properties (color, year, model) and behaviors (starting, accelerating, braking). OOP allows us to represent these real-world entities as software objects.

**2. Class: The Blueprint**

A class acts as a blueprint or template for creating objects.  It defines the structure and behavior shared by all objects of that class.  Think of it like the design for a car model – it specifies the features and functionalities common to all cars of that model.

```java
public class Car extends Vehicle {  // Car class inheriting from Vehicle
    // Fields (data):
    private String color;
    private String key;
    private double fuelLevel;
    // ... other fields ...

    // Methods (behavior):
    public void start(String key) { /* ... implementation ... */ }
    public void drive(int miles) { /* ... implementation ... */ }
    // ... other methods ...
}
```

**3. Objects: Instances of a Class**

An object is an instance of a class – a concrete realization of the blueprint. Each car rolling off the assembly line is an object – an instance of the "Car" class. Each object has its own unique state (e.g., color, fuel level) even though they are all based on the same blueprint.

```java
Car myCar = new Car(2024, "myKey", "red", 50);  // Creating a Car object
Car yourCar = new Car(2023, "yourKey", "blue", 75); // Creating another Car object
```

**4. Abstraction: Hiding Complexity**

Abstraction simplifies interaction with objects by hiding unnecessary details. You interact with a car using the steering wheel, pedals, and gear stick, without needing to know the intricacies of the engine or transmission. Similarly, in OOP, abstraction presents a simplified interface to the user, concealing the complex internal workings. The drive() method abstracts away the fuel consumption calculations and other internal logic.

**Abstraction with Abstract Classes:**

An abstract class can contain both concrete methods (methods with implementations) and abstract methods (methods without implementations). Abstract methods act as placeholders; they define the *signature* of a method but don't provide the actual *implementation*.  Subclasses are then *required* to provide concrete implementations for these abstract methods.

```java
public abstract class Vehicle {  // Abstract class
    private int year;

    public Vehicle(int year) {
        this.year = year;
    }

    public int getYear() { // Concrete method
        return year;
    }

    public abstract void start(); // Abstract method – no implementation

    public abstract void stop(); // Abstract method – no implementation
}

public class Car extends Vehicle {
    // ... other Car fields and methods ...

    @Override
    public void start() { // Car MUST provide a start() implementation
        System.out.println("Car started");
    }

    @Override
    public void stop() { // Car MUST provide a stop() implementation
        System.out.println("Car stopped");
    }
}


public class Motorcycle extends Vehicle {
    // ... other Motorcycle fields and methods ...

    @Override
    public void start() { // Motorcycle MUST provide a start() implementation
        System.out.println("Motorcycle started");
    }

    @Override
    public void stop() { // Motorcycle MUST provide a stop() implementation
        System.out.println("Motorcycle stopped");
    }
}

```

Here, `Vehicle` is an abstract class.  It defines the common `start()` and `stop()` behaviors for all vehicles, but it doesn't provide specific implementations.  The `Car` and `Motorcycle` subclasses are *forced* to provide their own implementations of these methods. This is how abstract classes enforce a certain structure while allowing for flexibility in implementation.

**Abstraction with Interfaces:**

An interface defines a contract that classes can implement.  It contains only abstract methods (methods without implementations) and constants.  A class can implement multiple interfaces, achieving a form of multiple inheritance.

```java
interface Drivable { // Interface
    void drive(int miles);
    void turn(String direction);
}


public class Car extends Vehicle implements Drivable {
    // Car inherits from Vehicle AND implements Drivable.

    @Override
    public void drive(int miles) { // Implement drive from Drivable
        System.out.println("Car driving " + miles + " miles");
    }
    
    @Override
    public void turn(String direction) {
        System.out.println("Car turning " + direction);
    }
    // Override and implement the abstract methods from Vehicle
}


public class Motorcycle extends Vehicle implements Drivable {

    // Override and implement the abstract methods from Vehicle and Drivable
}


```


Here, the `Drivable` interface defines a contract for any class that represents something that can be driven.  The `Car` class implements this interface, providing concrete implementations for the `drive()` and `turn()` methods. This further separates the *what* (the interface definition) from the *how* (the specific implementation in `Car`).


**5. Encapsulation: Protecting Data Integrity**

Encapsulation bundles the data (fields) and the methods that operate on that data within the class, controlling access to that data.  This protects the data from unwanted external modification and ensures data consistency.  The `private` keyword in Java enforces this access control.

```java
private double fuelLevel;  // Only accessible from within the Car class

public double getFuelLevel() { // Controlled access to fuelLevel
    return fuelLevel;
}

public void addFuel(double amount) { // Safe modification of fuelLevel
    fuelLevel += amount;
}
```

**6. Inheritance: Building Relationships**

Inheritance allows creating new classes (derived classes or subclasses) based on existing classes (base classes or superclasses).  The derived class inherits the properties and methods of the base class and can extend or modify them. This promotes code reuse and establishes "is-a" relationships between classes.


```java
public sealed class Vehicle permits Car, Truck, Motorcycle { // Sealed class
    private int year;
    // ... other fields and methods common to all vehicles ...
}

public final class Car extends Vehicle { // Car inherits from Vehicle
    // ... Car-specific fields and methods ...
}

public final class Truck extends Vehicle { // Truck also inherits from Vehicle
    // ... Truck-specific fields and methods ...
}

public non-sealed class Motorcycle extends Vehicle { // Motorcycle also inherits and can be extended
    // ... Motorcycle-specific fields and methods ...
}

```

The `sealed` keyword in Java (introduced in Java 17) allows you to restrict which classes can inherit from a sealed class.  Here, only `Car`, `Truck` and `Motorcycle` are permitted to inherit from `Vehicle`. Any attempt to create another subclass of `Vehicle` will result in a compile-time error. This enhances control over the class hierarchy and helps maintain code integrity. Making `Car` `final` prevent further subclassing. You can also specify `non-sealed` classes when extending a sealed class which opens inheritance again for that particular class (e.g. `Motorcycle`). This allows for flexible inheritance structures.

**7. Polymorphism: Flexibility and Reusability**

Polymorphism, meaning "many forms," allows objects of different classes to be treated as objects of a common type. This enables writing code that can work with objects of various types without needing to know their specific class.


```java
Vehicle myVehicle = new Car(2024, "carKey", "red", 50); // Polymorphism
myVehicle = new Truck(2023, 8000); // Now myVehicle references a Truck
myVehicle.getYear();    // Works for both Car and Truck objects

List<Vehicle> vehicles = new ArrayList<>();
vehicles.add(new Car(...));
vehicles.add(new Truck(...));
vehicles.add(new Motorcycle(...)); // Store different vehicle types

for (Vehicle v : vehicles) {
  System.out.println("Year: " + v.getYear()); // Process all vehicles uniformly
}
```
