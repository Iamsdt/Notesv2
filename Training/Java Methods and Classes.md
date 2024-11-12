---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - java
---


**1. What is a Method?**

* A *method* is a block of code that performs a specific task.  Think of it as a mini-program within your larger program.
* Methods help organize your code, make it reusable, and make it easier to understand.

**2. Defining a Method**

```java
returnType methodName(parameterType parameter1, parameterType parameter2, ...) {
  // Method body (the code that does the work)
  // ...
  return returnValue; // (If the method has a return type)
}
```

* `returnType`: The type of value the method returns (e.g., `int`, `String`, `void` if it doesn't return anything).
* `methodName`:  The name of the method (use meaningful names!).
* `parameterType`, `parameter1`: The types and names of the input values the method accepts (optional).
* `return returnValue`: Returns a value of the specified `returnType` (optional).

**3. Method Parameters**

* Parameters allow you to pass values *into* a method.
* The values passed to a method are called *arguments*.

```java
int add(int a, int b) {  // Method with two integer parameters
    return a + b;
}

// Calling the method:
int sum = add(5, 3); // 5 and 3 are the arguments
```

**4. Method Overloading**

* You can have multiple methods in the same class with the same name, but different parameters (either in number or type).
* This is called *method overloading*.

```java
double calculateArea(int side) { // Area of a square
    return side * side;
}

double calculateArea(double length, double width) { // Area of a rectangle
    return length * width;
}
```

**5. Method Scope**

* Variables declared *inside* a method are only accessible *within* that method. This is called *local scope*.

```java
void myMethod() {
    int x = 10; // x is only visible inside myMethod()
    // ...
}
```

**6. Method Recursion**

* A method can *call itself*. This is called *recursion*.
* Be careful!  You need a *base case* to stop the recursion, or it will run infinitely.

```java
int factorial(int n) {
    if (n == 0) {
        return 1; // Base case
    } else {
        return n * factorial(n - 1); // Recursive call
    }
}
```


**Java Classes - A Beginner's Guide**

**1. What is a Class?**

* A *class* is a blueprint or template for creating objects. Think of it as a cookie cutter.
* An *object* is an instance of a class – the actual cookie made using the cutter.
* Classes define the *data* (variables/attributes) and *behavior* (methods/functions) of objects.

**2. Basic Class Syntax**

```java
public class Dog { // Class declaration
    // Class members (variables and methods) go here
}
```

**3. Variables in a Class**

* *Instance variables*: Belong to each individual object. (Each cookie has its own sprinkles.)
* *Class variables*: Shared by all objects of the class.  (All cookies are made of the same dough.)

```java
public class Car {
    int year;            // Instance variable
    static String make = "Toyota"; // Class variable (shared)
}
```

**4. Methods in a Class**

* Methods define what objects of the class *can do*.  (A `Dog` object can `bark()`).
* (See the "Java Methods" section above for details on methods).

**5. Access Modifiers**

* Control the visibility and access to class members (variables and methods).
* `public`: Accessible from anywhere.
* `private`: Only accessible within the class itself.  (Encapsulation!)
* `protected`: Accessible within the package and by subclasses.
* (default/package-private): Accessible within the same package.

**6. Inner Classes**

* A class defined *inside* another class.

```java
public class OuterClass {
    // ...

    class InnerClass { // Inner class
        // ...
    }
}
```

**7. Encapsulation**

* Bundling data (variables) and the methods that operate on that data within a class, and protecting the data by making it `private`.
* Use *getter* and *setter* methods to access and modify private data in a controlled way.


**8. Putting it all together**

```java
public class Dog {
    private String name; // Private instance variable

    public Dog(String name) { // Constructor
        this.name = name;
    }


    public String getName() { // Getter method
        return name;
    }

    public void setName(String name) { // Setter method
        this.name = name;
    }

    public void bark() {
        System.out.println(name + " barks: Woof!");
    }

    public static void main(String[] args) {
        Dog myDog = new Dog("Buddy");
        System.out.println(myDog.getName()); // Accessing via getter
        myDog.bark();
    }
}

```
