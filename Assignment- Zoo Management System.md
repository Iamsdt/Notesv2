#### Objective:
To develop a Java application simulating a simple zoo management system using OOP principles. The system will include a base `Animal` class and various animal subclasses (`Mammal`, `Bird`, `Fish`) with specific behaviors, showcasing inheritance, polymorphism, encapsulation, and abstraction.

---

### Requirements:

#### 1. **Base Class - `Animal`**
   - **Attributes**:
     - `String name` (e.g., "Elephant")
     - `int age` (e.g., 5 years)
     - `String species` (e.g., "African Elephant")
   - **Constructor**:
     - Create a parameterized constructor to initialize `name`, `age`, and `species`.
   - **Methods**:
     - `void eat()` - Displays a message that the animal is eating (e.g., "The animal is eating").
     - `void sleep()` - Displays a message that the animal is sleeping (e.g., "The animal is sleeping").
     - `void makeSound()` - Displays a generic sound message like "This animal makes a sound."
     - `void displayInfo()` - Prints all details of the animal (name, age, species).

#### 2. **Derived Class - `Mammal`**
   - **Inherits** from `Animal`.
   - **Additional Attribute**:
     - `boolean isAquatic` (e.g., true if the mammal is an aquatic mammal like a dolphin)
   - **Constructor**:
     - Initialize `isAquatic` along with inherited attributes (`name`, `age`, `species`).
   - **Override Methods**:
     - `void makeSound()` - Provide a specific sound message for mammals (e.g., "The mammal roars or grunts").
   - **Additional Methods**:
     - `void swim()` - Displays a message like "The mammal is swimming" if `isAquatic` is true.

#### 3. **Derived Class - `Bird`**
   - **Inherits** from `Animal`.
   - **Additional Attributes**:
     - `double wingspan` (e.g., wingspan in meters)
     - `boolean canFly` (e.g., false if the bird is flightless like an ostrich)
   - **Constructor**:
     - Initialize `wingspan` and `canFly` along with inherited attributes.
   - **Override Methods**:
     - `void makeSound()` - Provide a specific sound for birds (e.g., "The bird chirps or squawks").
   - **Additional Methods**:
     - `void fly()` - Display a message like "The bird is flying" if `canFly` is true, otherwise say "This bird cannot fly."

#### 4. **Derived Class - `Fish`**
   - **Inherits** from `Animal`.
   - **Additional Attribute**:
     - `String waterType` (e.g., "Freshwater" or "Saltwater")
   - **Constructor**:
     - Initialize `waterType` along with inherited attributes.
   - **Override Methods**:
     - `void makeSound()` - Since fish typically don’t make audible sounds, display a message like "Fish are generally silent."
   - **Additional Methods**:
     - `void swim()` - Display a message like "The fish is swimming in `waterType` water."

#### 5. **Interface - `Care`**
   - **Methods**:
     - `void receiveCare()` - Method signature for administering care to the animal.
   - Implement this interface in each derived class (`Mammal`, `Bird`, `Fish`), with each class providing a unique message for care (e.g., "The mammal is being groomed" or "The bird is having its feathers preened").

#### 6. **Polymorphism and Testing**
   - **Create a `ZooManager` class** with a `main` method to:
     - Instantiate several animals of different types.
     - Store them in an array or list of `Animal` objects.
     - Use a loop to iterate over the array and:
       - Call `eat()`, `makeSound()`, and `displayInfo()` methods for each animal.
       - If an animal is of type `Bird`, call `fly()`.
       - If an animal is of type `Fish` or `Mammal` (and has a `swim()` method), call `swim()`.

#### 7. **Sample Output**
   - Demonstrate that each animal’s overridden behaviors are called correctly, and that polymorphism allows the `ZooManager` class to interact with all `Animal` objects seamlessly.
